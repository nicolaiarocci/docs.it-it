---
title: "Procedura: Attivare un'animazione quando il valore di una proprietà viene modificato"
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], starting when property values change
- triggering animation [WPF]
- Storyboards [WPF], starting when property values change
ms.assetid: 12399c21-0300-4f4f-9e3a-d92d9907e5f5
ms.openlocfilehash: 7e3eecedf7d464eeb8e4f60f2f05fa06d2e23e09
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59080709"
---
# <a name="how-to-trigger-an-animation-when-a-property-value-changes"></a>Procedura: Attivare un'animazione quando il valore di una proprietà viene modificato
In questo esempio viene illustrato come utilizzare un <xref:System.Windows.Trigger> per avviare un <xref:System.Windows.Media.Animation.Storyboard> quando viene modificato un valore della proprietà. È possibile usare una <xref:System.Windows.Trigger> all'interno di un <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate>, o <xref:System.Windows.DataTemplate>.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa una <xref:System.Windows.Trigger> animare il <xref:System.Windows.UIElement.Opacity%2A> di un <xref:System.Windows.Controls.Button> quando relativo <xref:System.Windows.UIElement.IsMouseOver%2A> proprietà diventa `true`.  
  
 [!code-xaml[AnimatePropertyStoryboards#PropertyTriggerExample](~/samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/PropertyTriggerExample.xaml#propertytriggerexample)]  
  
 Le animazioni applicate dalla proprietà <xref:System.Windows.Trigger> oggetti si comportano in modo più complesso rispetto <xref:System.Windows.EventTrigger> animazioni o animazioni all'uso di <xref:System.Windows.Media.Animation.Storyboard> metodi.  Sono "consegne" animazioni definite da altri <xref:System.Windows.Trigger> oggetti, ma possono essere combinate con <xref:System.Windows.EventTrigger> e animazioni avviate tramite metodi.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Trigger>
- [Cenni preliminari sulle tecniche di animazione delle proprietà](property-animation-techniques-overview.md)
- [Cenni preliminari sugli storyboard](storyboards-overview.md)
