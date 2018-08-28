---
title: 'Installazione di F #'
description: 'Informazioni su come installare F # nel proprio ambiente.'
ms.date: 07/03/2018
ms.openlocfilehash: 142265a95e1d3ee1603a89f650a24c6a45709181
ms.sourcegitcommit: 59b51cd7c95c75be85bd6ef715e9ef8c85720bac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2018
ms.locfileid: "37878846"
---
# <a name="install-f"></a>Installazione di F # #

È possibile installare F # in diversi modi, a seconda dell'ambiente.

## <a name="install-f-with-visual-studio"></a>Installare F # con Visual Studio

Se si sta scaricando [Visual Studio](https://visualstudio.microsoft.com/) per la prima volta, verranno installati prima il programma di installazione di Visual Studio. Installare l'appropriato dello SKU di Visual Studio dal programma di installazione. Se già installato, fare clic su **Modify**.

Successivamente, si verrà visualizzato un elenco dei carichi di lavoro. Selezionare **sviluppo ASP.NET e web**, che installerà supporto per F #, supporto per .NET Core, e i progetti F # supporto per ASP.NET Core.

Fare quindi clic **Modify** nel lato inferiore destro.  Verranno installati tutti gli elementi selezionati. È quindi possibile aprire Visual Studio 2017 con supporto del linguaggio F # facendo **avviare**.

## <a name="install-f-with-visual-studio-for-mac"></a>Installare F # con Visual Studio per Mac

F # è installato per impostazione predefinita in [Visual Studio per Mac](https://visualstudio.microsoft.com/vs/mac/), indipendentemente dal quale configurazione scelto.

Al termine dell'installazione, scegliere "Avvia Visual Studio". È anche possibile avviarla tramite Finder in macOS.

## <a name="install-f-with-visual-studio-code"></a>Installare F # con Visual Studio Code

È necessario disporre [git installato](https://git-scm.com/download) ed è disponibile nel percorso desiderato per rendere utilizzare modelli di progetto in Ionide. È possibile verificare che sia installato correttamente, digitando `git --version` in un prompt dei comandi e premendo **invio**.

### <a name="macostabmacos"></a>[macOS](#tab/macos)

Usa Ionide [Mono](http://www.mono-project.com). Il modo più semplice per installare Mono in macOS è tramite Homebrew. È sufficiente digitare quanto segue nel terminale:

```console
brew install mono
```

È inoltre necessario installare il [.NET Core SDK](https://www.microsoft.com/net/download).

### <a name="linuxtablinux"></a>[Linux](#tab/linux)

In Linux, viene utilizzato anche Ionide [Mono](https://www.mono-project.com). Se si usa Ubuntu o Debian, è possibile usare quanto segue:

```console
sudo apt-get update
sudo apt-get install mono-complete fsharp
```

È inoltre necessario installare il [.NET Core SDK](https://www.microsoft.com/net/download).

### <a name="windowstabwindows"></a>[Windows](#tab/windows)

Se si usa Windows, è necessario [installazione di Visual Studio con il supporto per F #](#install-f-with-visual-studio). Ciò consente di installare tutti i componenti necessari per scrivere, compilare ed eseguire codice F #.

È inoltre necessario installare il [.NET Core SDK](https://www.microsoft.com/net/download/).

---

Sarà quindi necessario [Visual Studio Code](https://code.visualstudio.com) installato.

Successivamente, fare clic sull'icona delle estensioni e cercare "Ionide":

Il plug-in unico necessaria per il supporto di F # in Visual Studio Code [Ionide-fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp). Tuttavia, è anche possibile installare [Ionide FAKE](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-FAKE) per ottenere [FAKE](https://fsharp.github.io/FAKE/) supportano e [Ionide Paket](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-Paket) ottenere [Paket](https://fsprojects.github.io/Paket/) supportano. SIMULARE e Paket sono aggiuntive degli strumenti della community F # per la compilazione di progetti e la gestione delle dipendenze, rispettivamente.