---
title: "Cómo: Recuperar un único atributo (LINQ to XML) (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 1b6b07b9-933f-47e9-874e-e790cab49dc5
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c48c8e96996a1e6eb5d44f847058b401cc91c277
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml-c"></a>Cómo: Recuperar un único atributo (LINQ to XML) (C#)
Este tema explica cómo recuperar un atributo concreto de un elemento, proporcionando el nombre del atributo. Esto puede resultar útil para escribir expresiones de consulta mediante las cuales encontrar un elemento que contiene un atributo en particular.  
  
 El método <xref:System.Xml.Linq.XElement.Attribute%2A>de la clase <xref:System.Xml.Linq.XElement> devuelve el <xref:System.Xml.Linq.XAttribute> con el nombre especificado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el método <xref:System.Xml.Linq.XElement.Attribute%2A>.  
  
```csharp  
XElement cust = new XElement("PhoneNumbers",  
    new XElement("Phone",  
        new XAttribute("type", "home"),  
        "555-555-5555"),  
    new XElement("Phone",  
        new XAttribute("type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =  
    from el in cust.Descendants("Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute("type"));  
```  
  
 Este ejemplo encuentra todos los descendientes en el árbol cuyo nombre es `Phone` y, a continuación, encuentra aquel atributo cuyo nombre es `type`.  
  
 Este código genera el siguiente resultado:  
  
```  
home  
work  
```  
  
## <a name="example"></a>Ejemplo  
 Si quiere recuperar el valor del atributo, puede convertirlo, de la misma forma que lo haría con los objetos <xref:System.Xml.Linq.XElement>. En el siguiente ejemplo se muestra cómo hacerlo.  
  
```csharp  
XElement cust = new XElement("PhoneNumbers",  
    new XElement("Phone",  
        new XAttribute("type", "home"),  
        "555-555-5555"),  
    new XElement("Phone",  
        new XAttribute("type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =   
    from el in cust.Descendants("Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute("type"));  
```  
  
 Este código genera el siguiente resultado:  
  
```  
home  
work  
```  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] proporciona operadores de conversión explícitos para la clase <xref:System.Xml.Linq.XAttribute> para `string`, `bool`, `bool?`, `int`, `int?`, `uint`, `uint?`, `long`, `long?`, `ulong`, `ulong?`, `float`, `float?`, `double`, `double?`, `decimal`, `decimal?`, `DateTime`, `DateTime?`, `TimeSpan`, `TimeSpan?`, `GUID` y `GUID?`.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra el mismo código para un atributo que se encuentre en un espacio de nombres. Para obtener más información, vea [Working with XML Namespaces (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md) (Trabajar con espacios de nombres XML [C#]).  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement cust = new XElement(aw + "PhoneNumbers",  
    new XElement(aw + "Phone",  
        new XAttribute(aw + "type", "home"),  
        "555-555-5555"),  
    new XElement(aw + "Phone",  
        new XAttribute(aw + "type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =  
    from el in cust.Descendants(aw + "Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute(aw + "type"));  
```  
  
 Este código genera el siguiente resultado:  
  
```  
home  
work  
```  
  
## <a name="see-also"></a>Vea también  
 [LINQ to XML Axes (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md) (Ejes de LINQ to XML [C#])
