---
title: "Cómo: crear literales XML (Visual Basic) | Documentos de Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- XML literals [Visual Basic], creating
ms.assetid: 573a6db5-b14d-4e42-b356-8cc7e2d77745
caps.latest.revision: 17
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
ms.openlocfilehash: 72d96f36fc17f32ac3ee3ea97175f112fcd21681
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-xml-literals-visual-basic"></a>Cómo: Crear literales XML (Visual Basic)
Puede crear un documento, fragmento o elemento XML directamente en el código mediante un literal XML. Los ejemplos de este tema muestran cómo crear un elemento XML que tiene tres elementos secundarios y cómo crear un documento XML.  
  
 También puede utilizar el [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] API para crear [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] objetos. Para obtener más información, consulte <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>  
  
### <a name="to-create-an-xml-element"></a>Para crear un elemento XML  
  
-   Crear el XML en línea mediante la sintaxis de literales XML, que es el mismo que la sintaxis XML.  
  
     [!code-vb[VbXMLSamples&#5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-xml-literals_1.vb)]  
  
     Ejecute el código. El resultado de este código es:  
  
     `<contact>`  
  
     `<name>Patrick Hines</name>`  
  
     `<phone type="home">206-555-0144</phone>`  
  
     `<phone type="work">425-555-0145</phone>`  
  
     `</contact>`  
  
### <a name="to-create-an-xml-document"></a>Para crear un documento XML  
  
-   Crear el documento XML en línea. El código siguiente crea un documento XML que tiene sintaxis de literales, una declaración XML, una instrucción de procesamiento, un comentario y un elemento que contiene otro elemento.  
  
     [!code-vb[VbXMLSamples Nº&30;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-xml-literals_2.vb)]  
  
     Ejecute el código. El resultado de este código es:  
  
     `<?xml-stylesheet type="text/xsl" href="show_book.xsl"?>`  
  
     `<!-- Tests that the application works. -->`  
  
     `<books>`  
  
     `<book/>`  
  
     `</books>`  
  
## <a name="see-also"></a>Vea también  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Crear XML en Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Literal de elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Literal de documento XML](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)
