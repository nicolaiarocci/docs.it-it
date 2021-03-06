---
title: 'Procedura: Usare la classe SystemParameters'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- classes [WPF], SystemParameters
ms.assetid: 02e7a5de-94eb-4953-b91c-52e6c872ad5b
ms.openlocfilehash: 344fb54b48bcbf188b36a29d8205c21deff713c4
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59199856"
---
# <a name="how-to-use-systemparameters"></a>Procedura: Usare la classe SystemParameters
Questo esempio viene illustrato come accedere e usare le proprietà di <xref:System.Windows.SystemParameters> per applicare uno stile a un pulsante o personalizzarlo.  
  
## <a name="example"></a>Esempio  
 Le risorse di sistema espongono diverse impostazioni basate sul sistema come risorse per consentire la creazione di oggetti visivi coerenti con le impostazioni del sistema. <xref:System.Windows.SystemParameters> è una classe contenente proprietà valore parametro di sistema e le chiavi di risorsa associate ai valori. Ad esempio, <xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> è un <xref:System.Windows.SystemParameters> il valore di proprietà e <xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A> è la chiave di risorsa corrispondente.  
  
 Nelle [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile usare i membri di <xref:System.Windows.SystemParameters> come utilizzo di una proprietà statica o di riferimenti di risorse dinamiche (con il valore della proprietà statica come chiave). Usare un riferimento alla risorsa dinamica per aggiornare automaticamente il valore basato sul sistema durante l'esecuzione dell'applicazione; in caso contrario, usare un riferimento statico. Le chiavi di risorsa hanno il suffisso `Key` accodato al nome della proprietà.  
  
 Nell'esempio seguente viene illustrato come accedere e usare i valori statici di <xref:System.Windows.SystemParameters> per applicare uno stile a un pulsante o personalizzarlo. Questo esempio di markup viene ridimensionato un pulsante applicando <xref:System.Windows.SystemParameters> valori a un pulsante.  
  
 [!code-xaml[SystemRes_snip#ParameterStaticResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#parameterstaticresources)]  
  
 Per usare i valori di <xref:System.Windows.SystemParameters> nel codice, non è necessario usare riferimenti statici o riferimenti a risorse dinamiche. Usare invece i valori del <xref:System.Windows.SystemParameters> classe. Anche se le proprietà non chiave sono apparentemente definite come proprietà statiche, il comportamento di runtime [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato dal sistema verranno rivaluterà le proprietà in tempo reale e risponderà correttamente eseguita dall'utente. le modifiche ai valori di sistema. Nell'esempio seguente viene illustrato come impostare la larghezza e altezza di un pulsante usando <xref:System.Windows.SystemParameters> valori.  
  
 [!code-csharp[SystemRes_snip#ParameterResourcesCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#parameterresourcescode)]
 [!code-vb[SystemRes_snip#ParameterResourcesCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#parameterresourcescode)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.SystemParameters>
- [Disegnare un'area con un pennello di sistema](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [Usare la classe SystemFonts](how-to-use-systemfonts.md)
- [Usare le chiavi dei parametri di sistema](how-to-use-system-parameters-keys.md)
- [Procedure relative](resources-how-to-topics.md)
