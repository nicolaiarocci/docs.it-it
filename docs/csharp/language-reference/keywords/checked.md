---
title: Parola chiave checked - Riferimenti per C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- checked_CSharpKeyword
- checked
helpviewer_keywords:
- checked keyword [C#]
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
ms.openlocfilehash: 5ce9291fd047dfa9c69048887ccbd878819f2de8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/23/2019
ms.locfileid: "54533131"
---
# <a name="checked-c-reference"></a>checked (Riferimenti per C#)

La parola chiave `checked` viene usata per abilitare in modo esplicito il controllo dell'overflow per le conversioni e le operazioni aritmetiche di tipo integrale.

Per impostazione predefinita, un'espressione che contiene solo valori costanti provoca un errore di compilazione se l'espressione produce un valore che non è incluso nell'intervallo del tipo di destinazione. Se l'espressione contiene uno o più valori non costanti, il compilatore non rileva l'overflow. La valutazione dell'espressione assegnata a `i2` nell'esempio seguente non genera un errore di compilazione.

[!code-csharp[csrefKeywordsChecked#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#3)]

Per impostazione predefinita, in queste espressioni non costanti non viene verificato l'overflow in fase di esecuzione e non vengono generate eccezioni di overflow. Nell'esempio precedente viene visualizzato il valore -2,147,483,639 come somma di due numeri interi positivi.

Il controllo dell'overflow può essere abilitato tramite le opzioni del compilatore, la configurazione dell'ambiente o l'uso della parola chiave `checked`. Gli esempi seguenti illustrano come usare un'espressione `checked` o un blocco `checked` per rilevare l'overflow generato dalla somma precedente in fase di esecuzione. Entrambi gli esempi generano un'eccezione di overflow.

[!code-csharp[csrefKeywordsChecked#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#4)]

La parola chiave [unchecked](../../../csharp/language-reference/keywords/unchecked.md) può essere usata per impedire il controllo dell'overflow.

## <a name="example"></a>Esempio

Questo esempio illustra come usare `checked` per abilitare il controllo dell'overflow in fase di esecuzione.

[!code-csharp[csrefKeywordsChecked#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#1)]

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Vedere anche

- [Riferimenti per C#](../../../csharp/language-reference/index.md)
- [Guida per programmatori C#](../../../csharp/programming-guide/index.md)
- [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)
- [Checked e Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)
- [unchecked](../../../csharp/language-reference/keywords/unchecked.md)
