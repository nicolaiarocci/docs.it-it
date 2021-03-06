---
title: "Procedura: Aggiungere un'animazione alle modifiche di dimensione usando fotogrammi chiave"
ms.date: 03/30/2017
helpviewer_keywords:
- key frames [WPF], animating size changes with
- animation [WPF], size changes with key frames
- size changes [WPF], animating with key frames
ms.assetid: 86bd2950-d4c9-4ec4-aa8d-7dc3ccadded4
ms.openlocfilehash: 0629b6600444bd172af451fd7e970bff894d8047
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59342366"
---
# <a name="how-to-animate-size-changes-by-using-key-frames"></a>Procedura: Aggiungere un'animazione alle modifiche di dimensione usando fotogrammi chiave
Questo esempio mostra come animare le modifiche di dimensione usando fotogrammi chiave.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa il <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames> classe per animare la <xref:System.Windows.Media.ArcSegment.Size%2A> proprietà di un <xref:System.Windows.Media.ArcSegment>. Questa animazione usa tre fotogrammi chiave nel modo seguente:  
  
1. Il primo mezzo secondo dell'animazione, viene usata un'istanza del <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> classe per aumentare gradualmente la dimensione dell'arco. Fotogrammi chiave lineari come <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> creano una transizione lineare uniforme tra i valori.  
  
2. Alla fine del successivo mezzo secondo viene usata un'istanza del <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> classe improvvisamente aumentare la dimensione dell'arco. Fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> creano salti improvvisi tra valori, vale a dire, le modifiche di dimensione si verificano improvvisamente e risultano immediatamente evidenti.  
  
3. Tramite i due secondi finali viene utilizzata un'istanza di <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> classe per aumentare la dimensione dell'arco. Ad esempio i fotogrammi chiave spline <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> creano una transizione variabile tra i valori a seconda dei valori del <xref:System.Windows.Media.Animation.SplineSizeKeyFrame.KeySpline%2A> proprietà. In questo esempio la dimensione dell'arco aumenta lentamente all'inizio e quindi aumenta in misura esponenziale verso la fine dell'intervallo di tempo.  
  
 [!code-xaml[keyframes_snip#SizeAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/SizeAnimationUsingKeyFramesExample.xaml#sizeanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](https://go.microsoft.com/fwlink/?LinkID=160012).  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>
- <xref:System.Windows.Media.ArcSegment.Size%2A>
- <xref:System.Windows.Media.ArcSegment>
- <xref:System.Windows.Media.Animation.LinearSizeKeyFrame>
- <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame>
- <xref:System.Windows.Media.Animation.SplineSizeKeyFrame>
- [Cenni preliminari sulle animazioni con fotogrammi chiave](key-frame-animations-overview.md)
- [Procedure relative ai fotogrammi chiave](key-frame-animation-how-to-topics.md)
