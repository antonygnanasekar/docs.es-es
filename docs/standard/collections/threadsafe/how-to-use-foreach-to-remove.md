---
title: "Cómo: Utilizar ForEach para quitar elementos de BlockingCollection"
description: "Cómo: Utilizar ForEach para quitar elementos de BlockingCollection"
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: f3db5825-b5c9-4e8b-80bc-e11760d9523e
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: ccee6060aa95b80f424a959e76ceabede473ed86
ms.lasthandoff: 03/02/2017

---

# <a name="how-to-use-foreach-to-remove-items-in-a-blockingcollection"></a>Cómo: Utilizar ForEach para quitar elementos de BlockingCollection

Además de obtener los elementos de [BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) usando los métodos `Take` y `TryTake`, también puede usar un bucle de `foreach` para quitar elementos hasta que se complete la adición y se vacíe la colección. Esto se denomina una enumeración de mutación o enumeración de consumo porque, a diferencia de un bucle `foreach` típico, este enumerador modifica la colección de origen mediante la eliminación de elementos.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo quitar todos los elementos de `BlockingCollection<T>` usando un bucle de `foreach`. 

```csharp
using System;
using System.Collections.Concurrent;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;

class Example
{
   // Limit the collection size to 2000 items at any given time.
   // Set itemsToProduce to > 500 to hit the limit.
   const int upperLimit = 1000;

   // Adjust this number to see how it impacts the producing-consuming pattern.
   const int itemsToProduce = 100;

   static BlockingCollection<long> collection = new BlockingCollection<long>(upperLimit);

   // Variables for diagnostic output only.
   static Stopwatch sw = new Stopwatch();
   static int totalAdditions = 0;

   // Counter for synchronizing producers.
   static int producersStillRunning = 2;

   static void Main()
   {
       // Start the stopwatch.
       sw.Start();

       // Queue the Producer threads. Store in an array
       // for use with ContinueWhenAll
       Task[] producers = new Task[2];
       producers[0] = Task.Run(() => RunProducer("A", 0));
       producers[1] = Task.Run(() => RunProducer("B", itemsToProduce));

       // Create a cleanup task that will call CompleteAdding after
       // all producers are done adding items.
       Task cleanup = Task.Factory.ContinueWhenAll(producers, (p) => collection.CompleteAdding());

       // Queue the Consumer thread. Put this call
       // before Parallel.Invoke to begin consuming as soon as
       // the producers add items.
       Task.Run(() => RunConsumer());

       // Keep the console window open while the
       // consumer thread completes its output.
       Console.ReadKey(true);
   }

   static void RunProducer(string ID, int start)
   {

       int additions = 0;
       for (int i = start; i < start + itemsToProduce; i++)
       {
           // The data that is added to the collection.
           long ticks = sw.ElapsedTicks;

           // Display additions and subtractions.
           Console.WriteLine("{0} adding tick value {1}. item# {2}", ID, ticks, i);

           if(!collection.IsAddingCompleted)
               collection.Add(ticks);

           // Counter for demonstration purposes only.
           additions++;

           // Uncomment this line to
           // slow down the producer threads     ing.
           Thread.SpinWait(100000);
       }

       Interlocked.Add(ref totalAdditions, additions);
       Console.WriteLine("{0} is done adding: {1} items", ID, additions);
   }

   static void RunConsumer()
   {
       // GetConsumingEnumerable returns the enumerator for the
       // underlying collection.
       int subtractions = 0;
       foreach (var item in collection.GetConsumingEnumerable())
       {
           Console.WriteLine("Consuming tick value {0} : item# {1} : current count = {2}",
                   item.ToString("D18"), subtractions++, collection.Count);
       }

       Console.WriteLine("Total added: {0} Total consumed: {1} Current count: {2} ",
                           totalAdditions, subtractions, collection.Count);
       sw.Stop();

       Console.WriteLine("Press any key to exit");
   }
}

```

Este ejemplo usa un bucle de `foreach` con el método `BlockingCollection<T>.GetConsumingEnumerable` en el subproceso de consumo, lo que provoca que se quite cada elemento de la colección según se enumera. `BlockingCollection<T>` limita el número máximo de elementos que se encuentran en la colección en cualquier momento. Al enumerar la colección de esta forma, bloquea el subproceso consumidor si no hay elementos disponibles o si la colección está vacía. En este ejemplo, el bloqueo no constituye un problema porque el subproceso de productor agrega elementos más rápido de lo que se pueden consumir. 

No hay ninguna garantía de que los elementos se enumeren en el mismo orden en que los agregan los subprocesos de productor.

Para enumerar la colección sin modificación alguna, simplemente use `foreach` sin el método `GetConsumingEnumerable`. Pero es importante comprender que este tipo de enumeración representa una instantánea de la colección en un momento concreto. Si otros subprocesos agregan o quitan elementos mientras se ejecuta el bucle, este no podría representar el estado real de la colección.

## <a name="see-also"></a>Vea también

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[Información general sobre BlockingCollection](blockingcollection-overview.md)

