---
ms.openlocfilehash: 297af393e86c65e84ea7271d98eab36dbc6dbb0e
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59234761"
---
### <a name="some-workflow-drag-and-drop-apis-are-obsolete"></a>Alcune API WorkFlow con trascinamento della selezione sono obsolete

|   |   |
|---|---|
|Dettagli|Questa API WorkFlow con trascinamento della selezione è obsoleta e genera avvisi del compilatore se l'app viene ricompilata per la versione 4.5.|
|Suggerimento|In alternativa è consigliabile usare le nuove API <xref:System.Activities.Presentation.DragDropHelper?displayProperty=name> che supportano operazioni con più oggetti. In alternativa, è possibile eliminare gli avvisi di compilazione o evitarli usando un compilatore precedente. Le API sono ancora supportate.|
|Ambito|Secondario|
|Versione|4.5|
|Tipo|Ridestinazione|
|API interessate|<ul><li><xref:System.Activities.Presentation.DragDropHelper.DoDragMove(System.Activities.Presentation.WorkflowViewElement,System.Windows.Point)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetCompositeView(System.Windows.DragEventArgs)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetDraggedModelItem(System.Windows.DragEventArgs)?displayProperty=nameWithType></li><li><xref:System.Activities.Presentation.DragDropHelper.GetDroppedObject(System.Windows.DependencyObject,System.Windows.DragEventArgs,System.Activities.Presentation.EditingContext)?displayProperty=nameWithType></li></ul>|
