---
title: 'Procedura: Disegnare una forma con contorno'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- Graphics.DrawEllipse
helpviewer_keywords:
- ellipses [Windows Forms], drawing
- circles [Windows Forms], drawing
- drawing [Windows Forms], shapes
- circular shapes
- forms [Windows Forms], drawing circular shapes
- circles
- outlined shapes [Windows Forms], examples
- outlined shapes [Windows Forms], drawing
- drawing [Windows Forms], circular shapes
- shapes [Windows Forms], drawing
ms.assetid: f4f9214c-607e-407d-8cdd-6549f0278451
ms.openlocfilehash: 019bbc19cc4b26c42f8539eccd93ec4ff87fab12
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59192205"
---
# <a name="how-to-draw-an-outlined-shape"></a>Procedura: Disegnare una forma con contorno
In questo esempio disegna ellissi e rettangoli in un form.  
  
## <a name="example"></a>Esempio  
 [!code-cpp[System.Drawing.ConceptualHowTos#6](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#6)]
 [!code-csharp[System.Drawing.ConceptualHowTos#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#6)]
 [!code-vb[System.Drawing.ConceptualHowTos#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#6)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 È possibile chiamare questo metodo nel <xref:System.Windows.Forms.Form.Load> gestore dell'evento. Il contenuto creato non verrà ridisegnato se il form viene ridimensionato o nascosto da un altro form. Per rendere il contenuto viene ridisegnata automaticamente, è necessario eseguire l'override di <xref:System.Windows.Forms.Control.OnPaint%2A> (metodo).  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 È sempre necessario chiamare <xref:System.IDisposable.Dispose%2A> tutti gli oggetti che utilizzano le risorse di sistema, ad esempio <xref:System.Drawing.Pen> e <xref:System.Drawing.Graphics> oggetti.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Drawing.Graphics.DrawEllipse%2A>
- <xref:System.Windows.Forms.Control.OnPaint%2A>
- <xref:System.Drawing.Graphics.DrawRectangle%2A>
- [Guida introduttiva alla programmazione grafica](getting-started-with-graphics-programming.md)
- [Utilizzo di un oggetto Pen per creare linee e forme](using-a-pen-to-draw-lines-and-shapes.md)
- [Grafica e disegno in Windows Form](graphics-and-drawing-in-windows-forms.md)
