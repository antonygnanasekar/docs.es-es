---
title: "Nothing y cadenas en Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "cadenas [Visual Basic], Nothing"
ms.assetid: 261380af-2024-4ecf-823b-43b1034d92cd
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Nothing y cadenas en Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

El runtime de [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] y el runtime de [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] evalúan `Nothing` de manera diferente cuando afecta a las cadenas.  
  
## Visual Basic Runtime y .NET Framework  
 Considere el ejemplo siguiente:  
  
 [!code-vb[VbVbalrStrings#47](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/nothing-and-strings_1.vb)]  
  
 El runtime de [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] normalmente evalúa `Nothing` como una cadena vacía \(""\).  Sin embargo, [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] no lo hace, y se producirá una excepción cuando se intente realizar una operación de cadena en `Nothing`.  
  
## Vea también  
 [Introducción a las cadenas en Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)