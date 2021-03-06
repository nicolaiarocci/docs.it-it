---
ms.openlocfilehash: 68da7216890da1819a994161507355a0b5ea1f9f
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236059"
---
### <a name="signedxml-and-encryptedxml-breaking-changes"></a>Modifiche di SignedXml ed EncryptedXml che causano interruzioni

|   |   |
|---|---|
|Dettagli|In .NET Framework 4.6.2 , le correzioni per la sicurezza in <xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=name> e <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=name> causano comportamenti diversi in fase di esecuzione. Ad esempio,<ul><li>se per un documento esistono più elementi con lo stesso attributo <code>id</code> e una firma fa riferimento a uno di tali elementi come radice della firma, il documento ora verrà considerato non valido.</li><li>I documenti che usano algoritmi di trasformazione XPath non canonici nei riferimenti ora vengono considerati non validi.</li><li>I documenti che usano algoritmi di trasformazione XSLT non canonici nei riferimenti ora vengono considerati non validi.</li><li>Eventuali programmi che usano firme di risorse esterne scollegate non saranno in grado di eseguire questa operazione.</li></ul>|
|Suggerimento|Gli sviluppatori devono esaminare l'uso di <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> e <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> nonché dei tipi derivati da <xref:System.Security.Cryptography.Xml.Transform>, poiché un destinatario del documento potrebbe non essere in grado di elaborarlo.|
|Ambito|Secondario|
|Versione|4.6.2|
|Tipo|Runtime|
|API interessate|<ul><li><xref:System.Security.Cryptography.Xml.Transform?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.XmlDsigXPathTransform?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform?displayProperty=nameWithType></li></ul>|
