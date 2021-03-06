---
ms.openlocfilehash: fe5dfa0b8866debd8a6091a264e251f2fd2e4dca
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59234500"
---
### <a name="x509certificateclaimsetfindclaims-considers-all-claimtypes"></a>X509CertificateClaimSet.FindClaims considera tutti gli argomenti claimType

|   |   |
|---|---|
|Dettagli|Nelle app destinate a .NET Framework 4.6.1, se un set di attestazioni X509 viene inizializzato da un certificato con più voci DNS nel proprio campo SAN, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=name> cerca di stabilire una corrispondenza con l'argomento claimType con tutte le voci DNS. Per le app destinate a versioni precedenti di .NET Framework, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=name> tenta di stabilire una corrispondenza con l'argomento claimType solo con l'ultima voce DNS.|
|Suggerimento|Questa modifica riguarda solo le applicazioni destinate a .NET Framework 4.6.1. Questa modifica può essere disabilitata (o abilitata se la destinazione è una versione precedente la 4.6.1) con l'opzione di compatibilità [DisableMultipleDNSEntries](~/docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md#mitigation).|
|Ambito|Secondario|
|Versione|4.6.1|
|Tipo|Ridestinazione|
|API interessate|<ul><li><xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=nameWithType></li></ul>|
