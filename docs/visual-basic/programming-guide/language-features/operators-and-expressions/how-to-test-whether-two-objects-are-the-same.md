---
title: 'Procedura: Verificare se due oggetti sono la stessa (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], reference
- Is operator [Visual Basic], comparing objects
- reference variables [Visual Basic]
- variables [Visual Basic], referring to same object
- objects [Visual Basic], variables referring to same
- Visual Basic code, operators
ms.assetid: f760e828-8704-4256-bc2d-c22a4c93b524
ms.openlocfilehash: dbb268175d197e7b931af45a98f3a273c593e5a3
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58819125"
---
# <a name="how-to-test-whether-two-objects-are-the-same-visual-basic"></a>Procedura: Verificare se due oggetti sono la stessa (Visual Basic)
Se si dispone di due variabili fanno riferimento agli oggetti, è possibile usare la `Is` o `IsNot` operatore o entrambi, per determinare se si riferiscono alla stessa istanza.  
  
### <a name="to-test-whether-two-objects-are-the-same"></a>Per verificare se due oggetti sono uguali.  
  
-   Usare la [operatore Is](../../../../visual-basic/language-reference/operators/is-operator.md) o nella [operatore IsNot](../../../../visual-basic/language-reference/operators/isnot-operator.md) con le due variabili come operandi.  
  
     [!code-vb[VbVbalrOperators#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#69)]  
  
 È possibile eseguire una determinata azione a seconda del fatto che due oggetti si riferiscono alla stessa istanza. Nell'esempio precedente viene confrontato il controllo `c` con il controllo attivo sul form `f`. Se non è disponibile alcun controllo attivo o se è presente uno ma non è la stessa istanza di controllo come `c`, quindi il `If` istruzione ha esito negativo e la procedura restituisce senza ulteriore elaborazione.  
  
 Se si utilizza `Is` o `IsNot` è una questione di praticità aggiuntivo personale all'utente. Uno potrebbe essere più facile da leggere rispetto a altro in una determinata espressione.  
  
## <a name="see-also"></a>Vedere anche

- [Operatori di confronto in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
