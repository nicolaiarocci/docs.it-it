---
title: Expressions1
ms.date: 03/30/2017
ms.assetid: c42341a9-43a1-462c-bffb-c5de004aa428
ms.openlocfilehash: 7643279c2db5608c028e0a1213802ab609a2d347
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704284"
---
# <a name="expressions"></a>Espressioni
Un'espressione di Windows Workflow Foundation (WF) è un'attività che restituisce un risultato. Tutte le attività di espressione derivano indirettamente da <xref:System.Activities.Activity%601>, che contiene una proprietà <xref:System.Activities.OutArgument> che viene denominata <xref:System.Activities.Activity%601.Result%2A> quando l'attività restituisce un valore. [!INCLUDE[wf1](../../../includes/wf1-md.md)] viene fornito con un'ampia gamma di attività di espressione, da quelle semplici come <xref:System.Activities.Expressions.VariableValue%601> e <xref:System.Activities.Expressions.VariableReference%601>, che consentono di accedere a variabili del flusso di lavoro attraverso attività dell'operatore, a quelle complesse come <xref:Microsoft.VisualBasic.Activities.VisualBasicReference%601> e <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> che, per produrre il risultato, offrono l'accesso all'intera gamma di funzionalità del linguaggio Visual Basic. È possibile creare attività di espressione aggiuntive derivando dall'oggetto <xref:System.Activities.CodeActivity%601> o <xref:System.Activities.NativeActivity%601>.  
  
## <a name="using-expressions"></a>Uso di espressioni  
 Progettazione flussi di lavoro usa <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> e <xref:Microsoft.VisualBasic.Activities.VisualBasicReference%601> per tutte le espressioni nei progetti Visual Basic e <xref:Microsoft.CSharp.Activities.CSharpValue%601> e <xref:Microsoft.CSharp.Activities.CSharpReference%601> per le espressioni nei progetti flusso di lavoro C#  
  
> [!NOTE]
>  Il supporto per le espressioni C# nei progetti flusso di lavoro è stato introdotto in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]. Per altre informazioni, vedere [ C# espressioni](csharp-expressions.md).  
  
 I flussi di lavoro prodotti dalla finestra di progettazione vengono salvati nel codice XAML, in cui le espressioni sono incluse tra parentesi quadre, come nell'esempio seguente.  
  
```xml  
<Sequence xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <Variable x:TypeArguments="x:Int32" Default="1" Name="a" />  
    <Variable x:TypeArguments="x:Int32" Default="2" Name="b" />  
    <Variable x:TypeArguments="x:Int32" Default="3" Name="c" />  
    <Variable x:TypeArguments="x:Int32" Default="0" Name="r" />  
  </Sequence.Variables>  
  <Assign>  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:Int32">[r]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:Int32">[a + b + c]</InArgument>  
    </Assign.Value>  
  </Assign>  
</Sequence>  
```  
  
 Quando si definisce un flusso di lavoro nel codice, è possibile usare qualsiasi attività di espressione. Nell'esempio seguente viene mostrato l'uso di una composizione di attività dell'operatore per aggiungere tre numeri.  
  
```  
Variable<int> a = new Variable<int>("a", 1);  
Variable<int> b = new Variable<int>("b", 2);  
Variable<int> c = new Variable<int>("c", 3);  
Variable<int> r = new Variable<int>("r", 0);  
  
Sequence w = new Sequence  
{  
    Variables = { a, b, c, r },  
    Activities =   
    {  
        new Assign {  
            To = new OutArgument<int>(r),  
            Value = new InArgument<int> {  
                Expression = new Add<int, int, int> {  
                    Left = new Add<int, int, int> {  
                        Left = new InArgument<int>(a),  
                        Right = new InArgument<int>(b)  
                    },  
                    Right = new InArgument<int>(c)  
                }  
            }  
        }  
    }  
};  
```  
  
 Lo stesso flusso di lavoro può essere espresso in modo più compatto usando le espressioni lambda di C#, come mostrato nell'esempio seguente.  
  
```  
Variable<int> a = new Variable<int>("a", 1);  
Variable<int> b = new Variable<int>("b", 2);  
Variable<int> c = new Variable<int>("c", 3);  
Variable<int> r = new Variable<int>("r", 0);  
  
Sequence w = new Sequence  
{  
    Variables = { a, b, c, r },  
    Activities =   
    {  
        new Assign {  
            To = new OutArgument<int>(r),  
            Value = new InArgument<int>((ctx) => a.Get(ctx) + b.Get(ctx) + c.Get(ctx))  
        }  
    }  
};  
```  
  
 Il flusso di lavoro può essere espresso anche usando le espressioni di attività di Visual Basic, come mostrato nell'esempio seguente.  
  
```  
Variable<int> a = new Variable<int>("a", 1);  
Variable<int> b = new Variable<int>("b", 2);  
Variable<int> c = new Variable<int>("c", 3);  
Variable<int> r = new Variable<int>("r", 0);  
  
Sequence w = new Sequence  
{  
    Variables = { a, b, c, r },  
    Activities =   
    {  
        new Assign {  
            To = new OutArgument<int>(r),  
            Value = new InArgument<int>(new VisualBasicValue<int>("a + b + c"))  
        }  
    }  
};  
```  
  
## <a name="extending-available-expressions-with-custom-expression-activities"></a>Estensione di espressioni disponibili con attività di espressione personalizzate  
 Le espressioni in [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] possono essere estese consentendo la creazione di attività di espressione aggiuntive. Nell'esempio seguente viene mostrata un'attività che restituisce una somma di tre valori Integer.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Activities;  
  
namespace ExpressionsDemo  
{  
    public sealed class AddThreeValues : CodeActivity<int>  
    {  
        public InArgument<int> Value1 { get; set; }  
        public InArgument<int> Value2 { get; set; }  
        public InArgument<int> Value3 { get; set; }  
  
        protected override int Execute(CodeActivityContext context)  
        {  
            return Value1.Get(context) +   
                   Value2.Get(context) +   
                   Value3.Get(context);  
        }  
    }  
}  
```  
  
 Con questa nuova attività è possibile riscrivere il flusso di lavoro precedente che ha aggiunto tre valori come mostrato nell'esempio seguente.  
  
```  
Variable<int> a = new Variable<int>("a", 1);  
Variable<int> b = new Variable<int>("b", 2);  
Variable<int> c = new Variable<int>("c", 3);  
Variable<int> r = new Variable<int>("r", 0);  
  
Sequence w = new Sequence  
{  
    Variables = { a, b, c, r },  
    Activities =   
    {  
        new Assign {  
            To = new OutArgument<int>(r),  
            Value = new InArgument<int> {  
                Expression = new AddThreeValues() {  
                    Value1 = new InArgument<int>(a),  
                    Value2 = new InArgument<int>(b),  
                    Value3 = new InArgument<int>(c)  
                }  
            }  
        }  
    }  
};  
```  
  
 Per altre informazioni sull'utilizzo delle espressioni nel codice, vedere [creazione di flussi di lavoro, attività e le espressioni tramite codice imperativo](authoring-workflows-activities-and-expressions-using-imperative-code.md).
