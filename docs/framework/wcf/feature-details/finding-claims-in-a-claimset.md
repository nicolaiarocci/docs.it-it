---
title: Ricerca di attestazioni in un ClaimSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- claims [WCF], finding in a claimset
- claims [WCF]
ms.assetid: a76ce107-aeb3-47d0-bfa9-134c53664e20
ms.openlocfilehash: 42e6ee682220913f872da337eb41f6c290082988
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59137124"
---
# <a name="finding-claims-in-a-claimset"></a>Ricerca di attestazioni in un ClaimSet
L'esame del contenuto di una classe <xref:System.IdentityModel.Claims.ClaimSet> per particolari tipi di attestazioni è un'attività comune quando si utilizza l'autorizzazione basata sulle attestazioni. Per esaminare una classe <xref:System.IdentityModel.Claims.ClaimSet> al fine di verificare la presenza di attestazioni particolari, utilizzare il metodo <xref:System.IdentityModel.Claims.ClaimSet.FindClaims%2A>. Questo metodo fornisce prestazioni migliori che non l'iterazione diretta su <xref:System.IdentityModel.Claims.ClaimSet>. Nell'esempio seguente viene illustrata questa sintassi. Si noti che i parametri `claimType` e `claimRight` possono essere `null`. In tal caso i parametri corrisponderanno a tutti i tipi e i diritti di attestazione.  
  
## <a name="example"></a>Esempio  
 [!code-csharp[c_FindClaimsPerf#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_findclaimsperf/cs/c_findclaimsperf.cs#2)]
 [!code-vb[c_FindClaimsPerf#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_findclaimsperf/vb/c_findclaimsperf.vb#2)]  
  
## <a name="see-also"></a>Vedere anche

- [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
