---
title: '#Direttiva del preprocessore if - Riferimenti per C#'
ms.custom: seodec18
ms.date: 06/30/2018
f1_keywords:
- '#if'
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
ms.openlocfilehash: b92660a69194ff2d52cd78427f73510de514ea48
ms.sourcegitcommit: 4a8c2b8d0df44142728b68ebc842575840476f6d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2019
ms.locfileid: "58545819"
---
# <a name="if-c-reference"></a>#if (Riferimenti per C#)

Quando il compilatore C# trova una direttiva `#if` seguita da una direttiva [#endif](preprocessor-endif.md), compila il codice tra tali direttive solo se il simbolo specificato è definito. Diversamente da C e C++, non è possibile assegnare un valore numerico a un simbolo. L'istruzione #if in C# è di tipo booleano e verifica solo se il simbolo è stato definito o meno. Ad esempio:

```csharp
#if DEBUG
    Console.WriteLine("Debug version");
#endif
```

È possibile usare gli operatori [==](../operators/equality-operators.md#equality-operator-) (uguaglianza) e [!=](../operators/equality-operators.md#inequality-operator-) (disuguaglianza) solo per verificare se una condizione è [true](../keywords/true.md) o [false](../keywords/false.md). True significa che il simbolo è definito. L'istruzione `#if DEBUG` ha lo stesso significato di `#if (DEBUG == true)`. È possibile usare gli operatori [&&](../operators/conditional-and-operator.md) (and), [&#124;&#124;](../operators/conditional-or-operator.md) (or) e [!](../operators/logical-negation-operator.md) (not) per stabilire se sono stati definiti più simboli. È anche possibile raggruppare simboli e operatori tra parentesi.

## <a name="remarks"></a>Osservazioni

`#if`, nsieme alle direttive [#else](preprocessor-else.md), [#elif](preprocessor-elif.md), [#endif](preprocessor-endif.md), [#define](preprocessor-define.md) e [#undef](preprocessor-undef.md), consente di includere o escludere il codice in base all'esistenza di uno o più simboli. Questo può essere utile quando si compila il codice per una build di debug o per una configurazione specifica.

Una direttiva condizionale che inizia con `#if` deve terminare in modo esplicito con una direttiva `#endif`.

`#define` consente di definire un simbolo. Usando poi il simbolo come espressione passata alla direttiva `#if`, l'espressione restituisce `true`.

Un simbolo può anche essere definito tramite l'opzione del compilatore [-define](../compiler-options/define-compiler-option.md). Per rimuovere la definizione di un simbolo, è possibile usare [#undef](preprocessor-undef.md).

Un simbolo definito tramite `-define` o `#define` non provoca conflitti con una variabile avente lo stesso nome. Il nome di una variabile, infatti, non può essere passato a una direttiva del preprocessore e un simbolo può essere valutato solo da una direttiva del preprocessore.

L'ambito di un simbolo creato con `#define` è il file in cui è stato definito.

Il sistema di compilazione è anche a conoscenza dei simboli del preprocessore predefiniti che rappresentano [framework di destinazione](../../../standard/frameworks.md) diversi. Questi simboli sono utili durante la creazione di applicazioni destinata a più di un'implementazione o versione di .NET.

[!INCLUDE [Preprocessor symbols](~/includes/preprocessor-symbols.md)]

Altri simboli predefiniti includono le costanti DEBUG e TRACE. È possibile sostituire i valori impostati per il progetto con `#define`. Il simbolo DEBUG, ad esempio, viene impostato automaticamente a seconda delle proprietà di configurazione della build (modalità "Debug" o "Versione").

## <a name="examples"></a>Esempi

L'esempio seguente illustra come definire un simbolo MYTEST su un file e quindi testare i valori dei simboli MYTEST e DEBUG. L'output di questo esempio dipende dal fatto che il progetto sia stato compilato con la modalità di configurazione Debug o Versione.

```csharp
#define MYTEST
using System;
public class MyClass
{
    static void Main()
    {
#if (DEBUG && !MYTEST)
        Console.WriteLine("DEBUG is defined");
#elif (!DEBUG && MYTEST)
        Console.WriteLine("MYTEST is defined");
#elif (DEBUG && MYTEST)
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else
        Console.WriteLine("DEBUG and MYTEST are not defined");
#endif
    }
}
```

L'esempio seguente illustra come eseguire test per framework di destinazione diversi, in modo da poter usare le API più recenti quando possibile:

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        WebClient _client = new WebClient();
#else
        HttpClient _client = new HttpClient();
#endif
    }
    //...
}
```

## <a name="see-also"></a>Vedere anche

- [Riferimenti per C#](../../../csharp/language-reference/index.md)
- [Guida per programmatori C#](../../../csharp/programming-guide/index.md)
- [Direttive per il preprocessore C#](index.md)
- [Procedura: Compilare in modo condizionale con traccia e debug](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
