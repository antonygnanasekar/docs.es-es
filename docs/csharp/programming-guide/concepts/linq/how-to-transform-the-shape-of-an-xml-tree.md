---
title: "Cómo: Transformar la forma de un árbol XML (C#) | Microsoft Docs"
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
ms.assetid: 93c5d426-dea2-4709-a991-60204de42e8f
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8f11c77bc6273642bc4ffce3bf546c5a897729bc
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-transform-the-shape-of-an-xml-tree-c"></a>Cómo: Transformar la forma de un árbol XML (C#)
La *forma* de un documento XML hace referencia a sus nombres de elemento, sus nombres de atributo y las características de su jerarquía.  
  
 A veces, deberá cambiar la forma de un elemento XML. Por ejemplo, es posible que deba enviar un documento XML a otro sistema que requiere nombres de elemento y atributo diferentes. Podría revisar el documento y eliminar y cambiar el nombre de los elementos necesarios, pero el uso de la construcción funcional proporciona un código más legible y fácil de mantener. Para obtener más información sobre la construcción funcional, consulte [Functional Construction (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/functional-construction-linq-to-xml.md) (Construcción funcional [LINQ to XML] [C#]).  
  
 El primer ejemplo cambia la organización del documento XML. Mueve los elementos complejos de una ubicación del árbol a otra.  
  
 El segundo ejemplo de este tema crea un documento XML con una forma diferente a la del documento de origen. Cambia el uso de mayúsculas y minúsculas de los nombres de elemento, cambia el nombre de algunos elementos y deja algunos de los elementos del árbol de origen fuera del árbol transformado.  
  
## <a name="example"></a>Ejemplo  
 El código siguiente cambia la forma de un archivo XML con las expresiones de consulta incrustadas.  
  
 El documento XML de origen de este ejemplo contiene un elemento `Customers` en el elemento `Root` que contiene todos los clientes. También contiene un elemento `Orders` en el elemento `Root` que contiene todos los pedidos. Este ejemplo crea un nuevo árbol XML en el que los pedidos de cada cliente se incluyen en un elemento `Orders` dentro del elemento `Customer`. El documento original también contiene un elemento `CustomerID` en el elemento `Order`; este elemento se quitará del documento con la forma cambiada.  
  
 En este ejemplo se usa el siguiente documento XML: [Archivo XML de muestra: clientes y pedidos (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
```csharp  
XElement co = XElement.Load("CustomersOrders.xml");  
XElement newCustOrd =  
    new XElement("Root",  
        from cust in co.Element("Customers").Elements("Customer")  
        select new XElement("Customer",  
            cust.Attributes(),  
            cust.Elements(),  
            new XElement("Orders",  
                from ord in co.Element("Orders").Elements("Order")  
                where (string)ord.Element("CustomerID") == (string)cust.Attribute("CustomerID")  
                select new XElement("Order",  
                    ord.Attributes(),  
                    ord.Element("EmployeeID"),  
                    ord.Element("OrderDate"),  
                    ord.Element("RequiredDate"),  
                    ord.Element("ShipInfo")  
                )  
            )  
        )  
    );  
Console.WriteLine(newCustOrd);  
```  
  
 Este código genera el siguiente resultado:  
  
```xml  
<Root>  
  <Customer CustomerID="GREAL">  
    <CompanyName>Great Lakes Food Market</CompanyName>  
    <ContactName>Howard Snyder</ContactName>  
    <ContactTitle>Marketing Manager</ContactTitle>  
    <Phone>(503) 555-7555</Phone>  
    <FullAddress>  
      <Address>2732 Baker Blvd.</Address>  
      <City>Eugene</City>  
      <Region>OR</Region>  
      <PostalCode>97403</PostalCode>  
      <Country>USA</Country>  
    </FullAddress>  
    <Orders />  
  </Customer>  
  <Customer CustomerID="HUNGC">  
    <CompanyName>Hungry Coyote Import Store</CompanyName>  
    <ContactName>Yoshi Latimer</ContactName>  
    <ContactTitle>Sales Representative</ContactTitle>  
    <Phone>(503) 555-6874</Phone>  
    <Fax>(503) 555-2376</Fax>  
    <FullAddress>  
      <Address>City Center Plaza 516 Main St.</Address>  
      <City>Elgin</City>  
      <Region>OR</Region>  
      <PostalCode>97827</PostalCode>  
      <Country>USA</Country>  
    </FullAddress>  
    <Orders />  
  </Customer>  
  . . .  
```  
  
## <a name="example"></a>Ejemplo  
 Este ejemplo cambia el nombre de algunos elementos y convierte algunos atributos en elementos.  
  
 El código llama a `ConvertAddress`, que devuelve una lista de objetos <xref:System.Xml.Linq.XElement>. El argumento del método es una consulta que determina el elemento complejo `Address` en el que el atributo `Type` tiene un valor `"Shipping"`.  
  
 En este ejemplo se usa el siguiente documento XML: [Sample XML File: Typical Purchase Order (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml-1.md) (Archivo XML de ejemplo: pedido de compra común [LINQ to XML]).  
  
```csharp  
static IEnumerable<XElement> ConvertAddress(XElement add)  
{  
    List<XElement> fragment = new List<XElement>() {  
        new XElement("NAME", (string)add.Element("Name")),  
        new XElement("STREET", (string)add.Element("Street")),  
        new XElement("CITY", (string)add.Element("City")),  
        new XElement("ST", (string)add.Element("State")),  
        new XElement("POSTALCODE", (string)add.Element("Zip")),  
        new XElement("COUNTRY", (string)add.Element("Country"))  
    };  
    return fragment;  
}  
  
static void Main(string[] args)  
{  
    XElement po = XElement.Load("PurchaseOrder.xml");  
    XElement newPo = new XElement("PO",  
        new XElement("ID", (string)po.Attribute("PurchaseOrderNumber")),  
        new XElement("DATE", (DateTime)po.Attribute("OrderDate")),  
        ConvertAddress(  
            (from el in po.Elements("Address")  
            where (string)el.Attribute("Type") == "Shipping"  
            select el)  
            .First()  
        )  
    );  
    Console.WriteLine(newPo);  
}  
```  
  
 Este código genera el siguiente resultado:  
  
```xml  
<PO>  
  <ID>99503</ID>  
  <DATE>1999-10-20T00:00:00</DATE>  
  <NAME>Ellen Adams</NAME>  
  <STREET>123 Maple Street</STREET>  
  <CITY>Mill Valley</CITY>  
  <ST>CA</ST>  
  <POSTALCODE>10999</POSTALCODE>  
  <COUNTRY>USA</COUNTRY>  
</PO>  
```  
  
## <a name="see-also"></a>Vea también  
 [Proyecciones y transformaciones (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
