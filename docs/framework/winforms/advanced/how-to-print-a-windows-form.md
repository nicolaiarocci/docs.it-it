---
title: 'Procedura: Stampare un Windows Form'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, printing
- printing [Windows Forms]
- printing a form
- printing [Windows Forms], printing a form
ms.assetid: c8dff5f8-f56a-4c07-ae31-64643b31f8fc
ms.openlocfilehash: 85fb12028687578b76e0f16061deb9b9a4de70e3
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59121966"
---
# <a name="how-to-print-a-windows-form"></a>Procedura: Stampare un Windows Form
Come parte del processo di sviluppo, è in genere opportuno stampare una copia di Windows Form. Esempio di codice seguente viene illustrato come stampare una copia del modulo corrente usando il <xref:System.Drawing.Graphics.CopyFromScreen%2A> (metodo).  
  
## <a name="example"></a>Esempio  
 [!code-csharp[System.Drawing.Graphics.CopyFromScreen#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Graphics.CopyFromScreen#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Questo è un esempio di codice completo che contiene un `Main` (metodo).  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Non hai le autorizzazioni per accedere alla stampante.  
  
-   Non è installata alcuna stampante.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Per eseguire questo esempio di codice, è necessario disporre dell'autorizzazione per accedere alla stampante utilizzata con il computer.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Drawing.Printing.PrintDocument>
- [Procedura: Eseguire il rendering delle immagini con GDI+](how-to-render-images-with-gdi.md)
- [Procedura: Stampare grafica in Windows Form](how-to-print-graphics-in-windows-forms.md)
