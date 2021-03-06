---
title: Autorizzazione in WCF
ms.date: 03/30/2017
helpviewer_keywords:
- authorization [WCF]
- security [WCF], authorization
ms.assetid: 8ea0b552-af65-45b0-a157-c6c111b8ce5e
ms.openlocfilehash: 26aa445f3136fcb16e2eb9cdce6b245476297dfd
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59161364"
---
# <a name="authorization-in-wcf"></a>Autorizzazione in WCF
L'autorizzazione è il processo di controllo dell'accesso e dei diritti alle risorse, ad esempio servizi o file. Gli argomenti in questa sezione illustrano come eseguire questa attività di base in Windows Communication Foundation (WCF) in diversi modi.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Meccanismi del controllo di accesso](../../../../docs/framework/wcf/feature-details/access-control-mechanisms.md)  
 Fornisce una breve descrizione dei meccanismi di autorizzazione in WCF e Usa suggerita.  
  
 [Procedura: Limitare l'accesso con la classe PrincipalPermissionAttribute](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)  
 Viene illustrato il processo di restrizione dell'accesso a un servizio con l'attributo <xref:System.Security.Permissions.PrincipalPermissionAttribute>.  
  
 [Procedura: Usare il provider di ruoli ASP.NET con un servizio](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)  
 Viene illustrata la configurazione di un servizio per attivare l'utilizzo della funzionalità del provider di ruoli di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
 [Procedura: Usare il provider di ruoli ASP.NET di Gestione autorizzazioni con un servizio](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)  
 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] può usare il gestore dell'autorizzazione per gestire le autorizzazioni per un sito Web. WCF in modo analogo è possibile sfruttare il [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]combinazione /Authorization Manager per l'autorizzazione dei client.  
  
 [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)  
 Vengono spiegate le nozioni di base dell'utilizzo dell'infrastruttura del modello di identità per l'autorizzazione basata su richieste.  
  
 [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)  
 Viene spiegata la differenza tra delega e rappresentazione.  
  
## <a name="reference"></a>Riferimenti  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.ServiceModel.Description.PrincipalPermissionMode>  
  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Autenticazione](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)  
  
## <a name="see-also"></a>Vedere anche

- [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [Sicurezza e protezione](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
