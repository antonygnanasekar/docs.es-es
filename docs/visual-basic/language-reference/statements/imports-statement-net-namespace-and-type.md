---
title: "Instrucción Imports (tipo y .NET Namespace) | Documentos de Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Imports
- imports
dev_langs:
- VB
helpviewer_keywords:
- declared element names [Visual Basic], qualification
- imports [Visual Basic]
- Imports statement [Visual Basic]
- aliases [Visual Basic], Imports statement
- container elements [Visual Basic]
- namespaces [Visual Basic], importing
- Imports statement [Visual Basic], syntax
- import aliases [Visual Basic]
- aliases [Visual Basic], import
- declared elements [Visual Basic], container elements
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
caps.latest.revision: 40
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 393f3e9a264817d8658585267c954d973290530a
ms.lasthandoff: 03/13/2017

---
# <a name="imports-statement-net-namespace-and-type"></a>Instrucción Imports (Tipo y espacio de nombres de .NET)
Permite escribe los nombres que se haga referencia sin la calificación de espacio de nombres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## <a name="parts"></a>Elementos  
  
|Término|Definición|  
|---|---|  
|`aliasname`|Opcional. Un *alias de importación* o nombre por el que el código puede hacer referencia a `namespace` en lugar de la cadena de calificación completa. Consulte [nombres de elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`namespace`|Obligatorio. El nombre completo del espacio de nombres que se va a importar. Puede ser una cadena de espacios de nombres anidada a cualquier nivel.|  
|`element`|Opcional. El nombre de un elemento de programación declarado en el espacio de nombres. Puede ser cualquier elemento contenedor.|  
  
## <a name="remarks"></a>Comentarios  
 El `Imports` instrucción permite los tipos que se encuentran en un espacio de nombres especificado que se haga referencia directamente.  
  
 Puede proporcionar un único espacio de nombres o una cadena de espacios de nombres anidados. Cada espacio de nombres anidado se separa del siguiente espacio de nombres de nivel superior por un punto (`.`), como se muestra en el ejemplo siguiente.  
  
 `Imports System.Collections.Generic`  
  
 Cada archivo de código fuente puede contener cualquier número de `Imports` instrucciones. Éstas deben seguir las declaraciones de opción, como el `Option Strict` instrucción y se debe preceder a cualquier declaración de elemento de programación como `Module` o `Class` las instrucciones.  
  
 Puede usar `Imports` sólo en el nivel de archivo. Esto significa que el contexto de la declaración de importación debe ser un archivo de origen y no puede ser un espacio de nombres, clase, estructura, módulo, interfaz, procedimiento o bloque.  
  
 Tenga en cuenta que el `Imports` no hace que los elementos de otros proyectos y ensamblados disponibles para su proyecto. Importación no realizará la definición de una referencia. Sólo quita la necesidad de calificar nombres que ya están disponibles para su proyecto. Para obtener más información, vea "Importar elementos contenedores" en [referencias a elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
> [!NOTE]
>  Puede definir implícita `Imports` instrucciones utilizando la [página referencias, Diseñador de proyectos (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic). Para obtener más información, consulte [Cómo: agregar o quitar espacios de nombres importados (Visual Basic)](http://msdn.microsoft.com/library/44cebec3-0ea0-47c2-8406-4edeab6a997e).  
  
## <a name="import-aliases"></a>Alias de importación  
 Un *alias de importación* define el alias para un espacio de nombres o tipo. Alias de importación son útiles cuando necesite utilizar los elementos con el mismo nombre que se declaran en uno o más espacios de nombres. Para obtener más información y un ejemplo, vea "Calificar un nombre de elemento" en [referencias a elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 No se deben declarar un miembro en el nivel de módulo con el mismo nombre que `aliasname`. Si lo hace, el compilador de Visual Basic utiliza `aliasname` sólo para el miembro declarado y ya no lo reconoce como un alias de importación.  
  
 Aunque la sintaxis utilizada para declarar un alias de importación que se utiliza para importar un prefijo de espacio de nombres XML, los resultados son distintos. Un alias de importación puede utilizarse como una expresión en el código, aunque se puede utilizar un prefijo de espacio de nombres XML en literales XML o propiedades de eje XML como el prefijo para un elemento calificado o nombre de atributo.  
  
### <a name="element-names"></a>Nombres de elementos  
 Si proporciona `element`, debe representar un *elemento contenedor*, es decir, un elemento de programación que puede contener otros elementos. Elementos contenedores incluyen clases, estructuras, módulos, interfaces y enumeraciones.  
  
 El ámbito de los elementos disponibles mediante una `Imports` instrucción depende de si se especifica `element`. Si sólo especifica `namespace`, todo de manera exclusiva con el nombre de los miembros de ese espacio de nombres y miembros de elementos contenedores dentro de ese espacio de nombres, están disponibles sin calificación. Si se especifican ambas `namespace` y `element`, sólo los miembros de ese elemento están disponibles sin calificación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve todas las carpetas en el directorio C:\ mediante el uso de la <xref:System.IO.DirectoryInfo>clase.</xref:System.IO.DirectoryInfo>  
  
 El código no tiene ningún `Imports` en la parte superior del archivo. Por lo tanto, la `DirectoryInfo`, <xref:System.Text.StringBuilder>, y <xref:Microsoft.VisualBasic.ControlChars.CrLf>referencias están totalmente calificadas con los espacios de nombres.</xref:Microsoft.VisualBasic.ControlChars.CrLf> </xref:System.Text.StringBuilder>  
  
 [!code-vb[VbVbalrStatements&#152;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_1.vb)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se incluye `Imports` instrucciones para los espacios de nombres que se hace referencia. Por lo tanto, los tipos no deben ser completo con los espacios de nombres.  
  
 [!code-vb[VbVbalrStatements&#153;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_2.vb)]  
  
 [!code-vb[VbVbalrStatements&#154;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_3.vb)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se incluye `Imports` instrucciones que creación alias para los espacios de nombres que se hace referencia. Los tipos se califican con el alias.  
  
 [!code-vb[VbVbalrStatements&#155;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_4.vb)]  
  
 [!code-vb[VbVbalrStatements&#156;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_5.vb)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se incluye `Imports` instrucciones que creación alias para los tipos de referencia. Los alias se utilizan para especificar los tipos.  
  
 [!code-vb[VbVbalrStatements&#157;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_6.vb)]  
  
 [!code-vb[VbVbalrStatements&#158;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_7.vb)]  
  
## <a name="see-also"></a>Vea también  
 [Instrucción Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Espacios de nombres en Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Referencias y la instrucción Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports (instrucción) (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Referencias a elementos declarados](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
