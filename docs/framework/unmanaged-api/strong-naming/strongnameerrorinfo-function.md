---
title: Funzione StrongNameErrorInfo
ms.date: 03/30/2017
api_name:
- StrongNameErrorInfo
api_location:
- mscoree.dll
- mscorsn.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameErrorInfo
helpviewer_keywords:
- StrongNameErrorInfo function [.NET Framework strong naming]
ms.assetid: e91bf8c3-7c26-4732-938e-2e5b04abfc99
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 909c283b1355153ffe1aa02acfbe8acc25a7e215
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59124098"
---
# <a name="strongnameerrorinfo-function"></a>Funzione StrongNameErrorInfo
Ottiene l'ultimo codice di errore che è stato generato da una delle funzioni con nome sicuro.  
  
 Questa funzione è stata deprecata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT StrongNameErrorInfo ();   
```  
  
## <a name="return-value"></a>Valore restituito  
 L'ultimo codice di errore COM impostato da una delle funzioni con nome sicuro.  
  
## <a name="remarks"></a>Note  
 La maggior parte dei metodi con nome sicuro restituiscono un semplice `true` o `false` indicazione del completamento. Usare il `StrongNameErrorInfo` funzione per recuperare un valore HRESULT che specifica l'ultimo errore generato dalle funzioni con nome sicuro.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** StrongName.h  
  
 **Libreria:** Inclusa come risorsa in Mscoree. dll  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
