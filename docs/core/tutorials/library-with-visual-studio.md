---
title: Compilare una libreria .NET Standard in C# con Visual Studio 2017
description: Informazioni su come creare una libreria di classi .NET Standard scritta in C# usando Visual Studio 2017.
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: 6228cd93b275a059da63a8b8e3408032d78c5e39
ms.sourcegitcommit: 542aa405b295955eb055765f33723cb8b588d0d0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54362015"
---
# <a name="build-a-net-standard-library-with-c-and-the-net-core-sdk-in-visual-studio-2017"></a>Compilare una libreria .NET Standard con C# e .NET Core SDK in Visual Studio 2017

La *libreria di classi* definisce tipi e metodi chiamati da un'applicazione. Una libreria di classi che esegue la destinazione a .NET Standard 2.0 consente la chiamata alla libreria da qualsiasi implementazione di .NET che supporti questa versione di .NET Standard. Dopo aver completato la libreria di classi, è possibile decidere se si vuole distribuirla come componente di terze parti o se si vuole includerla come componente in bundle con una o più applicazioni.

> [!NOTE]
> Per un elenco delle versioni di .NET Standard e delle piattaforme supportate, vedere [.NET Standard](../../standard/net-standard.md).

In questo argomento si creerà una semplice libreria di utilità contenente un solo metodo di gestione delle stringhe, che verrà implementato come [metodo di estensione](../../csharp/programming-guide/classes-and-structs/extension-methods.md), in modo da poter essere chiamato come se fosse un membro della classe <xref:System.String>.

## <a name="creating-a-class-library-solution"></a>Creazione di una soluzione per la libreria di classi

Iniziare creando una soluzione per il progetto di libreria di classi e per i progetti correlati. Una soluzione Visual Studio funge solo da contenitore per uno o più progetti. Per creare la soluzione:

1. Nella barra dei menu di Visual Studio scegliere **File** > **Nuovo** > **Progetto**.

1. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Altri tipi di progetti** e selezionare **Soluzioni di Visual Studio**. Assegnare alla soluzione il nome "ClassLibraryProjects" e selezionare il pulsante **OK**.

   ![Finestra di dialogo Nuovo progetto con la nuova soluzione vuota evidenziata](./media/library-with-visual-studio/new-project-dialog.png)

## <a name="creating-the-class-library-project"></a>Creazione del progetto di libreria di classi

Creare un progetto di libreria di classi:

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file della soluzione **ClassLibraryProjects** e dal menu di scelta rapida selezionare **Aggiungi** > **Nuovo progetto**.

1. Nella finestra di dialogo **Aggiungi nuovo progetto** espandere il nodo **Visual C#**, quindi selezionare il nodo **.NET Standard** seguito dal modello di progetto **Libreria di classi (.NET Standard)**. Nella casella di testo **Nome** immettere "StringLibrary" come nome del progetto. Scegliere **OK** per creare il progetto di libreria di classi.

   ![Finestra di dialogo Aggiungi nuovo progetto per libreria di classi](./media/library-with-visual-studio/add-new-library-project.png)

   La finestra di codice viene quindi aperta nell'ambiente di sviluppo di Visual Studio.

   ![Finestra dell'applicazione di Visual Studio che illustra il codice del modello della libreria di classi predefinito](./media/library-with-visual-studio/string-library-project.png)

1. Assicurarsi che sia stata eseguita la destinazione della libreria alla versione corretta di .NET Standard. Fare clic con il pulsante destro del mouse sul progetto libreria nelle finestre di **Esplora soluzioni**, quindi selezionare **Proprietà**. La casella di testo **Framework di destinazione** indica che si sta eseguendo la destinazione a .NET 2.0 Standard.

   ![Proprietà del progetto per la libreria di classi](./media/library-with-visual-studio/library-project-properties.png)

1. Nella finestra del codice sostituire il codice con il seguente:

   [!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs)]

   La libreria di classi `UtilityLibraries.StringLibrary` contiene un metodo denominato `StartsWithUpper`, che restituisce un valore <xref:System.Boolean> che indica se l'istanza della stringa corrente inizia con un carattere maiuscolo. Lo standard Unicode distingue i caratteri maiuscoli dai minuscoli. Il metodo <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> restituisce `true` se un carattere è maiuscolo.

1. Nella barra dei menu selezionare **Compila** > **Compila soluzione**. Il progetto dovrebbe essere compilato senza errori.

   ![Riquadro di output che illustra che la compilazione ha avuto esito positivo](./media/library-with-visual-studio/output-pane-successful-build.png)

## <a name="next-step"></a>Passaggio successivo

La compilazione della libreria è stata completata. Non è tuttavia possibile sapere se funziona come previsto poiché non è stato ancora chiamato uno dei metodi. Il passaggio successivo per lo sviluppo della libreria consiste nel testarla usando un [Progetto unit test](testing-library-with-visual-studio.md).