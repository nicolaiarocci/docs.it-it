---
ms.openlocfilehash: dbe96abebdc61fae469f7727673e6fcb93cbc739
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236644"
---
### <a name="no-longer-able-to-set-enableviewstatemac-to-false"></a>Non è più possibile impostare EnableViewStateMac su false

|   |   |
|---|---|
|Dettagli|ASP.NET non consente più agli sviluppatori di specificare <code>&lt;pages enableViewStateMac=&quot;false&quot;/&gt;</code> o <code>&lt;@Page EnableViewStateMac=&quot;false&quot; %&gt;</code>. L'algoritmo Message Authentication Code (MAC) dello stato di visualizzazione viene ora applicato per tutte le richieste con stato di visualizzazione incorporato. Riguarda solo le app che impostano in modo esplicito la proprietà EnableViewStateMac su <code>false</code>.|
|Suggerimento|Partire dal presupposto che la proprietà EnableViewStateMac sia true e risolvere eventuali errori MAC risultanti, come spiegato in [queste istruzioni](https://support.microsoft.com/kb/2915218) che contengono più soluzioni in base alle cause specifiche degli errori MAC.|
|Ambito|Principale|
|Versione|4.5.2|
|Tipo|Runtime|
