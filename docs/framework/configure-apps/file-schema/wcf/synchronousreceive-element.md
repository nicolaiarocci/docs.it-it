---
title: <synchronousReceive> elemento
ms.date: 03/30/2017
ms.assetid: cc070387-3d11-4b02-a952-bc08ad2df05a
ms.openlocfilehash: 20390f747c8beaccba1cfea7a9ea0ed366037ecb
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59166543"
---
# <a name="synchronousreceive-element"></a>\<synchronousReceive > elemento
Questo elemento di configurazione viene usato per specificare il comportamento in fase di esecuzione per la ricezione di messaggi in un servizio o in un'applicazione client. Non prevede attributi o elementi figlio.  
  
 \<system.ServiceModel>  
\<behaviors>  
\<endpointBehaviors>  
\<behavior>  
\<synchronousReceive>  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<synchronousReceive />
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
 Nessuno.  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[\<behavior>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un comportamento dell'endpoint.|  
  
## <a name="remarks"></a>Note  
 Usare questo comportamento per fornire al listener del canale l'istruzione di usare la ricezione sincrona anziché l'impostazione predefinita, ovvero la modalità asincrona. Windows Communication Foundation (WCF) genera un nuovo thread per la distribuzione per ogni canale accettato. Se esistono molti canali, sussiste la possibilità di esaurire i thread.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.ServiceModel.Configuration.SynchronousReceiveElement>
- <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>
