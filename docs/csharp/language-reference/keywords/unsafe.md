---
title: Parola chiave unsafe - Riferimenti per C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- unsafe_CSharpKeyword
- unsafe
helpviewer_keywords:
- unsafe keyword [C#]
ms.assetid: 7e818009-1c6e-4b9e-b769-3728a01586a0
ms.openlocfilehash: 81a293a6922a71f7428167c50aed064d7387a099
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53236622"
---
# <a name="unsafe-c-reference"></a>unsafe (Riferimenti per C#)

La parola chiave `unsafe` denota un contesto unsafe, necessario per qualsiasi operazione che interessa i puntatori. Per altre informazioni, vedere [Codice unsafe e puntatori](../../programming-guide/unsafe-code-pointers/index.md).

È possibile usare il modificatore `unsafe` nella dichiarazione di un tipo o di un membro. L'intera estensione testuale del tipo o membro viene pertanto considerato come contesto unsafe. Ad esempio, il seguente è un metodo dichiarato con il modificatore `unsafe`:

```csharp
unsafe static void FastCopy(byte[] src, byte[] dst, int count)
{
    // Unsafe context: can use pointers here.
}
```

L'ambito del contesto unsafe si estende dall'elenco di parametri alla fine del metodo, in modo tale che i puntatori possano essere usati anche nell'elenco dei parametri:

```csharp
unsafe static void FastCopy ( byte* ps, byte* pd, int count ) {...}
```

È anche possibile usare un blocco unsafe per consentire l'uso di un codice unsafe all'interno del blocco. Ad esempio:

```csharp
unsafe
{
    // Unsafe context: can use pointers here.
}
```

Per compilare codice unsafe, è necessario specificare l'opzione del compilatore [/unsafe](../compiler-options/unsafe-compiler-option.md). Il codice unsafe non è verificabile da Common Language Runtime.

## <a name="example"></a>Esempio

[!code-csharp[csrefKeywordsModifiers#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#22)]

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

Per altre informazioni, vedere [Codice di tipo unsafe](~/_csharplang/spec/unsafe-code.md) nella [specifica del linguaggio C#](../language-specification/index.md). La specifica del linguaggio costituisce il riferimento ufficiale principale per la sintassi e l'uso di C#.

## <a name="see-also"></a>Vedere anche

- [Riferimenti per C#](../index.md)
- [Guida per programmatori C#](../../programming-guide/index.md)
- [Parole chiave di C#](index.md)
- [Istruzione fixed](fixed-statement.md)
- [Codice unsafe e puntatori](../../programming-guide/unsafe-code-pointers/index.md)
- [Buffer a dimensione fissa](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md)