---
title: Supporto di tipi di dati nelle classi System.Xml
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 63570538-06e3-4401-ad4d-ac50be90c7bf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bb47eec7153624b1822b6393bb4a1621b1cd63db
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2018
ms.locfileid: "33569694"
---
# <a name="type-support-in-the-systemxml-classes"></a>Supporto di tipi di dati nelle classi System.Xml
In .NET Framework versione 2.0 le classi principali XML sono state migliorate per includere funzionalità di supporto dei tipi di dati. Le classi <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> e <xref:System.Xml.XPath.XPathNavigator> includono funzionalità di supporto dei tipi che comprendono la capacità di conversione tra tipi XML Schema e tipi CLR (Common Language Runtime).  
  
 In .NET Framework versione 2.0 le classi <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> e <xref:System.Xml.XPath.XPathNavigator> sono state migliorate per includere funzionalità di supporto dei tipi di dati.  
  
-   Le classi <xref:System.Xml.XmlReader> e <xref:System.Xml.XPath.XPathNavigator> includono ciascuna una proprietà **SchemaInfo** che consente di restituire le informazioni sullo schema in un nodo.  
  
-   Le proprietà **ReadContentAs** e **ReadElementContentAs** nella classe <xref:System.Xml.XmlReader> leggono un valore di testo e lo convertono in un valore CLR con una singola chiamata al metodo.  
  
-   Il metodo <xref:System.Xml.XmlWriter.WriteValue%2A> nella classe <xref:System.Xml.XmlWriter> converte un tipo CLR in un tipo XML Schema durante la scrittura XML.  
  
-   Le proprietà **ValueAs** e <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> nella classe <xref:System.Xml.XPath.XPathNavigator> restituiscono un valore di nodo e lo convertono in un valore CLR con una singola chiamata al metodo.  
  
> [!NOTE]
>  In .NET Framework versione 1.0 era necessario convertire la classe <xref:System.Xml.XmlConvert> tra il tipo XML Schema e il tipo CLR.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Mapping dei tipi di dati XML a tipi di dati CLR](../../../../docs/standard/data/xml/mapping-xml-data-types-to-clr-types.md)  
 Vengono descritti i mapping predefiniti dei tipi di dati XML ai tipi di dati CLR.  
  
 [Note sull'implementazione del supporto per il tipo XML](../../../../docs/standard/data/xml/xml-type-support-implementation-notes.md)  
 Vengono illustrati alcuni dettagli relativi all'implementazione del supporto per i tipi di dati.  
  
 [Conversione dei tipi di dati XML](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)  
 Viene descritto come usare la classe <xref:System.Xml.XmlConvert> per eseguire la conversione tra tipi XML Schema e tipi CLR.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Accesso a dati XML fortemente tipizzati con XPathNavigator](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
