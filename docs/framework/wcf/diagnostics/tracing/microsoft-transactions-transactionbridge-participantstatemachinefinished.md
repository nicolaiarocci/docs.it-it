---
title: Microsoft.Transactions.TransactionBridge.ParticipantStateMachineFinished
ms.date: 03/30/2017
ms.assetid: 54b677f7-03ad-40f2-9c5d-297a8ad9bf90
ms.openlocfilehash: 7f37cb5d9ee3d2d9d56519f785388f278b3333b9
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59170729"
---
# <a name="microsofttransactionstransactionbridgeparticipantstatemachinefinished"></a>Microsoft.Transactions.TransactionBridge.ParticipantStateMachineFinished
La macchina a stati dell'integrazione di un partecipante è passata allo stato di operazione completata.  
  
## <a name="description"></a>Descrizione  
 Traccia eseguita quando l'elaborazione 2PC dell'integrazione di un partecipante subordinato è stata completata. Il risultato dell'integrazione può essere "Committed" o "Aborted", a indicare rispettivamente il commit o l'interruzione di una transazione. Questa traccia viene inoltre eseguita se un partecipante vota "ReadOnly" durante la fase di preparazione.  
  
## <a name="see-also"></a>Vedere anche

- [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)
- [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)
