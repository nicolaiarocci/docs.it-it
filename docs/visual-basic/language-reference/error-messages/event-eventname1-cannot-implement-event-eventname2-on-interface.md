---
title: L'evento '<eventname1>' non può implementare l'evento '<eventname2>' nell'interfaccia '<interface>' poiché i tipi delegati '<delegate1>' e '<delegate2>' non corrispondono
ms.date: 07/20/2015
f1_keywords:
- vbc31423
- bc31423
helpviewer_keywords:
- BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
ms.openlocfilehash: 9581168fa86f8f0715e004b60c2eb2a813cd38ab
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58840523"
---
# <a name="event-eventname1-cannot-implement-event-eventname2-on-interface-interface-because-their-delegate-types-delegate1-and-delegate2-do-not-match"></a>Evento '\<eventname1 >' non può implementare l'evento '\<eventname2 >' nell'interfaccia '\<interfaccia >' perché i relativi tipi delegato\<delegate1 >' e '\<delegate2 >' non corrispondono
Visual Basic non può implementare un evento perché il tipo di delegato dell'evento non corrisponde al tipo delegato dell'evento nell'interfaccia. Questo errore può insorgere quando si definiscono più eventi in un'interfaccia e si prova a implementarli assieme con lo stesso evento. Un evento può implementare due o più eventi solo se tutti gli eventi implementati vengono dichiarati usando la sintassi `As` e se tutti specificano lo stesso tipo delegato.  
  
 **ID errore:** BC31423  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Implementare gli eventi separatamente.  
  
     -oppure-  
  
-   Definire gli eventi nell'interfaccia utilizzando il `As` sintassi e specificare lo stesso tipo di delegato.  
  
## <a name="see-also"></a>Vedere anche

- [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)
- [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)
- [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)
