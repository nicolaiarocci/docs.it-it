---
title: 'Procedura: Usare il ritaglio per definire una regione'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regions [Windows Forms], clipping
- regions [Windows Forms], restricting drawing surface
ms.assetid: 43d121b4-e14c-4901-b25c-2d6c25ba4e29
ms.openlocfilehash: cf60b32df805a49f8da2760332dc32e34209f6dc
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59163735"
---
# <a name="how-to-use-clipping-with-a-region"></a>Procedura: Usare il ritaglio per definire una regione
Una delle proprietà del <xref:System.Drawing.Graphics> classe è l'area di ritaglio. Tutti i disegni effettuati un determinato <xref:System.Drawing.Graphics> è limitato per l'area di ritaglio di tale oggetto <xref:System.Drawing.Graphics> oggetto. È possibile impostare l'area di ritaglio chiamando il <xref:System.Drawing.Graphics.SetClip%2A> (metodo).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente crea un percorso che è costituito da un singolo poligono. Nel codice viene quindi creata un'area, in base a tale percorso. L'area viene passato per il <xref:System.Drawing.Graphics.SetClip%2A> metodo di un <xref:System.Drawing.Graphics> vengono disegnati oggetti e quindi due stringhe.  
  
 La figura seguente mostra le stringhe tagliate.  
  
 ![Clip](./media/clip1.png "clip1")  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.MiscLegacyTopics#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio precedente è progettato per l'uso con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Vedere anche

- [Regioni in GDI+](regions-in-gdi.md)
- [Utilizzo delle regioni](using-regions.md)
