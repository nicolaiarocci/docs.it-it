---
title: Clausola Alias (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Alias
helpviewer_keywords:
- Alias keyword [Visual Basic]
ms.assetid: 58c06b11-465d-4d87-906a-73200a3d7f19
ms.openlocfilehash: 84c8f39e632eebbe5382492669820910b38bc360
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58839743"
---
# <a name="alias-clause-visual-basic"></a>Clausola Alias (Visual Basic)
Indica che una routine esterna ha un altro nome nella relativa DLL.  
  
## <a name="remarks"></a>Note  
 Il `Alias` parola chiave può essere usata in questo contesto:  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 Nell'esempio seguente, il `Alias` parola chiave viene usata per specificare il nome della funzione in advapi32.dll, `GetUserNameA`, che `getUserName` viene usato al posto di questo esempio. Funzione `getUserName` viene chiamato nella sub `getUser`, che consente di visualizzare il nome dell'utente corrente.  
  
 [!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>Vedere anche

- [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)
