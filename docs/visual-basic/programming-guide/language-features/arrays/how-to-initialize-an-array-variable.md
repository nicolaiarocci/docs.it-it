---
title: 'Procedura: Inizializzare una variabile di matrice in Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], initializing
- arrays [Visual Basic], variables
- arrays [Visual Basic], initializing
- arrays [Visual Basic], declaring
ms.assetid: aadd7a60-7ca4-4608-b986-091f19e7fc10
ms.openlocfilehash: 4aa783d6179c72760a12d0259d587b5b38bb9140
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58832242"
---
# <a name="how-to-initialize-an-array-variable-in-visual-basic"></a>Procedura: Inizializzare una variabile di matrice in Visual Basic
Inizializzare una variabile di matrice includendo un valore letterale nell'array un `New` clausola e specificando i valori iniziali della matrice. È possibile specificare il tipo o consentire che possa essere dedotto dai valori nel valore letterale di matrice. Per ulteriori informazioni su come viene dedotto il tipo, vedere "Popolamento di una matrice con valori iniziali" nella [matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
### <a name="to-initialize-an-array-variable-by-using-an-array-literal"></a>Per inizializzare una variabile di matrice usando un valore letterale di matrice  
  
-   Nel `New` clausola, o quando si assegna il valore della matrice, fornire i valori degli elementi tra parentesi graffe (`{}`). Nell'esempio seguente vengono illustrati diversi modi per dichiarare, creare e inizializzare una variabile per contenere una matrice con elementi di tipo `Char`.  
  
     [!code-vb[VbVbalrArrays#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#16)]  
  
     Dopo l'esecuzione di ogni istruzione, la matrice creata ha una lunghezza pari a 3, con elementi in corrispondenza dell'indice 0 e l'indice 2 contenenti i valori iniziali. Se si specificano sia il limite superiore che i valori, è necessario includere un valore per ogni elemento dall'indice 0 al limite superiore.  
  
     Si noti che non è necessario specificare il limite superiore dell'indice se si specificano valori degli elementi in un valore letterale di matrice. Se non viene specificato alcun limite superiore, la dimensione della matrice viene dedotta in base al numero di valori nel valore letterale di matrice.  
  
### <a name="to-initialize-a-multidimensional-array-variable-by-using-array-literals"></a>Per inizializzare una variabile di matrice multidimensionale tramite valori letterali di matrice  
  
-   Annidare i valori tra parentesi graffe (`{}`) all'interno delle parentesi graffe. Verificare che i valori letterali di matrice annidati che tutti dedotti come matrici dello stesso tipo e lunghezza. Esempio di codice seguente mostra alcuni esempi di inizializzazione di matrici multidimensionali.  
  
     [!code-vb[VbVbalrArrays#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#17)]  
  
-   In modo esplicito, è possibile specificare i limiti della matrice o tralasciarli e che il compilatore li deduca in base ai valori nel valore letterale di matrice. Se si specificano sia i limiti superiori che i valori, è necessario includere un valore per ogni elemento dall'indice 0 al limite superiore di ogni dimensione. Nell'esempio seguente vengono illustrati diversi modi per dichiarare, creare e inizializzare una variabile per contenere una matrice bidimensionale con elementi di tipo `Short`  
  
     [!code-vb[VbVbalrArrays#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#18)]  
  
     Dopo l'esecuzione di ogni istruzione, la matrice creata contiene sei elementi inizializzati che includono indici `(0,0)`, `(0,1)`, `(0,2)`, `(1,0)`, `(1,1)`, e `(1,2)`. Ogni posizione della matrice contiene il valore `10`.  
  
-   Nell'esempio seguente scorre una matrice multidimensionale. In un'applicazione console Windows scritta in Visual Basic, incollare il codice all'interno di `Sub Main()` (metodo). Gli ultimi commenti illustrano l'output.  
  
     [!code-vb[VbVbalrArrays#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#31)]  
  
### <a name="to-initialize-a-jagged-array-variable-by-using-array-literals"></a>Per inizializzare una variabile di matrice di matrici tramite valori letterali di matrice  
  
-   Annidare i valori di oggetto all'interno delle parentesi graffe (`{}`). Sebbene sia possibile annidare anche valori letterali di matrice che specificano matrici di lunghezze diverse, in caso di una matrice di matrici, assicurarsi che i valori letterali di matrice annidati siano racchiusi tra parentesi (`()`). Le parentesi forzano la valutazione dei valori letterali della matrice annidati e le matrici risultante vengono utilizzate come valori iniziali della matrice di matrici. Esempio di codice seguente mostra due esempi di inizializzazione di matrice di matrici.  
  
     [!code-vb[VbVbalrArrays#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#19)]  
  
-   Nell'esempio seguente scorre una matrice di matrici. In un'applicazione console Windows scritta in Visual Basic, incollare il codice all'interno di `Sub Main()` (metodo).  Gli ultimi commenti nel codice illustrano l'output.  
  
     [!code-vb[VbVbalrArrays#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#32)]  
  
## <a name="see-also"></a>Vedere anche

- [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [Risoluzione dei problemi relativi alle matrici](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)
