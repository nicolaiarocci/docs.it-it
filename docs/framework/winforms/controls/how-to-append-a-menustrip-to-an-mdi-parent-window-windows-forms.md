---
title: 'Procedura: Aggiungere un MenuStrip a una finestra padre MDI (Windows Form)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- MenuStrip control [Windows Forms], merging
- MenuStrip control [Windows Forms], appending
- MDI [Windows Forms], merging menu items
ms.assetid: ab70c936-b452-4653-b417-17be57bb795b
ms.openlocfilehash: a335531b090983de4e2b3daccc9f956930cbad6e
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59298942"
---
# <a name="how-to-append-a-menustrip-to-an-mdi-parent-window-windows-forms"></a>Procedura: Aggiungere un MenuStrip a una finestra padre MDI (Windows Form)
In alcune applicazioni, il tipo di una finestra figlio di interfaccia a documenti multipli (MDI, Multiple Document Interface) può essere diverso dalla finestra padre MDI. Ad esempio, il padre MDI potrebbe essere un foglio di calcolo, mentre il figlio MDI potrebbe essere un grafico. In tal caso, è consigliabile aggiornare il contenuto del menu del padre MDI con il contenuto del menu del figlio MDI in quanto vengono attivate finestre figlio MDI di tipi diversi.  
  
 La procedura seguente usa la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A>, <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>, <xref:System.Windows.Forms.MergeAction>, e <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> per aggiungere il menu del figlio MDI al menu del padre MDI. Chiudere la finestra figlio MDI rimuove il menu aggiunto dall'elemento padre MDI.  
  
 Vedere anche [le applicazioni di interfaccia a documenti multipli (MDI)](../advanced/multiple-document-interface-mdi-applications.md).  
  
### <a name="to-append-a-menu-item-to-an-mdi-parent"></a>Per aggiungere una voce di menu a un padre MDI  
  
1. Creare un form e impostarne la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true`.  
  
2. Aggiungere <xref:System.Windows.Forms.MenuStrip> a `Form1` e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> di <xref:System.Windows.Forms.MenuStrip> su `true`.  
  
3. Impostare il <xref:System.Windows.Forms.ToolStripItem.Visible%2A> proprietà del `Form1`<xref:System.Windows.Forms.MenuStrip> a `false`.  
  
4. Aggiungere una voce di menu di primo livello per il `Form1`<xref:System.Windows.Forms.MenuStrip> e impostare relativi <xref:System.Windows.Forms.Control.Text%2A> proprietà `&File`.  
  
5. Aggiungere una voce del sottomenu alla voce di menu `&File` e impostare la relativa proprietà <xref:System.Windows.Forms.Form.Text%2A> su `&Open`.  
  
6. Aggiungere un modulo al progetto, aggiungere un <xref:System.Windows.Forms.MenuStrip> al form e impostare il <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> proprietà delle `Form2`<xref:System.Windows.Forms.MenuStrip> a `true`.  
  
7. Aggiungere una voce di menu di primo livello per il `Form2`<xref:System.Windows.Forms.MenuStrip> e impostare relativi <xref:System.Windows.Forms.Form.Text%2A> proprietà `&Special`.  
  
8. Aggiungere due voci di sottomenu alla voce di menu `&Special` e impostare le relative proprietà <xref:System.Windows.Forms.Form.Text%2A> su `Command&1` e `Command&2`, rispettivamente.  
  
9. Impostare la proprietà <xref:System.Windows.Forms.MergeAction> delle voci di menu `&Special`, `Command&1` e `Command&2` su <xref:System.Windows.Forms.MergeAction.Append>.  
  
10. Creare un gestore eventi per il <xref:System.Windows.Forms.Control.Click> eventi del `&New`<xref:System.Windows.Forms.ToolStripMenuItem>.  
  
11. Nel gestore eventi inserire codice simile all'esempio di codice riportato di seguito per creare e visualizzare nuove istanze di `Form2` come finestre figlio MDI di `Form1`.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
    ```  
  
    ```csharp  
    private void openToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
    ```  
  
12. Inserire codice simile al seguente esempio di codice nel `&Open`<xref:System.Windows.Forms.ToolStripMenuItem> per registrare il gestore dell'evento.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles openToolStripMenuItem.Click  
    ```  
  
    ```csharp  
    this.openToolStripMenuItem.Click += new System.EventHandler(this.openToolStripMenuItem_Click);  
    ```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Due controlli <xref:System.Windows.Forms.Form> denominati `Form1` e `Form2`.  
  
-   Un controllo <xref:System.Windows.Forms.MenuStrip> su `Form1` denominato `menuStrip1` e un controllo <xref:System.Windows.Forms.MenuStrip> su `Form2` denominato `menuStrip2`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=nameWithType> e <xref:System.Windows.Forms?displayProperty=nameWithType>.
