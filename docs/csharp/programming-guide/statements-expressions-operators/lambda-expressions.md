---
title: Espressioni lambda - Guida per programmatori C#
ms.custom: seodec18
ms.date: 03/14/2019
helpviewer_keywords:
- lambda expressions [C#]
- outer variables [C#]
- statement lambda [C#]
- expression lambda [C#]
- expressions [C#], lambda
ms.assetid: 57e3ba27-9a82-4067-aca7-5ca446b7bf93
ms.openlocfilehash: dd9b77a90030a96d17104c8c0e48964b6a85d165
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2019
ms.locfileid: "58125733"
---
# <a name="lambda-expressions-c-programming-guide"></a>Espressioni lambda (Guida per programmatori C#)

Un'*espressione lambda* è un blocco di codice costituito da espressioni o da istruzioni che viene trattato come oggetto. Tale blocco può essere passato come argomento ai metodi e può anche essere restituito dalle chiamate al metodo. Le espressioni lambda sono spesso usate per eseguire le attività seguenti:

- Passaggio del codice da eseguire a metodi asincroni, ad esempio <xref:System.Threading.Tasks.Task.Run(System.Action)?displayProperty=nameWithType>.

- Scrittura di [espressioni di query LINQ](../../linq/index.md).

- Creazione di [alberi delle espressioni](../concepts/expression-trees/index.md).

Le espressioni lambda sono codice che può essere rappresentato come delegato o come albero delle espressioni che viene compilato in un delegato. Il tipo di delegato specifico di un'espressione lambda dipende dai parametri dell'espressione e dal valore restituito. Le espressioni lambda che non restituiscono un valore corrispondano a un delegato `Action` specifico, che dipende dal relativo numero di parametri. Le espressioni lambda che restituiscono un valore corrispondano a un delegato `Func` specifico, che dipende dal relativo numero di parametri. Se ad esempio un'espressione lambda con due parametri non restituisce un valore, corrisponde a un delegato <xref:System.Action%602>. Se un'espressione lambda ha un parametro e restituisce un valore, corrisponde a un delegato <xref:System.Func%602>.

Un'espressione lambda usa `=>`, vale a dire l'[operatore di dichiarazione lambda](../../language-reference/operators/lambda-operator.md), per separare l'elenco di parametri dell'espressione lambda dal codice eseguibile. Per creare un'espressione lambda, specificare gli eventuali parametri di input a sinistra dell'operatore lambda e inserire il blocco di espressioni o di istruzioni dall'altra parte. Ad esempio, l'espressione lambda `x => x * x` a riga singola specifica un parametro denominato `x` e restituisce il valore di `x` al quadrato. È possibile assegnare questa espressione a un tipo di delegato, come illustrato nell'esempio riportato di seguito:

[!code-csharp-interactive[lambda is delegate](~/samples/snippets/csharp/programming-guide/lambda-expressions/Introduction.cs#Delegate)]

È anche possibile assegnare un'espressione lambda a un tipo di albero delle espressioni:

[!code-csharp-interactive[lambda is expression tree](~/samples/snippets/csharp/programming-guide/lambda-expressions/Introduction.cs#ExpressionTree)]

Oppure è possibile passarla direttamente come argomento del metodo:

[!code-csharp-interactive[lambda is argument](~/samples/snippets/csharp/programming-guide/lambda-expressions/Introduction.cs#Argument)]

Quando si usa la sintassi basata sul metodo per chiamare il metodo <xref:System.Linq.Enumerable.Select%2A?displayProperty=nameWithType> nella classe <xref:System.Linq.Enumerable?displayProperty=nameWithType>, come in LINQ to Objects e LINQ to XML, il parametro è un tipo delegato <xref:System.Func%602?displayProperty=nameWithType>. Un'espressione lambda è il modo più pratico per creare tale delegato. Quando si chiama il metodo <xref:System.Linq.Queryable.Select%2A?displayProperty=nameWithType> nella classe <xref:System.Linq.Queryable?displayProperty=nameWithType>, come in LINQ to SQL, il tipo di parametro è un tipo di albero delle espressioni [`Expression<Func<TSource,TResult>>`](<xref:System.Linq.Expressions.Expression%601>). Un'espressione lambda rappresenta quindi un modo rapido per costruire tale albero delle espressioni. Mediante le espressioni lambda, le chiamate `Select` risultano simili anche se in realtà il tipo di oggetto creato dall'espressione lambda è diverso.

Tutte le restrizioni che si applicano ai [metodi anonimi](anonymous-methods.md) si applicano anche alle espressioni lambda.
  
## <a name="expression-lambdas"></a>Espressioni lambda

Un'espressione lambda con un'espressione a destra dell'operatore `=>` è denominata *espressione lambda*. Queste espressioni vengono usate spesso nella costruzione di [alberi delle espressioni](../concepts/expression-trees/index.md). Un'espressione lambda dell'espressione restituisce il risultato dell'espressione e ha il formato di base seguente:

```csharp
(input-parameters) => expression
```

Le parentesi sono facoltative solo se l'espressione lambda ha un parametro di input; in caso contrario sono obbligatorie.

Specificare zero parametri di input con parentesi vuote:  

[!code-csharp[zero parameters](~/samples/snippets/csharp/programming-guide/lambda-expressions/ExpressionAndStatementLambdas.cs#ZeroParameters)]

Due o più parametri di input vengono separati da virgole e racchiusi tra parentesi:

[!code-csharp[two parameters](~/samples/snippets/csharp/programming-guide/lambda-expressions/ExpressionAndStatementLambdas.cs#TwoParameters)]

Talvolta è impossibile che il compilatore deduca i tipi di input. È possibile specificare i tipi in modo esplicito come illustrato nell'esempio seguente:

[!code-csharp[explicitly typed parameters](~/samples/snippets/csharp/programming-guide/lambda-expressions/ExpressionAndStatementLambdas.cs#ExplicitlyTypedParameters)]

I parametri di input devono essere tutti di tipo esplicito o tutti di tipo implicito. In caso contrario, si verifica un errore del compilatore [CS0748](../../misc/cs0748.md).

Il corpo di un'espressione lambda può essere costituito da una chiamata al metodo. Se tuttavia si creano alberi delle espressioni valutati al di fuori del contesto di Common Language Runtime di .NET Framework, ad esempio in SQL Server, non è consigliabile usare chiamate al metodo nelle espressioni lambda. I metodi non avranno alcun significato all'esterno del contesto di .NET Common Language Runtime.

## <a name="statement-lambdas"></a>Espressioni lambda dell'istruzione

Un'espressione lambda dell'istruzione è simile a un'espressione lambda dell'espressione con la differenza che l'istruzione o le istruzioni sono racchiuse tra parentesi graffe:

```csharp  
(input-parameters) => { statement; }
```

Il corpo di un'espressione lambda dell'istruzione può essere costituito da un numero qualsiasi di istruzioni, sebbene in pratica generalmente non ce ne siano più di due o tre.

[!code-csharp-interactive[statement lambda](~/samples/snippets/csharp/programming-guide/lambda-expressions/ExpressionAndStatementLambdas.cs#StatementLambda)]

Le espressioni lambda dell'istruzione, come i metodi anonimi, non possono essere utilizzate per creare alberi delle espressioni.
  
## <a name="async-lambdas"></a>Espressioni lambda asincrone

È facile creare istruzioni ed espressioni lambda che includono l'elaborazione asincrona utilizzando le parole chiave [async](../../language-reference/keywords/async.md) e [await](../../language-reference/keywords/await.md) . Nell'esempio seguente di Windows Form è presente un gestore eventi che chiama e attende un metodo asincrono, `ExampleMethodAsync`.

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
        button1.Click += button1_Click;
    }

    private async void button1_Click(object sender, EventArgs e)
    {
        await ExampleMethodAsync();
        textBox1.Text += "\r\nControl returned to Click event handler.\n";
    }

    private async Task ExampleMethodAsync()
    {
        // The following line simulates a task-returning asynchronous process.
        await Task.Delay(1000);
    }
}
```

È possibile aggiungere lo stesso gestore eventi utilizzando un'espressione lambda asincrona. Per aggiungere il gestore, aggiungere un modificatore `async` prima dell'elenco di parametri lambda, come illustrato di seguito:

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
        button1.Click += async (sender, e) =>
        {
            await ExampleMethodAsync();
            textBox1.Text += "\r\nControl returned to Click event handler.\n";
        };
    }

    private async Task ExampleMethodAsync()
    {
        // The following line simulates a task-returning asynchronous process.
        await Task.Delay(1000);
    }
}
```

Per altre informazioni su come creare e usare i metodi asincroni, vedere [Programmazione asincrona con async e await](../concepts/async/index.md).

## <a name="lambda-expressions-and-tuples"></a>Espressioni lambda e tuple

A partire da C# 7.0, il linguaggio C# offre supporto predefinito per le [tuple](../../tuples.md). È possibile specificare una tupla come argomento di un'espressione lambda e l'espressione lambda può restituire una tupla. In alcuni casi, il compilatore C# usa l'inferenza del tipo per determinare i tipi di componenti della tupla.

Per definire una tupla, è necessario racchiudere tra parentesi un elenco di componenti delimitato da virgole. L'esempio riportato sotto usa una tupla con tre componenti per passare una sequenza di numeri a un'espressione lambda, la quale raddoppia ogni valore e restituisce una tupla con tre componenti che contiene il risultato delle moltiplicazioni.

[!code-csharp-interactive[lambda and tuples](~/samples/snippets/csharp/programming-guide/lambda-expressions/LambdasAndTuples.cs#WithoutComponentName)]

In genere, i campi di una tupla sono denominati `Item1`, `Item2` e così via. È possibile tuttavia definire una tupla usando i componenti denominati, come illustra l'esempio seguente.

[!code-csharp-interactive[lambda and named tuples](~/samples/snippets/csharp/programming-guide/lambda-expressions/LambdasAndTuples.cs#WithComponentName)]

Per altre informazioni sulle tuple in C#, vedere [Tipi tupla in C#](../../tuples.md).

## <a name="lambdas-with-the-standard-query-operators"></a>Espressioni lambda con operatori query standard

LINQ to Objects, tra altre implementazioni, ha un parametro di input il cui tipo appartiene alla famiglia <xref:System.Func%601> di delegati generici. Questi delegati usano parametri di tipo per definire il numero e il tipo di parametri di input e il tipo restituito del delegato. I delegati`Func` sono molto utili per incapsulare le espressioni definite dall'utente applicate a ogni elemento in un set di dati di origine. Considerare ad esempio il tipo delegato <xref:System.Func%602>:  

```csharp
public delegate TResult Func<in T, out TResult>(T arg)
```

È possibile creare un'istanza `Func<int, bool>` del delegato, dove `int` è un parametro di input e `bool` è il valore restituito. Il valore restituito è sempre specificato nell'ultimo parametro di tipo. `Func<int, string, bool>`, ad esempio, definisce un delegato con due parametri di input, `int` e `string`, e un tipo restituito `bool`. Quando viene richiamato, il delegato `Func` seguente restituisce il valore booleano indicante se il parametro di input è uguale a cinque:

[!code-csharp-interactive[Func example](~/samples/snippets/csharp/programming-guide/lambda-expressions/LambdasWithQueryMethods.cs#Func)]

È anche possibile specificare un'espressione lambda quando il tipo di argomento è <xref:System.Linq.Expressions.Expression%601>, ad esempio negli operatori query standard definiti nel tipo <xref:System.Linq.Queryable>. Quando si specifica un argomento <xref:System.Linq.Expressions.Expression%601>, l'espressione lambda viene compilata per un albero delle espressioni.
  
L'esempio seguente usa l'operatore query standard <xref:System.Linq.Enumerable.Count%2A>:

[!code-csharp-interactive[Count example](~/samples/snippets/csharp/programming-guide/lambda-expressions/LambdasWithQueryMethods.cs#Count)]

Il compilatore è in grado di dedurre il tipo del parametro di input oppure è possibile specificarlo in modo esplicito. Questa espressione lambda particolare conta i numeri interi (`n`) che divisi per due danno il resto di 1.

L'esempio seguente crea una sequenza contenente tutti gli elementi presenti nella matrice `numbers` che si trovano a sinistra di 9, vale a dire il primo numero della sequenza che non soddisfa la condizione:

[!code-csharp-interactive[TakeWhile example](~/samples/snippets/csharp/programming-guide/lambda-expressions/LambdasWithQueryMethods.cs#TakeWhile)]

In questo esempio viene illustrato come specificare più parametri di input racchiudendoli tra parentesi. Il metodo restituisce tutti gli elementi presenti nella matrice `numbers` finché non viene rilevato un numero il cui valore è inferiore alla relativa posizione all'interno della matrice:

[!code-csharp-interactive[TakeWhile example 2](~/samples/snippets/csharp/programming-guide/lambda-expressions/LambdasWithQueryMethods.cs#TakeWhileWithIndex)]

## <a name="type-inference-in-lambda-expressions"></a>Inferenza del tipo nelle espressioni lambda

Quando si scrivono espressioni lambda, spesso non occorre specificare un tipo per i parametri di input, perché il compilatore può dedurlo in base al corpo dell'espressione lambda, ai tipi di parametro e ad altri fattori, come descritto nelle specifiche del linguaggio C#. Per la maggior parte degli operatori di query standard, il primo input è il tipo degli elementi nella sequenza di origine. Pertanto, se si esegue una query su un oggetto `IEnumerable<Customer>`, si deduce che la variabile di input sia un oggetto `Customer`, ovvero che si dispone dell'accesso ai relativi metodi e proprietà:  

```csharp
customers.Where(c => c.City == "London");
```

Di seguito sono riportate le regole generali per l'inferenza del tipo nelle espressioni lambda:

- L'espressione lambda deve contenere lo stesso numero di parametri del tipo delegato.

- Ogni parametro di input nell'espressione lambda deve essere convertibile in modo implicito nel parametro del delegato corrispondente.

- Il valore restituito dell'espressione lambda, se presente, deve essere convertibile in modo implicito nel tipo restituito del delegato.
  
Si noti che le espressioni lambda non hanno un tipo perché Common Type System non ha alcun concetto intrinseco di "espressione lambda". In alcuni casi, tuttavia, può essere utile fare riferimento in modo informale al "tipo" di un'espressione lambda. In questi casi, per tipo si intende il tipo delegato o il tipo <xref:System.Linq.Expressions.Expression> in cui viene convertita l'espressione lambda.

## <a name="variable-scope-in-lambda-expressions"></a>Ambito delle variabili nelle espressioni lambda

Le espressioni lambda possono fare riferimento alle *variabili esterne* (vedere [Metodi anonimi](anonymous-methods.md)) presenti nell'ambito del metodo che definisce l'espressione lambda oppure nell'ambito del tipo che contiene l'espressione lambda. Le variabili acquisite in questo modo vengono archiviate per poter essere utilizzate nell'espressione lambda anche se le variabili diventano esterne all'ambito e vengono sottoposte a Garbage Collection. Una variabile esterna deve essere assegnata prima di poter essere utilizzata in un'espressione lambda. Nell'esempio seguente vengono illustrate queste regole:

[!code-csharp[variable scope](~/samples/snippets/csharp/programming-guide/lambda-expressions/VariableScopeWithLambdas.cs#VariableScope)]

Le regole seguenti si applicano all'ambito delle variabili nelle espressioni lambda:  

- Una variabile acquisita non sarà sottoposta a Garbage Collection finché il delegato a cui fa riferimento non diventa idoneo per il Garbage Collection.

- Le variabili introdotte in un'espressione lambda non sono visibili nel metodo contenitore.

- Un'espressione lambda non può acquisire direttamente un parametro [in](../../language-reference/keywords/in-parameter-modifier.md), [ref](../../language-reference/keywords/ref.md) o [out](../../language-reference/keywords/out-parameter-modifier.md) dal metodo contenitore.

- Un'istruzione [return](../../language-reference/keywords/return.md) in un'espressione lambda non causa la restituzione del metodo contenitore.

- Un'espressione lambda non può contenere un'istruzione [goto](../../language-reference/keywords/goto.md), [break](../../language-reference/keywords/break.md) o [continue](../../language-reference/keywords/continue.md) se la destinazione di tale istruzione di salto è esterna al blocco dell'espressione lambda. È anche errato inserire all'esterno del blocco dell'espressione lambda un'istruzione di salto se la destinazione è interna al blocco.

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

Per altre informazioni, vedere la sezione [Espressioni di funzioni anonime](~/_csharplang/spec/expressions.md#anonymous-function-expressions) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).

## <a name="featured-book-chapter"></a>Capitoli del libro rappresentati

[Delegates, Events, and Lambda Expressions](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518994%28v=orm.10%29) (Delegati, eventi ed espressioni Lambda) in [C# 3.0 Cookbook, Third Edition: More than 250 solutions for C# 3.0 programmers](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff518995%28v=orm.10%29) (Tutto su C# 3.0, terza edizione: più di 250 soluzioni per i programmatori C# 3.0)  
  
## <a name="see-also"></a>Vedere anche

- [Guida per programmatori C#](../index.md)
- [LINQ (Language-Integrated Query)](../concepts/linq/index.md)
- [Metodi anonimi](anonymous-methods.md)
- [Alberi delle espressioni](../concepts/expression-trees/index.md)
- [Confronto tra funzioni locali ed espressioni lambda](../../local-functions-vs-lambdas.md)
- [Espressioni lambda tipizzate in modo implicito](../../implicitly-typed-lambda-expressions.md)
- [Esempi C# di Visual Studio 2008 (vedere i file di query di esempio LINQ e il programma XQuery)](https://code.msdn.microsoft.com/Visual-Studio-2008-C-d295cdba)
- [Recursive lambda expressions (Espressioni lambda ricorsive)](https://blogs.msdn.microsoft.com/madst/2007/05/11/recursive-lambda-expressions/)
