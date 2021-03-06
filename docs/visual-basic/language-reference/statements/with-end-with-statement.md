---
title: "With...End With (Instrucci&#243;n, Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.With"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "End (palabra clave), With...End With (instrucciones)"
  - "ejecución, on (objeto)"
  - "instrucciones, repetir"
  - "estructuras de bucle, e instrucciones With...End With"
  - "objetos [Visual Basic], obtener acceso"
  - "With (bloque)"
  - "With (palabra clave)"
  - "With (instrucción)"
  - "With (instrucción), anidar"
  - "With...End With (instrucciones)"
ms.assetid: 340d5fbb-4f43-48ec-a024-80843c137817
caps.latest.revision: 34
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 34
---
# With...End With (Instrucci&#243;n, Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Ejecuta una serie de instrucciones que hacen referencia repetidamente a un único objeto o estructura, por lo que las instrucciones pueden utilizar una sintaxis simplificada al acceder a los miembros del objeto o estructura.  Cuando use una estructura, sola podrá leer los valores de los miembros o invocar métodos, y recibirá un error si intenta asignar valores a los miembros de una estructura utilizada en una instrucción `With...End With`.  
  
## Sintaxis  
  
```  
With objectExpression  
    [ statements ]  
End With  
```  
  
## Elementos  
  
|||  
|-|-|  
|Término|Definición|  
|`objectExpression`|Obligatorio.  Una expresión que se evalúa como un objeto.  La expresión puede ser arbitrariamente compleja y se evalúa solo una vez.  La expresión se puede evaluar como cualquier tipo de datos, incluidos los tipos elementales.|  
|`statements`|Opcional.  Una o varias instrucciones entre `With` y `End With` que pueden hacer referencia a los miembros de un objeto generado por la evaluación de `objectExpression`.|  
|`End With`|Obligatorio.  Termina la definición del bloque `With`.|  
  
## Comentarios  
 Con `With...End With`, puede ejecutar una serie de instrucciones en un objeto especificado sin necesidad especificar el nombre del objeto varias veces.  En un bloque de instrucciones `With`, puede especificar un miembro del objeto que comience por un punto, como si el objeto de la instrucción `With` lo precediera.  
  
 Por ejemplo, para cambiar varias propiedades de un único objeto, coloque las instrucciones de asignación de las propiedades dentro del bloque `With...End With` y haga referencia al objeto una vez, en lugar de hacerlo en cada una de las asignaciones de las propiedades.  
  
 Si el código tiene acceso al mismo objeto en varias instrucciones, la instrucción `With` le brinda las ventajas siguientes:  
  
-   No es necesario evaluar varias veces una expresión compleja ni asignar el resultado a una variable temporal para hacer referencia a sus miembros varias veces.  
  
-   El código resulta más legible al eliminar expresiones de calificación repetitivas.  
  
 El tipo de datos de `objectExpression` puede ser cualquier tipo de clase o estructura, o incluso un tipo elemental de Visual Basic, como `Integer`.  Si `objectExpression` produce un valor que no es un objeto, solo podrá leer los valores de sus miembros o invocar métodos, y recibirá un error si intenta asignar valores a los miembros de una estructura utilizada en una instrucción `With...End With`.  Este es el mismo error que obtendría si invocara un método que devolviera una estructura y accediera inmediatamente a un miembro del resultado de la función, como `GetAPoint().x = 1`, y le asignara un valor.  El problema en ambos casos es que la estructura solo existe en la pila de llamadas y no hay forma de que un miembro de la estructura modificada en estas situaciones pueda escribir en una ubicación de forma que cualquier otro código del programa pueda observar el cambio.  
  
 `objectExpression` se evalúa una vez, tras su entrada en el bloque.  No se puede reasignar `objectExpression` desde el interior del bloque `With`.  
  
 En un bloque `With`, solo de puede acceder a los métodos y propiedades del objeto especificado sin calificarlos.  Se pueden usar métodos y propiedades de otros objetos, pero es necesario calificarlos con los nombres de objeto.  
  
 Puede incluir una instrucción `With...End With` dentro de otra.  Las instrucciones `With...End With` anidadas pueden resultar confusas si los objetos a los que se hace referencia no están claros por el contexto.  Debe proporcionar una referencia completa a un objeto que esté en un bloque `With` externo cuando se haga referencia al objeto desde dentro de un bloque `With` interno.  
  
 No se pueden crear bifurcaciones en un bloque de instrucciones `With` desde fuera del bloque.  
  
 A menos que el bloque contenga un bucle, las instrucciones se ejecutan una sola vez.  Puede anidar diferentes tipos de estructuras de control.  Para obtener más información, vea [Estructuras de control anidadas](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
> [!NOTE]
>  La palabra clave `With` también se puede usar en inicializadores de objeto.  Para obtener más información y ejemplos, vea [Inicializadores de objeto: Tipos con nombre y anónimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md) y [Tipos anónimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
>   
>  Si usa un bloque `With` solo para inicializar las propiedades o campos de un objeto del que acaba de crear instancias, considere la posibilidad de utilizar en su lugar un inicializador de objetos.  
  
## Ejemplo  
 En el ejemplo siguiente, cada bloque `With` ejecuta una serie de instrucciones en un único objeto.  
  
 [!code-vb[VbVbalrWithStatement#2](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/with-end-with-statement_1.vb)]  
  
## Ejemplo  
 En el ejemplo siguiente se anidan las instrucciones `With…End With`.  En la instrucción `With` anidada, la sintaxis hace referencia al objeto interno.  
  
 [!code-vb[VbVbalrWithStatement#1](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/with-end-with-statement_2.vb)]  
  
## Vea también  
 <xref:System.Collections.Generic.List%601>   
 [Estructuras de control anidadas](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Inicializadores de objeto: Tipos con nombre y anónimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Tipos anónimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)