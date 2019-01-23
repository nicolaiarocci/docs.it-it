---
title: Interfaccia ISOSDacInterface
ms.date: 01/16/2019
api.name:
- ISOSDacInterface Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface Interface
helpviewer.keywords:
- ISOSDacInterface Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 5e037cf6fb88fff4886733ff4152dca0a827e0a3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/23/2019
ms.locfileid: "54491028"
---
# <a name="isosdacinterface-interface"></a><span data-ttu-id="74d5a-102">Interfaccia ISOSDacInterface</span><span class="sxs-lookup"><span data-stu-id="74d5a-102">ISOSDacInterface Interface</span></span>

<span data-ttu-id="74d5a-103">Fornisce metodi helper per accedere ai dati da `SOS`.</span><span class="sxs-lookup"><span data-stu-id="74d5a-103">Provides helper methods to access data from `SOS`.</span></span>

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a><span data-ttu-id="74d5a-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="74d5a-104">Methods</span></span>

| <span data-ttu-id="74d5a-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="74d5a-105">Method</span></span>                                                                                                               | <span data-ttu-id="74d5a-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="74d5a-106">Description</span></span>                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [<span data-ttu-id="74d5a-107">GetMethodDescData</span><span class="sxs-lookup"><span data-stu-id="74d5a-107">GetMethodDescData</span></span>](../../../../docs/framework/unmanaged-api/debugging/isosdacinterface-getmethoddescdata-method.md) | <span data-ttu-id="74d5a-108">Ottiene i dati per il dato [MethodDesc](../../../../docs/framework/unmanaged-api/common-data-types-unmanaged-api-reference.md).</span><span class="sxs-lookup"><span data-stu-id="74d5a-108">Gets the data for the given [MethodDesc](../../../../docs/framework/unmanaged-api/common-data-types-unmanaged-api-reference.md).</span></span> |

## <a name="remarks"></a><span data-ttu-id="74d5a-109">Note</span><span class="sxs-lookup"><span data-stu-id="74d5a-109">Remarks</span></span>

<span data-ttu-id="74d5a-110">Questa interfaccia si trova all'interno del runtime e non viene esposto tramite le intestazioni o i file di libreria.</span><span class="sxs-lookup"><span data-stu-id="74d5a-110">This interface lives inside the runtime and is not exposed through any headers or library files.</span></span> <span data-ttu-id="74d5a-111">Tuttavia, è un'interfaccia COM che deriva da `IUnknown` con GUID `436f00f2-b42a-4b9f-870c-e73db66ae930` che può essere ottenuto tramite i normali meccanismi di COM.</span><span class="sxs-lookup"><span data-stu-id="74d5a-111">However, it's a COM interface that derives from `IUnknown` with GUID `436f00f2-b42a-4b9f-870c-e73db66ae930` that can be obtained through the usual COM mechanisms.</span></span>

## <a name="requirements"></a><span data-ttu-id="74d5a-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="74d5a-112">Requirements</span></span>

<span data-ttu-id="74d5a-113">**Piattaforme:** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="74d5a-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
<span data-ttu-id="74d5a-114">**Intestazione:** nessuno</span><span class="sxs-lookup"><span data-stu-id="74d5a-114">**Header:** None</span></span>  
<span data-ttu-id="74d5a-115">**Libreria:** nessuno</span><span class="sxs-lookup"><span data-stu-id="74d5a-115">**Library:** None</span></span>  
<span data-ttu-id="74d5a-116">**Versioni di .NET Framework:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span><span class="sxs-lookup"><span data-stu-id="74d5a-116">**.NET Framework Versions:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="74d5a-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="74d5a-117">See also</span></span>

- [<span data-ttu-id="74d5a-118">Debug</span><span class="sxs-lookup"><span data-stu-id="74d5a-118">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [<span data-ttu-id="74d5a-119">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="74d5a-119">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)