---
title: 'Procedura: Disegnare con pennelli opachi e semitrasparenti'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- semi-transparent shapes [Windows Forms], drawing
- transparency [Windows Forms], semi-transparent shapes
- alpha blending [Windows Forms], brush
- brushes [Windows Forms], using semi-transparent
ms.assetid: a4f6f6b8-3bc8-440a-84af-d62ef0f8ff40
ms.openlocfilehash: a302b8bf978afcead5768fadeb6336c1ece986ec
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59100926"
---
# <a name="how-to-draw-with-opaque-and-semitransparent-brushes"></a>Procedura: Disegnare con pennelli opachi e semitrasparenti
Quando si riempie una forma, è necessario passare un oggetto <xref:System.Drawing.Brush> a uno dei metodi di riempimento della classe <xref:System.Drawing.Graphics>. L'unico parametro del costruttore <xref:System.Drawing.SolidBrush.%23ctor%2A> è un oggetto <xref:System.Drawing.Color>. Per riempire una forma opaca, impostare il componente alfa del colore su 255. Per riempire una forma semitrasparente, impostare il componente alfa su un valore qualsiasi compreso tra 1 e 254.  
  
 Quando si riempie una forma semitrasparente, il colore della forma viene sfumato con i colori dello sfondo. Il componente alfa specifica come si combinano i colori della forma e dello sfondo. I valori alfa vicini a 0 rendono più intensi i colori di sfondo, mentre i valori alfa più vicini a 255 rendono più intenso il colore della forma.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente disegna una bitmap e quindi riempie tre ellissi che si sovrappongono alla bitmap. Per la prima ellisse si usa un componente alfa con un valore pari a 255, quindi l'ellisse risulta opaca. Per la seconda e la terza ellisse si usa un componente alfa con un valore pari a 128, quindi le ellissi risultano semitrasparenti. L'immagine di sfondo è visibile attraverso le ellissi. La chiamata che imposta la proprietà <xref:System.Drawing.Graphics.CompositingQuality%2A> determina la sfumatura della terza ellissi ottenuta in combinazione con la correzione gamma.  

 [!code-csharp[System.Drawing.AlphaBlending#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.AlphaBlending#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#31)]  

 Nella figura seguente mostra l'output del codice seguente: 
  
 ![Figura che mostra l'output opache e semitrasparenti.](./media/how-to-draw-with-opaque-and-semitransparent-brushes/compositingquality-ellipse-semitransparent.png)  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio precedente è progettato per l'uso con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs>`e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Vedere anche

- [Grafica e disegno in Windows Form](graphics-and-drawing-in-windows-forms.md)
- [Linee e riempimenti con fusione alfa](alpha-blending-lines-and-fills.md)
- [Procedura: Assegnare al controllo uno sfondo trasparente](../controls/how-to-give-your-control-a-transparent-background.md)
- [Procedura: Disegnare linee opache e semitrasparenti](how-to-draw-opaque-and-semitransparent-lines.md)
