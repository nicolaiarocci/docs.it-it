---
title: Impossibile completare l'operazione. La directory di destinazione è una sottodirectory della directory di origine
ms.date: 07/20/2015
f1_keywords:
- vbrIO_CyclicOperation
ms.assetid: 850d3a24-5d51-4ac8-a912-630efcd75278
ms.openlocfilehash: f53ad664b341d4db803dee1f0f008c3918d13d93
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2019
ms.locfileid: "58039435"
---
# <a name="could-not-complete-operation-since-target-directory-is-under-source-directory"></a>Impossibile completare l'operazione. La directory di destinazione è una sottodirectory della directory di origine
Un'operazione ciclica non è riuscita. Queste operazioni sono cicliche e quindi non possono essere completate. Ad esempio, un oggetto A potrebbe provare a ereditare dall'oggetto B, che a sua volta eredita dall'oggetto A.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Quando si eredita, assicurarsi che non siano presenti riferimenti ciclici.  
  
## <a name="see-also"></a>Vedere anche

- [Tipi di errore](../../visual-basic/programming-guide/language-features/error-types.md)
- [Usare i punti di interruzione nel debugger di Visual Studio](/visualstudio/debugger/using-breakpoints)
