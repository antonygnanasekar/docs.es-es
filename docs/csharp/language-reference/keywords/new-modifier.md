---
title: new (Modificador, Referencia de C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- new modifier keyword [C#]
ms.assetid: a2e20856-33b9-4620-b535-a60dbce8349b
caps.latest.revision: 28
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3c636d50e6c871c529104d5f2985e861f9a652b2
ms.lasthandoff: 03/13/2017

---
# <a name="new-modifier-c-reference"></a>new (Modificador, Referencia de C#)
Cuando se utiliza como modificador de una declaración, la palabra clave `new` oculta explícitamente un miembro heredado de una clase base. Cuando se oculta un miembro heredado, la versión derivada del miembro reemplaza a la versión de la clase base. Aunque los miembros se pueden ocultar sin utilizar el modificador `new`, obtendrá una advertencia del compilador. Si utiliza `new` explícitamente para ocultar un miembro, se suprime esta advertencia.  
  
 Para ocultar un miembro heredado, declárelo en la clase derivada con el mismo nombre de miembro y modifíquelo con la palabra clave `new`. Por ejemplo:  
  
 [!code-cs[csrefKeywordsOperator#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-modifier_1.cs)]  
  
 En este ejemplo, `BaseC.Invoke` oculta `DerivedC.Invoke`. El campo `x` no se ve afectado porque no lo oculta un nombre similar.  
  
 La ocultación de nombres por medio de la herencia toma una de las siguientes formas:  
  
-   Normalmente, una constante, un campo, una propiedad o un tipo que se muestran en una clase o struct ocultan a todos los miembros de la clase base que comparten su nombre.  Hay casos especiales.  Por ejemplo, si declara un nuevo campo con el nombre `N` para tener un tipo que no es invocable y un tipo base declara `N` como método, el nuevo campo no oculta la declaración base en la sintaxis de invocación.  Vea [Especificación del lenguaje C#](http://go.microsoft.com/fwlink/?LinkId=199552) para obtener información detallada (vea la sección "Búsqueda de miembros" en la sección "Expresiones").  
  
-   Un método introducido en una clase o struct oculta las propiedades, los campos y los tipos que comparten el nombre en la clase base. También oculta todos los métodos de la clase base que tienen la misma signatura.  
  
-   Un indizador introducido en una clase o struct oculta todos los indizadores de la clase base que tienen la misma signatura.  
  
 Es un error usar `new` y [override](../../../csharp/language-reference/keywords/override.md) en el mismo miembro, porque los dos modificadores tienen significados mutuamente excluyentes. El modificador `new` crea un nuevo miembro con el mismo nombre y oculta el miembro original. El modificador `override` amplía la implementación de un miembro heredado.  
  
 Si se utiliza el modificador `new` en una declaración que no oculta un miembro heredado, se genera una advertencia.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo, una clase base, `BaseC`, y una clase derivada, `DerivedC`, utilizan el mismo nombre de campo `x`, lo que oculta el valor del campo heredado. El ejemplo muestra el uso del modificador `new`. También muestra cómo obtener acceso a los miembros ocultos de la clase base mediante sus nombres completos.  
  
 [!code-cs[csrefKeywordsOperator#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-modifier_2.cs)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo, una clase anidada oculta una clase que tiene el mismo nombre en la clase base. El ejemplo muestra cómo utilizar el modificador `new` para eliminar el mensaje de advertencia y cómo obtener acceso a los miembros de la clase oculta mediante sus nombres completos.  
  
 [!code-cs[csrefKeywordsOperator#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-modifier_3.cs)]  
  
 Si quita el modificador `new`, el programa seguirá compilándose y ejecutándose, pero aparecerá la siguiente advertencia:  
  
```  
The keyword new is required on 'MyDerivedC.x' because it hides inherited member 'MyBaseC.x'.  
```  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Referencia de C#](../../../csharp/language-reference/index.md)   
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Palabras clave de C#](../../../csharp/language-reference/keywords/index.md)   
 [Palabras clave de operador](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [Modificadores](../../../csharp/language-reference/keywords/modifiers.md)   
 [Control de versiones con las palabras clave Override y New](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)   
 [Saber cuándo utilizar las palabras clave Override y New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)
