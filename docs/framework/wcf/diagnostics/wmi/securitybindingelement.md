---
title: SecurityBindingElement
ms.date: 03/30/2017
ms.assetid: ef93b6e6-3524-48a8-94d3-c8837f1872f9
ms.openlocfilehash: 1d367d0c5d14e6e75539dd2b20cdffcf2b34963d
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59153855"
---
# <a name="securitybindingelement"></a>SecurityBindingElement
SecurityBindingElement  
  
## <a name="syntax"></a>Sintassi  
  
```csharp
class SecurityBindingElement : BindingElement  
{  
  string DefaultAlgorithmSuite;  
  boolean IncludeTimestamp;  
  string KeyEntropyMode;  
  LocalServiceSecuritySettings LocalServiceSecuritySettings;  
  string MessageSecurityVersion;  
  string SecurityHeaderLayout;  
};  
```  
  
## <a name="methods"></a>Metodi  
 La classe SecurityBindingElement non definisce metodi.  
  
## <a name="properties"></a>Proprietà  
 La classe SecurityBindingElement ha le proprietà seguenti:  
  
### <a name="defaultalgorithmsuite"></a>DefaultAlgorithmSuite  
 Tipo di dati: stringa  
  
 Tipo di accesso: Sola lettura  
  
 Specifica gli algoritmi da usare con l'associazione.  
  
### <a name="includetimestamp"></a>IncludeTimestamp  
 Tipo di dati: booleano  
  
 Tipo di accesso: Sola lettura  
  
 Valore booleano che specifica se ogni messaggio contiene un timestamp.  
  
### <a name="keyentropymode"></a>KeyEntropyMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: Sola lettura  
  
 Origine dell'entropia usata per creare chiavi.  
  
### <a name="localservicesecuritysettings"></a>LocalServiceSecuritySettings  
 Tipo di dati: LocalServiceSecuritySettings  
  
 Tipo di accesso: Sola lettura  
  
 Proprietà di sicurezza specifiche dell'associazione per il servizio locale.  
  
### <a name="messagesecurityversion"></a>MessageSecurityVersion  
 Tipo di dati: stringa  
  
 Tipo di accesso: Sola lettura  
  
 Versione usata per la protezione del messaggio.  
  
### <a name="securityheaderlayout"></a>SecurityHeaderLayout  
 Tipo di dati: stringa  
  
 Tipo di accesso: Sola lettura  
  
 Ordine degli elementi nell'intestazione di sicurezza di questa associazione.  
  
## <a name="requirements"></a>Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-----------------------------------|  
|Spazio dei nomi|Definito in root\ServiceModel|  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.ServiceModel.Channels.SecurityBindingElement>
