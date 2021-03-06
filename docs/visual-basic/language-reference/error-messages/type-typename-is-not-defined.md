---
title: Tipo '<typename>' non definito
ms.date: 07/20/2015
f1_keywords:
- vbc30002
- bc30002
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
ms.openlocfilehash: c2675d61307d92da1710368668f43af3559060a3
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58825040"
---
# <a name="type-typename-is-not-defined"></a>Tipo '\<nomeTipo >' non è definito
L'istruzione ha fatto riferimento a un tipo che non è stato definito. È possibile definire un tipo in un'istruzione di dichiarazione, ad esempio `Enum`, `Structure`, `Class`, o `Interface`.  
  
 **ID errore:** BC30002  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Assicurarsi che la definizione del tipo e il relativo riferimento usino entrambi la stessa ortografia.  
  
-   Verificare che la definizione del tipo sia accessibile al riferimento. Ad esempio, se il tipo è in un altro modulo ed è stato dichiarato `Private`spostare la definizione del tipo per il riferimento modulo o dichiararla `Public`.  
  
-   Assicurarsi che lo spazio dei nomi del tipo viene ridefinito non all'interno del progetto. Se si tratta, usare il `Global` parola chiave per qualificare completamente il nome del tipo. Ad esempio, se un progetto definisce uno spazio dei nomi denominato `System`, il <xref:System.Object?displayProperty=nameWithType> tipo non è accessibile, a meno che non è completo, con la `Global` parola chiave: `Global.System.Object`.  
  
-   Se il tipo è definito, ma la libreria di oggetto o una libreria dei tipi in cui viene definito non è registrata in Visual Basic, scegliere **Aggiungi riferimento** nel **progetto** menu e quindi selezionare l'oggetto sia appropriato raccolta o libreria dei tipi.  
  
-   Assicurarsi che il tipo è in un assembly che fa parte del profilo di .NET Framework di destinazione. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli errori di impostazione di .NET Framework come destinazione](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors).  
  
## <a name="see-also"></a>Vedere anche

- [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [Istruzione Enum](../../../visual-basic/language-reference/statements/enum-statement.md)
- [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)
- [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Gestione dei riferimenti in un progetto](/visualstudio/ide/managing-references-in-a-project)
