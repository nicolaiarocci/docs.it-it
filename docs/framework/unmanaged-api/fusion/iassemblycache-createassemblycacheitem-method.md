---
title: Metodo IAssemblyCache::CreateAssemblyCacheItem
ms.date: 03/30/2017
api_name:
- IAssemblyCache.CreateAssemblyCacheItem
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCache::CreateAssemblyCacheItem
helpviewer_keywords:
- IAssemblyCache::CreateAssemblyCacheItem method [.NET Framework fusion]
- CreateAssemblyCacheItem method [.NET Framework fusion]
ms.assetid: 017a7ba5-aaaf-44e2-9cbe-ceebef259df0
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 648b641cbd2ec97305674451df06ce5be6a93a49
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59183690"
---
# <a name="iassemblycachecreateassemblycacheitem-method"></a>Metodo IAssemblyCache::CreateAssemblyCacheItem
Ottiene un riferimento a una nuova [IAssemblyCacheItem](../../../../docs/framework/unmanaged-api/fusion/iassemblycacheitem-interface.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT CreateAssemblyCacheItem (  
    [in]  DWORD dwFlags,  
    [in]  PVOID pvReserved,  
    [out] IAssemblyCacheItem **ppAsmItem,  
    [in, optional] LPCWSTR pszAssemblyName  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `dwFlags`  
 [in] Flag definiti in Fusion. Sono supportati i valori seguenti:  
  
-   IASSEMBLYCACHE_INSTALL_FLAG_REFRESH (0x00000001)  
  
-   IASSEMBLYCACHE_INSTALL_FLAG_FORCE_REFRESH (0x00000002)  
  
 `pvReserved`  
 [in] Riservato per un'estendibilità futura. `pvReserved` deve essere un riferimento null.  
  
 `ppAsmItem`  
 [out] L'oggetto restituito `IAssemblyCacheItem` puntatore.  
  
 `pszAssemblyName`  
 [in, optional] In formato non canonico, delimitati da virgole `name=value` coppie.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Fusion. h  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia IAssemblyCache](../../../../docs/framework/unmanaged-api/fusion/iassemblycache-interface.md)
- [Interfaccia IAssemblyCacheItem](../../../../docs/framework/unmanaged-api/fusion/iassemblycacheitem-interface.md)
