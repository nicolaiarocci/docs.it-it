---
title: "Procedura: Registrare messaggi all'avvio o all'arresto dell'applicazione (Visual Basic)"
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, shutdown
- My.Application.Log object, logging
- Startup event [Visual Basic]
- event logs, startup
- Shutdown event [Visual Basic]
- My.Log object, logging
ms.assetid: 67624d05-cddf-48b7-8c36-5c99baa4c621
ms.openlocfilehash: 8fc7b441c6e19d70ceefa3422cf9823007280b64
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59330571"
---
# <a name="how-to-log-messages-when-the-application-starts-or-shuts-down-visual-basic"></a>Procedura: Registrare messaggi all'avvio o all'arresto dell'applicazione (Visual Basic)
È possibile usare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione. Questo esempio illustra come usare il metodo `My.Application.Log.WriteEntry` con gli eventi `Startup` e `Shutdown` per scrivere informazioni di traccia.  
  
### <a name="to-access-the-applications-event-handler-code"></a>Per accedere al codice del gestore eventi dell'applicazione  
  
1. Selezionare un progetto in **Esplora soluzioni**. Scegliere **Proprietà** dal menu **Progetto**.  
  
2. Fare clic sulla scheda **Applicazione** .  
  
3. Fare clic sul pulsante **Visualizza eventi applicazione** per aprire l'editor di codice.  
  
     Verrà aperto il file ApplicationEvents.vb.  
  
### <a name="to-log-messages-when-the-application-starts"></a>Per registrare messaggi all'avvio dell'applicazione  
  
1. Aprire il file ApplicationEvents.vb nell'editor di codice. Scegliere **Eventi MyApplication** dal menu **Generale**.  
  
2. Scegliere **Avvio** dal menu **Dichiarazioni**.  
  
     L'applicazione genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> prima dell'esecuzione dell'applicazione principale.  
  
3. Aggiungere il metodo `My.Application.Log.WriteEntry` al gestore eventi `Startup` .  
  
     [!code-vb[VbVbalrMyApplicationLog#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#1)]  
  
### <a name="to-log-messages-when-the-application-shuts-down"></a>Per registrare messaggi all'arresto dell'applicazione  
  
1. Aprire il file ApplicationEvents.vb nell'editor di codice. Scegliere **Eventi MyApplication** dal menu **Generale**.  
  
2. Scegliere **Arresto** dal menu **Dichiarazioni**.  
  
     L'applicazione genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> dopo l'esecuzione dell'applicazione principale, ma prima dell'arresto.  
  
3. Aggiungere il metodo `My.Application.Log.WriteEntry` al gestore eventi `Shutdown` .  
  
     [!code-vb[VbVbalrMyApplicationLog#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#2)]  
  
## <a name="example"></a>Esempio  
 Per accedere agli eventi dell'applicazione nell'editor del codice è possibile usare **Creazione progetti** . Per altre informazioni, vedere [Pagina Applicazione, Creazione progetti (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
 [!code-vb[VbVbalrMyApplicationLog#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#3)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [Application Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
