---
title: 'Procedura: Usare i colori di sistema in una sfumatura'
ms.date: 03/30/2017
helpviewer_keywords:
- gradients [WPF], system colors in
- system colors in gradients [WPF]
ms.assetid: 11942e7e-6300-4b50-8ed1-f50e8d20e7d2
ms.openlocfilehash: 55c99640907a0c372f8c7bbc50b9b45c9f15ef3c
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59229440"
---
# <a name="how-to-use-system-colors-in-a-gradient"></a>Procedura: Usare i colori di sistema in una sfumatura
Per usare un colore di sistema in una sfumatura, si utilizza il  *\<SystemColor >* colore e  *\<SystemColor >* ColorKey proprietà statiche del <xref:System.Windows.SystemColors> classe per ottenere una riferimento al colore, dove  *\<SystemColor >* è il nome del colore di sistema desiderato. Usare la  *\<SystemColor >* ColorKey proprietà quando si desidera creare un riferimento dinamico che viene aggiornato automaticamente quando cambia il tema del sistema. In caso contrario, usare il  *\<SystemColor >* proprietà dei colori.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa risorse di colore di sistema dinamiche per creare una sfumatura.  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemColorExample.xaml#graphicsmmdynamicsystemcolorgradientexamplewholepage)]  
  
 L'esempio seguente usa risorse di colore di sistema statiche per creare una sfumatura.  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemColorExample.xaml#graphicsmmstaticsystemcolorgradientexamplewholepage)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.SystemColors>
- [Disegnare un'area con un pennello di sistema](how-to-paint-an-area-with-a-system-brush.md)
- [Cenni sul disegno con colori a tinta unita e sfumature](painting-with-solid-colors-and-gradients-overview.md)
