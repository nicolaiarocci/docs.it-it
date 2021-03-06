---
title: 'Procedura: Creare una sfumatura lineare'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- linear gradients [Windows Forms], creating
- gradients [Windows Forms], creating linear
- colors [Windows Forms], creating linear gradients
- gradients
ms.assetid: 6c88e1cc-1217-4399-ac12-cb37592b9f01
ms.openlocfilehash: 540b6d422be5d5c0898f019592a755258145d14d
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59125021"
---
# <a name="how-to-create-a-linear-gradient"></a>Procedura: Creare una sfumatura lineare
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] fornisce orizzontali, verticali e diagonali sfumature lineari. Per impostazione predefinita, il colore in una sfumatura lineare viene modificato in modo uniforme. Tuttavia, è possibile personalizzare una sfumatura lineare in modo che il colore viene modificato in modo non uniforme.  
  
 Nell'esempio seguente inserisce una riga, un'ellisse e un rettangolo con un pennello sfumatura lineare orizzontale.  
  
 Il <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> costruttore riceve quattro argomenti: due punti e due colori. Il primo punto (0, 10) è associato il primo colore (rosso) e il secondo punto (200, 10) è associato il secondo colore (blu). Come si può immaginare, la riga disegnata dal punto (0, 10) a (200, 10) cambia gradualmente da rosso a blu.  
  
 Il numero 10 in quanto (50, 10) e (200, 10) non sono importanti. È importante che i due punti abbiano la stessa coordinata secondo, ovvero la linea di connessione è orizzontale. I puntini di sospensione e il rettangolo inoltre modificare gradualmente da rosso a blu come la coordinata orizzontale va da 0 a 200.  
  
 La figura seguente mostra la riga, i puntini di sospensione e il rettangolo. Si noti che la sfumatura di colore viene ripetuto man mano che aumenta la coordinata orizzontale a oltre 200.  
  
 ![Sfumatura lineare](./media/cslineargradient1.png "cslineargradient1")  
  
### <a name="to-use-horizontal-linear-gradients"></a>Per utilizzare sfumature lineari orizzontali  
  
-   Passare blu rosso ed è opaco opaco come il terzo e quarto argomento, rispettivamente.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#21)]
     [!code-vb[System.Drawing.UsingaGradientBrush#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#21)]  
  
 Nell'esempio precedente, i componenti di colore modificare in modo lineare come si spostano da una coordinata orizzontale pari a 0 a una coordinata orizzontale pari a 200. Ad esempio, un punto di cui prima coordinata è compreso tra 0 e 200 avrà un componente blu che è compreso tra 0 e 255.  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] Consente di regolare la modalità di che un colore varia da un bordo di una sfumatura a altro. Si supponga di che voler creare un pennello a sfumatura che le modifiche apportate dal nero al rosso in base alla tabella riportata di seguito.  
  
|Coordinata orizzontale|Componenti RGB|  
|---------------------------|--------------------|  
|0|(0, 0, 0)|  
|40|(128, 0, 0)|  
|200|(255, 0, 0)|  
  
 Si noti che il componente rossa intensità media quando la coordinata orizzontale corrisponde solo il 20% del modo in cui da 0 a 200.  
  
 L'esempio seguente imposta la <xref:System.Drawing.Drawing2D.LinearGradientBrush.Blend%2A> proprietà di un <xref:System.Drawing.Drawing2D.LinearGradientBrush> oggetto da associare tre intensità relative tre posizioni relative. Come indicato nella tabella precedente, è associata a una posizione relativa di 0.2 un'intensità di 0,5. Il codice viene compilato un rettangolo con il pennello a sfumatura e un'ellisse.  
  
 La figura seguente mostra l'ellisse risultante e il rettangolo.  
  
 ![Sfumatura lineare](./media/cslineargradient2.png "cslineargradient2")  
  
### <a name="to-customize-linear-gradients"></a>Per personalizzare le sfumature lineari  
  
-   Passare il rosso opaco e nero opaco come il terzo e quarto argomento, rispettivamente.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#22)]
     [!code-vb[System.Drawing.UsingaGradientBrush#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#22)]  
  
 Le sfumature negli esempi precedenti sono state orizzontale; vale a dire il colore cambia gradualmente quando si sposta lungo una linea orizzontale. È anche possibile definire le sfumature verticali e diagonali.  
  
 L'esempio seguente passa i punti (0, 0) e (200, 100) per un <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> costruttore. È associato il colore blu (0, 0), ed è associato il colore verde (200, 100). Una riga (con la larghezza della penna 10) e un elemento ellipse vengono riempiti con il pennello sfumato lineare.  
  
 La figura seguente mostra la riga e l'ellisse. Si noti che il colore in ellisse cambia gradualmente quando si sposta lungo una riga che sono parallelo a quella che passa attraverso (0, 0) e (200, 100).  
  
 ![Sfumatura lineare](./media/cslineargradient3.png "cslineargradient3")  
  
### <a name="to-create-diagonal-linear-gradients"></a>Per creare diagonale sfumature lineari  
  
-   Passare l'opaco blu e verde opaco come il terzo e quarto argomento, rispettivamente.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#23)]
     [!code-vb[System.Drawing.UsingaGradientBrush#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#23)]  
  
## <a name="see-also"></a>Vedere anche

- [Utilizzo di un pennello a sfumatura per il riempimento di forme](using-a-gradient-brush-to-fill-shapes.md)
- [Grafica e disegno in Windows Form](graphics-and-drawing-in-windows-forms.md)
