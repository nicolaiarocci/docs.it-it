---
title: 'Procedura: Disegnare testo sullo sfondo di un controllo'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], drawing text to backgrounds
- text [WPF], drawing to control backgrounds
- drawing [WPF], text to control backgrounds
- backgrounds [WPF], drawing text to
- typography [WPF], drawing text to control backgrounds
ms.assetid: 686d8fba-f61c-4974-a871-c635d67a7f69
ms.openlocfilehash: 76449c88f9a720741c8ed61255e04a40e6a8613f
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59128453"
---
# <a name="how-to-draw-text-to-a-controls-background"></a>Procedura: Disegnare testo sullo sfondo di un controllo
È possibile disegnare testo direttamente sullo sfondo di un controllo convertendo una stringa di testo a un <xref:System.Windows.Media.FormattedText> dell'oggetto e quindi disegnare l'oggetto per il controllo <xref:System.Windows.Media.DrawingContext>. È anche possibile usare questa tecnica per disegnare sullo sfondo di oggetti derivati da <xref:System.Windows.Controls.Panel>, ad esempio <xref:System.Windows.Controls.Canvas> e <xref:System.Windows.Controls.StackPanel>.  
  
 ![Controlli che visualizzano testo come sfondo](./media/drawtext2background01.png "DrawText2Background01")  
Esempio di controlli con sfondi di testo personalizzati  
  
## <a name="example"></a>Esempio  
 Per disegnare sullo sfondo di un controllo, creare una nuova <xref:System.Windows.Media.DrawingBrush> dell'oggetto e disegnare il testo convertito dell'oggetto <xref:System.Windows.Media.DrawingContext>. Quindi, assegnare al nuovo <xref:System.Windows.Media.DrawingBrush> alla proprietà dello sfondo del controllo.  
  
 Esempio di codice seguente viene illustrato come creare un <xref:System.Windows.Media.FormattedText> dell'oggetto e disegnare lo sfondo di un <xref:System.Windows.Controls.Label> e <xref:System.Windows.Controls.Button> oggetto.  
  
 [!code-csharp[DrawTextToControlBackground#DrawTextToControlBackground1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawTextToControlBackground/CSHARP/Window1.xaml.cs#drawtexttocontrolbackground1)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Media.FormattedText>
- [Disegno di testo formattato](drawing-formatted-text.md)
