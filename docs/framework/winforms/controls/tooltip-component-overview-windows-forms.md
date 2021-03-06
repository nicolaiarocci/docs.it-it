---
title: Cenni preliminari sul componente ToolTip (Windows Form)
ms.date: 03/30/2017
f1_keywords:
- ToolTip
helpviewer_keywords:
- tooltips [Windows Forms], about tooltips
- ToolTip component [Windows Forms], about ToolTip component
ms.assetid: 3fbc6f08-c882-4acd-a960-a08efe3c7e6e
ms.openlocfilehash: 3fbe883501d1ce36ca25ea07631f98042f451e07
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59197308"
---
# <a name="tooltip-component-overview-windows-forms"></a>Cenni preliminari sul componente ToolTip (Windows Form)
Il componente <xref:System.Windows.Forms.ToolTip> di Windows Form visualizza un testo quando l'utente posiziona il puntatore sui controlli. Una descrizione comando può essere associata a qualsiasi controllo. Un esempio di uso di questo componente: per risparmiare spazio in un form, è possibile visualizzare una piccola icona su un pulsante e usando una descrizione comando per illustrare la funzione del pulsante.  
  
## <a name="working-with-the-tooltip-component"></a>Utilizzo del componente ToolTip  
 Oggetto <xref:System.Windows.Forms.ToolTip> componente fornisce un `ToolTip` proprietà per più controlli in un modulo di Windows o un altro contenitore. Ad esempio, se si inserisce uno <xref:System.Windows.Forms.ToolTip> componente in un form, è possibile visualizzare "Digitare qui il nome" per un <xref:System.Windows.Forms.TextBox> controllano e "Fare clic qui per salvare le modifiche" per un <xref:System.Windows.Forms.Button> controllo.  
  
 I metodi principali dei <xref:System.Windows.Forms.ToolTip> componente vengono <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> e <xref:System.Windows.Forms.ToolTip.GetToolTip%2A>. È possibile usare il <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> metodo per impostare le descrizioni comandi visualizzate per i controlli. Per altre informazioni, vedere [Procedura: Impostare le descrizioni comandi per i controlli in un Windows Form in fase di progettazione](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md). Le proprietà della chiave sono <xref:System.Windows.Forms.ToolTip.Active%2A>, che deve essere impostata su `true` per la descrizione comando da visualizzare, e <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>, che imposta il periodo di tempo che viene visualizzata la stringa di descrizione comando, quanto tempo l'utente deve fare riferimento al controllo per la descrizione comando da visualizzare e come tempo necessario per le successive finestre della descrizione comando da visualizzare. Per altre informazioni, vedere [Procedura: Modifica del ritardo del componente di Windows Form della descrizione comando](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md).  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.ToolTip>
- [Procedura: Impostare le descrizioni comando per i controlli in un Windows Form in fase di progettazione](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)
- [Procedura: Modificare il ritardo del componente ToolTip di Windows Forms](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
