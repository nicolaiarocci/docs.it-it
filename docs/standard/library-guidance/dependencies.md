---
title: Dipendenze e librerie .NET
description: Procedure consigliate per la gestione delle dipendenze NuGet nelle librerie .NET.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: c5df30c606e77c9ef44387233b0072ab890f612f
ms.sourcegitcommit: e42d09e5966dd9fd02847d3e7eeb4ec0877069f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2018
ms.locfileid: "49400551"
---
# <a name="dependencies"></a><span data-ttu-id="15295-103">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="15295-103">Dependencies</span></span>

<span data-ttu-id="15295-104">Il modo principale per aggiungere dipendenze a una libreria .NET consiste nel fare riferimento ai pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="15295-104">The primary way of adding dependencies to a .NET library is referencing NuGet packages.</span></span> <span data-ttu-id="15295-105">I riferimenti ai pacchetti NuGet consentono di riutilizzare rapidamente e di sfruttare le funzionalità già scritte, ma possono causare problemi per gli sviluppatori .NET.</span><span class="sxs-lookup"><span data-stu-id="15295-105">NuGet package references allow you to quickly reuse and leverage already written functionality, but they're a common source of friction for .NET developers.</span></span> <span data-ttu-id="15295-106">La corretta gestione delle dipendenze è importante per evitare che le modifiche apportate in altre librerie .NET impediscano il funzionamento della libreria .NET in uso e viceversa.</span><span class="sxs-lookup"><span data-stu-id="15295-106">Correctly managing dependencies is important to prevent changes in other .NET libraries from breaking your .NET library, and vice versa!</span></span>

## <a name="diamond-dependencies"></a><span data-ttu-id="15295-107">Dipendenze a rombo</span><span class="sxs-lookup"><span data-stu-id="15295-107">Diamond dependencies</span></span>

<span data-ttu-id="15295-108">In un progetto .NET è comune la presenza di più versioni di un pacchetto nel relativo albero delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="15295-108">It's a common situation for a .NET project to have multiple versions of a package in its dependency tree.</span></span> <span data-ttu-id="15295-109">Ad esempio, un'app dipende da due pacchetti NuGet, ognuno dei quali dipende da versioni diverse dello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="15295-109">For example, an app depends on two NuGet packages, each of which depends on different versions of the same package.</span></span> <span data-ttu-id="15295-110">Nel grafo delle dipendenze dell'app è ora presente una dipendenza a rombo.</span><span class="sxs-lookup"><span data-stu-id="15295-110">A diamond dependency now exists in the app's dependency graph.</span></span>

<span data-ttu-id="15295-111">![Dipendenza a rombo](./media/dependencies/diamond-dependency.png "Dipendenza a rombo")</span><span class="sxs-lookup"><span data-stu-id="15295-111">![Diamond dependency](./media/dependencies/diamond-dependency.png "Diamond dependency")</span></span>

<span data-ttu-id="15295-112">In fase di compilazione NuGet analizza tutti i pacchetti da cui un progetto dipende, incluse le dipendenze delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="15295-112">At build time, NuGet analyzes all the packages that a project depends on, including the dependencies of dependencies.</span></span> <span data-ttu-id="15295-113">Quando vengono rilevate più versioni di un pacchetto, vengono valutate le regole per scegliere un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="15295-113">When multiple versions of a package are detected, rules are evaluated to pick one.</span></span> <span data-ttu-id="15295-114">È necessario unificare i pacchetti perché l'esecuzione affiancata di versioni diverse di un assembly nella stessa applicazione è problematica in .NET.</span><span class="sxs-lookup"><span data-stu-id="15295-114">Unifying packages is necessary because running side-by-side versions of an assembly in the same application is problematic in .NET.</span></span>

<span data-ttu-id="15295-115">La maggior parte delle dipendenze a rombo può essere risolta facilmente, tuttavia in alcune circostanze è possibile che si verifichino problemi:</span><span class="sxs-lookup"><span data-stu-id="15295-115">Most diamond dependencies are easily resolved; however, they can create issues in certain circumstances:</span></span>

1. <span data-ttu-id="15295-116">I **riferimenti ai pacchetti NuGet in conflitto** impediscono la risoluzione di una versione durante il ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="15295-116">**Conflicting NuGet package references** prevent a version from being resolved during package restore.</span></span>
2. <span data-ttu-id="15295-117">Le **modifiche tra versioni che causano un'interruzione** provocano bug ed eccezioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="15295-117">**Breaking changes between the versions** cause bugs and exceptions at runtime.</span></span>
3. <span data-ttu-id="15295-118">L'**assembly del pacchetto ha un nome sicuro**, la versione dell'assembly è stata modificata e l'app è in esecuzione in .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="15295-118">**The package assembly is strong named**, the assembly version changed, and the app is running on the .NET Framework.</span></span> <span data-ttu-id="15295-119">Sono richiesti reindirizzamenti di binding dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="15295-119">Assembly binding redirects are required.</span></span>

<span data-ttu-id="15295-120">Non è possibile sapere quali pacchetti verranno usati insieme ai propri.</span><span class="sxs-lookup"><span data-stu-id="15295-120">It's not possible to know what packages will be used alongside your own.</span></span> <span data-ttu-id="15295-121">Un buon metodo per ridurre le probabilità che una dipendenza a rombo provochi il malfunzionamento della libreria consiste nel ridurre al minimo il numero di pacchetti da cui la libreria dipende.</span><span class="sxs-lookup"><span data-stu-id="15295-121">A good way to reduce the likelihood of a diamond dependency breaking your library is to minimize the number of packages you depend on.</span></span>

<span data-ttu-id="15295-122">**✔️ ESAMINARE** la libreria .NET per individuare eventuali dipendenze non necessarie.</span><span class="sxs-lookup"><span data-stu-id="15295-122">**✔️ DO** review your .NET library for unnecessary dependencies.</span></span>

## <a name="nuget-dependency-version-ranges"></a><span data-ttu-id="15295-123">Intervalli di versione delle dipendenze NuGet</span><span class="sxs-lookup"><span data-stu-id="15295-123">NuGet dependency version ranges</span></span>

<span data-ttu-id="15295-124">Un riferimento a un pacchetto specifica l'intervallo di pacchetti validi consentiti.</span><span class="sxs-lookup"><span data-stu-id="15295-124">A package reference specifies the range of valid packages it allows.</span></span> <span data-ttu-id="15295-125">In genere, la versione di riferimento del pacchetto nel file di progetto è la versione minima e non è previsto alcun limite massimo.</span><span class="sxs-lookup"><span data-stu-id="15295-125">Typically, the package reference version in the project file is the minimum version and there's no maximum.</span></span>

```xml
<!-- Accepts any version 1.0 and above. -->
<PackageReference Include="ExamplePackage" Version="1.0" />
```

<span data-ttu-id="15295-126">Le regole usate da NuGet per la risoluzione delle dipendenze sono [complesse](/nuget/consume-packages/dependency-resolution), ma NuGet cerca sempre la versione più bassa applicabile.</span><span class="sxs-lookup"><span data-stu-id="15295-126">The rules that NuGet uses when resolving dependencies are [complex](/nuget/consume-packages/dependency-resolution), but NuGet always looks for the lowest applicable version.</span></span> <span data-ttu-id="15295-127">NuGet privilegia la versione più bassa applicabile rispetto all'uso della versione più alta disponibile perché la più bassa presenta meno problemi di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="15295-127">NuGet prefers the lowest applicable version over using the highest available because the lowest will have the least compatibility issues.</span></span>

<span data-ttu-id="15295-128">A causa della regola di ricerca della versione più bassa applicabile da parte di NuGet, non è necessario inserire una versione superiore o un intervallo esatto nei riferimenti ai pacchetti per evitare di ottenere la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="15295-128">Because of NuGet's lowest applicable version rule, it isn't necessary to place an upper version or exact range on package references to avoid getting the latest version.</span></span> <span data-ttu-id="15295-129">NuGet cerca già di trovare la versione più bassa e più compatibile.</span><span class="sxs-lookup"><span data-stu-id="15295-129">NuGet already tries to find the lowest, most compatible version for you.</span></span>

```xml
<!-- Accepts 1.0 up to 1.x, but not 2.0 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.0,2.0)" />

<!-- Accepts exactly 1.0. -->
<PackageReference Include="ExamplePackage" Version="[1.0]" />
```

<span data-ttu-id="15295-130">I limiti superiori per la versione provocano un errore di NuGet in caso di conflitto.</span><span class="sxs-lookup"><span data-stu-id="15295-130">Upper version limits will cause NuGet to fail if there's a conflict.</span></span> <span data-ttu-id="15295-131">Ad esempio, una libreria accetta esattamente la versione 1.0, mentre un'altra libreria richiede la versione 2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="15295-131">For example, one library accepts exactly 1.0 while another library requires 2.0 or above.</span></span> <span data-ttu-id="15295-132">Sebbene nella versione 2.0 potrebbero essere state introdotte modifiche che causano un'interruzione, una dipendenza di versione rigida o con un limite superiore garantisce la generazione di un errore.</span><span class="sxs-lookup"><span data-stu-id="15295-132">While breaking changes may have been introduced in version 2.0, a strict or upper limit version dependency guarantees an error.</span></span>

<span data-ttu-id="15295-133">![Conflitto di dipendenza a rombo](./media/dependencies/diamond-dependency-conflict.png "Conflitto di dipendenza a rombo")</span><span class="sxs-lookup"><span data-stu-id="15295-133">![Diamond dependency conflict](./media/dependencies/diamond-dependency-conflict.png "Diamond dependency conflict")</span></span>

<span data-ttu-id="15295-134">**❌ NON** creare riferimenti a pacchetti NuGet senza una versione minima.</span><span class="sxs-lookup"><span data-stu-id="15295-134">**❌ DO NOT** have NuGet package references with no minimum version.</span></span>

<span data-ttu-id="15295-135">**❌ EVITARE** riferimenti ai pacchetti NuGet che richiedono una versione esatta.</span><span class="sxs-lookup"><span data-stu-id="15295-135">**❌ AVOID** NuGet package references that demand an exact version.</span></span>

<span data-ttu-id="15295-136">**❌ EVITARE** riferimenti ai pacchetti NuGet con un limite superiore di versione.</span><span class="sxs-lookup"><span data-stu-id="15295-136">**❌ AVOID** NuGet package references with a version upper limit.</span></span>

## <a name="nuget-shared-source-packages"></a><span data-ttu-id="15295-137">Pacchetti di codice sorgente condiviso NuGet</span><span class="sxs-lookup"><span data-stu-id="15295-137">NuGet shared source packages</span></span>

<span data-ttu-id="15295-138">Un modo per ridurre le dipendenze esterne dei pacchetti NuGet consiste nel fare riferimento a pacchetti di codice sorgente condiviso.</span><span class="sxs-lookup"><span data-stu-id="15295-138">One way to reduce external NuGet package dependencies is to reference shared source packages.</span></span> <span data-ttu-id="15295-139">Un pacchetto di codice sorgente condiviso contiene [file di codice sorgente](/nuget/reference/nuspec#including-content-files) che vengono inclusi in un progetto quando vi viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="15295-139">A shared source package contains [source code files](/nuget/reference/nuspec#including-content-files) that are included in a project when referenced.</span></span> <span data-ttu-id="15295-140">Perché vengono inclusi solo i file di codice sorgente compilati con il resto del progetto, non c'è alcuna dipendenza esterna e di conseguenza non c'è possibilità di conflitto.</span><span class="sxs-lookup"><span data-stu-id="15295-140">Because you're just including source code files that are compiled with the rest of your project, there's no external dependency and chance of conflict.</span></span>

<span data-ttu-id="15295-141">I pacchetti di codice sorgente condiviso sono ideali per includere funzionalità di piccola entità.</span><span class="sxs-lookup"><span data-stu-id="15295-141">Shared source packages are great for including small pieces of functionality.</span></span> <span data-ttu-id="15295-142">Ad esempio, un pacchetto di codice sorgente condiviso di metodi helper per l'esecuzione di chiamate HTTP.</span><span class="sxs-lookup"><span data-stu-id="15295-142">For example, a shared source package of helper methods for making HTTP calls.</span></span>

<span data-ttu-id="15295-143">![Pacchetto di codice sorgente condiviso](./media/dependencies/shared-source-package.png "Pacchetto di codice sorgente condiviso")</span><span class="sxs-lookup"><span data-stu-id="15295-143">![Shared source package](./media/dependencies/shared-source-package.png "Shared source package")</span></span>

```xml
<PackageReference Include="Microsoft.Extensions.Buffers.Testing.Sources" PrivateAssets="All" Version="1.0" />
```

<span data-ttu-id="15295-144">![Progetto di codice sorgente condiviso](./media/dependencies/shared-source-project.png "Progetto di codice sorgente condiviso")</span><span class="sxs-lookup"><span data-stu-id="15295-144">![Shared source project](./media/dependencies/shared-source-project.png "Shared source project")</span></span>

<span data-ttu-id="15295-145">I pacchetti di codice sorgente condiviso presentano alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="15295-145">Shared source packages have some limitations.</span></span> <span data-ttu-id="15295-146">È possibile farvi riferimento solo tramite `PackageReference`, quindi i progetti `packages.config` precedenti sono esclusi.</span><span class="sxs-lookup"><span data-stu-id="15295-146">They can only be referenced by `PackageReference`, so older `packages.config` projects are excluded.</span></span> <span data-ttu-id="15295-147">I pacchetti di codice sorgente condiviso, inoltre, possono essere usati solo da progetti con lo stesso tipo di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="15295-147">Also shared source packages are only usable by projects with the same language type.</span></span> <span data-ttu-id="15295-148">A causa di queste limitazioni, è preferibile usare i pacchetti di codice sorgente condiviso per condividere funzionalità in un progetto open source.</span><span class="sxs-lookup"><span data-stu-id="15295-148">Because of these limitations shared source packages are best used to share functionality within an open-source project.</span></span>

<span data-ttu-id="15295-149">**✔️ VALUTARE** la possibilità di fare riferimento a pacchetti di codice sorgente condiviso per funzionalità interne di piccola entità.</span><span class="sxs-lookup"><span data-stu-id="15295-149">**✔️ CONSIDER** referencing shared source packages for small, internal pieces of functionality.</span></span>

<span data-ttu-id="15295-150">**✔️ VALUTARE** la possibilità di impostare un pacchetto come pacchetto di codice sorgente condiviso se fornisce funzionalità interne di piccola entità.</span><span class="sxs-lookup"><span data-stu-id="15295-150">**✔️ CONSIDER** making your package a shared source package if it provides small, internal pieces of functionality.</span></span>

<span data-ttu-id="15295-151">**✔️ FARE RIFERIMENTO** ai pacchetti di codice sorgente condiviso con `PrivateAssets="All"`.</span><span class="sxs-lookup"><span data-stu-id="15295-151">**✔️ DO** reference shared source packages with `PrivateAssets="All"`.</span></span>

> <span data-ttu-id="15295-152">Questa impostazione indica a NuGet che il pacchetto deve essere usato solo in fase di sviluppo e non deve essere esposto come dipendenza pubblica.</span><span class="sxs-lookup"><span data-stu-id="15295-152">This setting tells NuGet the package is only to be used at development time and shouldn't be exposed as a public dependency.</span></span>

<span data-ttu-id="15295-153">**❌ NON** inserire tipi di pacchetti di codice sorgente condiviso nell'API pubblica.</span><span class="sxs-lookup"><span data-stu-id="15295-153">**❌ DO NOT** have shared source package types in your public API.</span></span>

> <span data-ttu-id="15295-154">I tipi di codice sorgente condiviso vengono compilati nell'assembly di riferimento e non possono essere scambiati tra assembly diversi.</span><span class="sxs-lookup"><span data-stu-id="15295-154">Shared source types are compiled into the referencing assembly and can't be exchanged across assembly boundaries.</span></span> <span data-ttu-id="15295-155">Ad esempio, un tipo `IRepository` di codice sorgente condiviso in un progetto è un tipo diverso dallo stesso oggetto `IRepository` di codice sorgente condiviso in un altro progetto.</span><span class="sxs-lookup"><span data-stu-id="15295-155">For example, a shared-source `IRepository` type in one project is a separate type from the same shared-source `IRepository` in another project.</span></span> <span data-ttu-id="15295-156">I tipi nei pacchetti di codice sorgente condiviso devono avere visibilità `internal`.</span><span class="sxs-lookup"><span data-stu-id="15295-156">Types in shared source packages should have an `internal` visibility.</span></span>

<span data-ttu-id="15295-157">**❌ NON** pubblicare pacchetti di codice sorgente condiviso in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="15295-157">**❌ DO NOT** publish shared source packages to nuget.org.</span></span>

> <span data-ttu-id="15295-158">I pacchetti di codice sorgente condiviso contengono codice sorgente e possono essere usati solo da progetti con lo stesso tipo di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="15295-158">Shared source packages contain source code and can only be used by projects with the same language type.</span></span> <span data-ttu-id="15295-159">Ad esempio, un pacchetto di codice sorgente condiviso C# non può essere usato da un'applicazione F#.</span><span class="sxs-lookup"><span data-stu-id="15295-159">For example, a C# shared source package cannot be used by an F# application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="15295-160">[Precedente](./nuget.md)
[Successivo](./sourcelink.md)</span><span class="sxs-lookup"><span data-stu-id="15295-160">[Previous](./nuget.md)
[Next](./sourcelink.md)</span></span>