---
title: 'Procedura: Gestire le chiavi composite nelle query'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ce2f14fd-1038-458a-91e3-a078c61f0d10
ms.openlocfilehash: 2621ab4db207d1b868fbe3778c30c744201b0506
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59135252"
---
# <a name="how-to-handle-composite-keys-in-queries"></a>Procedura: Gestire le chiavi composite nelle query
Alcuni operatori possono accettare un solo argomento. Se l'argomento deve includere più di una colonna del database, è necessario creare un tipo anonimo per rappresentare la combinazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata una query che richiama l'operatore `GroupBy` che può accettare un solo argomento `key`.  
  
 [!code-csharp[DLinqCompositeKeys#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCompositeKeys/cs/Program.cs#1)]
 [!code-vb[DLinqCompositeKeys#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCompositeKeys/vb/Module1.vb#1)]  
  
## <a name="example"></a>Esempio  
 La stessa situazione è applicabile ai join, come nell'esempio seguente:  
  
 [!code-csharp[DLinqCompositeKeys#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCompositeKeys/cs/Program.cs#2)]
 [!code-vb[DLinqCompositeKeys#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCompositeKeys/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>Vedere anche

- [Concetti relatici alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)
