---
title: 'Procedura: Recuperare una raccolta di elementi (LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 2269f9de-8fb9-4666-b8a1-a4e754fa6a81
ms.openlocfilehash: 53572ac3c80e012b95527d32da28c8685cd8cfd3
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58833635"
---
# <a name="how-to-retrieve-a-collection-of-elements-linq-to-xml-visual-basic"></a>Procedura: Recuperare una raccolta di elementi (LINQ to XML) (Visual Basic)
In questo argomento viene illustrato il metodo <xref:System.Xml.Linq.XContainer.Elements%2A>, che consente di recuperare una raccolta degli elementi figlio di un elemento.  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono scorsi gli elementi figlio dell'elemento `purchaseOrder`.  
  
 Nell'esempio viene usato il documento XML seguente: [File XML di esempio: tipico ordine di acquisto (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md).  
  
```vb  
Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
Dim childElements As IEnumerable(Of XElement)  
childElements = _  
    From el In po.Elements() _  
    Select el  
For Each el As XElement In childElements  
    Console.WriteLine("Name: " & el.Name.ToString())  
Next  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Name: Address  
Name: Address  
Name: DeliveryNotes  
Name: Items  
```  
  
## <a name="see-also"></a>Vedere anche

- [Assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
