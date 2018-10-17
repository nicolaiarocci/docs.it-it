---
title: Architettura approcci - App senza server
description: Per la compilazione di applicazioni aziendali basate su cloud, da architetture a più livelli per senza server si avvicina un'introduzione all'architettura.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 21e191f17e7d0b4f2d64454fb14c46a4831a8375
ms.sourcegitcommit: 64f4baed249341e5bf64d1385bf48e3f2e1a0211
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "49370020"
---
# <a name="architecture-approaches"></a><span data-ttu-id="45932-103">Approcci di architettura</span><span class="sxs-lookup"><span data-stu-id="45932-103">Architecture approaches</span></span>

<span data-ttu-id="45932-104">La comprensione di approcci esistenti per la progettazione di App aziendali consente di chiarire il ruolo svolto da senza server.</span><span class="sxs-lookup"><span data-stu-id="45932-104">Understanding existing approaches to architecting enterprise apps helps clarify the role played by serverless.</span></span> <span data-ttu-id="45932-105">Esistono molti approcci e i modelli che si è evoluta negli decenni dello sviluppo software e tutti i propri vantaggi e svantaggi.</span><span class="sxs-lookup"><span data-stu-id="45932-105">There are many approaches and patterns that evolved over decades of software development, and all have their own pros and cons.</span></span> <span data-ttu-id="45932-106">In molti casi, la soluzione definitiva non può riguardare scelta di un unico approccio ma può essere integrato diversi approcci.</span><span class="sxs-lookup"><span data-stu-id="45932-106">In many cases, the ultimate solution may not involve deciding on a single approach but may integrate several approaches.</span></span> <span data-ttu-id="45932-107">Gli scenari di migrazione includono spesso shifting dall'approccio di uno architettura a altro tramite un approccio ibrido.</span><span class="sxs-lookup"><span data-stu-id="45932-107">Migration scenarios often involve shifting from one architecture approach to another through a hybrid approach.</span></span>

<span data-ttu-id="45932-108">In questo capitolo viene fornita una panoramica di entrambi i modelli di architettura logica e fisica per le applicazioni aziendali.</span><span class="sxs-lookup"><span data-stu-id="45932-108">This chapter provides an overview of both logical and physical architecture patterns for enterprise applications.</span></span>

## <a name="architecture-patterns"></a><span data-ttu-id="45932-109">Modelli di architettura</span><span class="sxs-lookup"><span data-stu-id="45932-109">Architecture patterns</span></span>

<span data-ttu-id="45932-110">Le applicazioni aziendali moderne seguono un'ampia gamma di modelli di architettura.</span><span class="sxs-lookup"><span data-stu-id="45932-110">Modern business applications follow a variety of architecture patterns.</span></span> <span data-ttu-id="45932-111">In questa sezione rappresenta un sondaggio di modelli comuni.</span><span class="sxs-lookup"><span data-stu-id="45932-111">This section represents a survey of common patterns.</span></span> <span data-ttu-id="45932-112">I modelli elencati di seguito non sono necessariamente tutte le procedure consigliate, ma vengono illustrati diversi approcci.</span><span class="sxs-lookup"><span data-stu-id="45932-112">The patterns listed here aren't necessarily all best practices, but illustrate different approaches.</span></span>

<span data-ttu-id="45932-113">Per altre informazioni, vedere [Guida all'architettura delle applicazione Azure](https://docs.microsoft.com/azure/architecture/guide/).</span><span class="sxs-lookup"><span data-stu-id="45932-113">For more information, see [Azure application architecture guide](https://docs.microsoft.com/azure/architecture/guide/).</span></span>

## <a name="monoliths"></a><span data-ttu-id="45932-114">Strutture monolitiche</span><span class="sxs-lookup"><span data-stu-id="45932-114">Monoliths</span></span>

<span data-ttu-id="45932-115">Molte applicazioni aziendali seguono un modello di App monolitica.</span><span class="sxs-lookup"><span data-stu-id="45932-115">Many business applications follow a monolith pattern.</span></span> <span data-ttu-id="45932-116">Le applicazioni legacy vengono spesso implementate come strutture monolitiche.</span><span class="sxs-lookup"><span data-stu-id="45932-116">Legacy applications are often implemented as monoliths.</span></span> <span data-ttu-id="45932-117">Nel modello di struttura monolitica, tutti i problemi relativi all'applicazione sono contenuti in una singola distribuzione.</span><span class="sxs-lookup"><span data-stu-id="45932-117">In the monolith pattern, all application concerns are contained in a single deployment.</span></span> <span data-ttu-id="45932-118">Tutti gli elementi dell'interfaccia utente per le chiamate al database è incluso nella stessa codebase.</span><span class="sxs-lookup"><span data-stu-id="45932-118">Everything from user interface to database calls is included in the same codebase.</span></span>

![Architettura monolite](./media/monolith-architecture.png)

<span data-ttu-id="45932-120">Esistono diversi vantaggi dell'approccio monolite.</span><span class="sxs-lookup"><span data-stu-id="45932-120">There are several advantages to the monolith approach.</span></span> <span data-ttu-id="45932-121">Spesso è facile ottenga una singola codebase e iniziare a lavorare.</span><span class="sxs-lookup"><span data-stu-id="45932-121">It's often easy to pull down a single code base and start working.</span></span> <span data-ttu-id="45932-122">Periodo di addestramento può essere inferiore e la creazione di ambienti di test è semplice come fornire una nuova copia.</span><span class="sxs-lookup"><span data-stu-id="45932-122">Ramp up time may be less, and creating test environments is as simple as providing a new copy.</span></span> <span data-ttu-id="45932-123">Il monolite può essere progettato per includere più componenti e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="45932-123">The monolith may be designed to include multiple components and applications.</span></span>

<span data-ttu-id="45932-124">Sfortunatamente, il modello di struttura monolitica tende a suddividere su larga scala.</span><span class="sxs-lookup"><span data-stu-id="45932-124">Unfortunately, the monolith pattern tends to break down at scale.</span></span> <span data-ttu-id="45932-125">Principali svantaggi dell'approccio monolite includono:</span><span class="sxs-lookup"><span data-stu-id="45932-125">Major disadvantages of the monolith approach include:</span></span>

* <span data-ttu-id="45932-126">Difficoltà di operare in parallelo nella stessa base di codice.</span><span class="sxs-lookup"><span data-stu-id="45932-126">Difficult to work in parallel in the same code base.</span></span>
* <span data-ttu-id="45932-127">Qualsiasi modifica, indipendentemente dal modo in cui banale, richiede la distribuzione di una nuova versione dell'intera applicazione.</span><span class="sxs-lookup"><span data-stu-id="45932-127">Any change, no matter how trivial, requires deploying a new version of the entire application.</span></span>
* <span data-ttu-id="45932-128">Refactoring potenzialmente interessa l'intera applicazione.</span><span class="sxs-lookup"><span data-stu-id="45932-128">Refactoring potentially impacts the entire application.</span></span>
* <span data-ttu-id="45932-129">Spesso l'unica soluzione per la scalabilità consiste nel creare più copie di elevato utilizzo di risorse dell'App monolitica.</span><span class="sxs-lookup"><span data-stu-id="45932-129">Often the only solution to scale is to create multiple, resource-intensive copies of the monolith.</span></span>
* <span data-ttu-id="45932-130">Come espandere i sistemi o vengono acquisiti altri sistemi, integrazione può essere difficile.</span><span class="sxs-lookup"><span data-stu-id="45932-130">As systems expand or other systems are acquired, integration can be difficult.</span></span>
* <span data-ttu-id="45932-131">Potrebbe essere difficile testare a causa della necessità di configurare il monolite intero.</span><span class="sxs-lookup"><span data-stu-id="45932-131">It may be difficult to test due to the need to configure the entire monolith.</span></span>
* <span data-ttu-id="45932-132">Riutilizzo del codice è complesso e spesso altre App finisce con le proprie copie del codice.</span><span class="sxs-lookup"><span data-stu-id="45932-132">Code reuse is challenging and often other apps end up having their own copies of code.</span></span>

<span data-ttu-id="45932-133">Molte aziende Cerca nel cloud come un'opportunità per la migrazione delle applicazioni monolite e allo stesso tempo il refactoring per più modelli utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="45932-133">Many businesses look to the cloud as an opportunity to migrate monolith applications and at the same time refactor them to more usable patterns.</span></span> <span data-ttu-id="45932-134">È comune per suddividere le singole applicazioni e i componenti in modo che possano essere gestiti, distribuire e ridimensionare separatamente.</span><span class="sxs-lookup"><span data-stu-id="45932-134">It's common to break out the individual applications and components to allow them to be maintained, deployed, and scaled separately.</span></span>

## <a name="n-layer-applications"></a><span data-ttu-id="45932-135">Applicazioni a più livelli</span><span class="sxs-lookup"><span data-stu-id="45932-135">N-Layer applications</span></span>

<span data-ttu-id="45932-136">Applicazione a più livelli partizione dell'applicazione per la logica in livelli specifici.</span><span class="sxs-lookup"><span data-stu-id="45932-136">N-layer application partition application logic into specific layers.</span></span> <span data-ttu-id="45932-137">I livelli più comuni includono:</span><span class="sxs-lookup"><span data-stu-id="45932-137">The most common layers include:</span></span>

* <span data-ttu-id="45932-138">Interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="45932-138">User interface</span></span>
* <span data-ttu-id="45932-139">logica di Business</span><span class="sxs-lookup"><span data-stu-id="45932-139">Business logic</span></span>
* <span data-ttu-id="45932-140">Accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="45932-140">Data access</span></span>

<span data-ttu-id="45932-141">Possono includere altri livelli middleware, l'elaborazione batch e API.</span><span class="sxs-lookup"><span data-stu-id="45932-141">Other layers may include middleware, batch processing, and API.</span></span> <span data-ttu-id="45932-142">È importante tenere presente che i livelli sono logici.</span><span class="sxs-lookup"><span data-stu-id="45932-142">It's important to note the layers are logical.</span></span> <span data-ttu-id="45932-143">Sebbene svilupparono in isolamento, tutti di questi può essere distribuiti per la stessa piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="45932-143">Although they're developed in isolation, they may all be deployed to the same target platform.</span></span>

![Architettura a più livelli](./media/n-layer-architecture.png)

<span data-ttu-id="45932-145">Esistono diversi vantaggi dell'approccio a più livelli, tra cui:</span><span class="sxs-lookup"><span data-stu-id="45932-145">There are several advantages to the N-Layer approach, including:</span></span>

* <span data-ttu-id="45932-146">Il refactoring è isolata e prevede un livello.</span><span class="sxs-lookup"><span data-stu-id="45932-146">Refactoring is isolated to a layer.</span></span>
* <span data-ttu-id="45932-147">In modo indipendente i team possono creare, testare, distribuire e gestire livelli separati.</span><span class="sxs-lookup"><span data-stu-id="45932-147">Teams can independently build, test, deploy, and maintain separate layers.</span></span>
* <span data-ttu-id="45932-148">I livelli possono essere scambiati in modo, ad esempio il livello dati può accedere a più database senza dover apportare modifiche a livello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="45932-148">Layers can be swapped out, for example the data layer may access multiple databases without requiring changes to the UI layer.</span></span>

<span data-ttu-id="45932-149">Serverless può essere utilizzato per implementare uno o più livelli.</span><span class="sxs-lookup"><span data-stu-id="45932-149">Serverless may be used to implement one or more layers.</span></span>

## <a name="microservices"></a><span data-ttu-id="45932-150">Microservizi</span><span class="sxs-lookup"><span data-stu-id="45932-150">Microservices</span></span>

<span data-ttu-id="45932-151">**[I Microservizi](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)**  architetture contengano caratteristiche comuni che includono:</span><span class="sxs-lookup"><span data-stu-id="45932-151">**[Microservices](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)** architectures contain common characteristics that include:</span></span>

* <span data-ttu-id="45932-152">Le applicazioni sono costituite da piccoli servizi diversi.</span><span class="sxs-lookup"><span data-stu-id="45932-152">Applications are composed of several small services.</span></span>
* <span data-ttu-id="45932-153">Ogni servizio viene eseguito nel proprio processo.</span><span class="sxs-lookup"><span data-stu-id="45932-153">Each service runs in its own process.</span></span>
* <span data-ttu-id="45932-154">I servizi sono allineati intorno a domini aziendali.</span><span class="sxs-lookup"><span data-stu-id="45932-154">Services are aligned around business domains.</span></span>
* <span data-ttu-id="45932-155">I servizi comunicano tramite API leggere, in genere Usa HTTP come trasporto.</span><span class="sxs-lookup"><span data-stu-id="45932-155">Services communicate over lightweight APIs, typically using HTTP as the transport.</span></span>
* <span data-ttu-id="45932-156">Servizi possono essere distribuiti e aggiornati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="45932-156">Services can be deployed and upgraded independently.</span></span>
* <span data-ttu-id="45932-157">Servizi non dipendenti da un unico archivio dati.</span><span class="sxs-lookup"><span data-stu-id="45932-157">Services aren't dependent on a single data store.</span></span>
* <span data-ttu-id="45932-158">Il sistema è progettato con un errore presente, e le app possono comunque eseguire anche quando determinati servizi hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="45932-158">The system is designed with failure in mind, and the app may still run even when certain services fail.</span></span>

<span data-ttu-id="45932-159">I Microservizi non dovranno essere si escludono a vicenda per altri approcci di architettura.</span><span class="sxs-lookup"><span data-stu-id="45932-159">Microservices don't have to be mutually exclusive to other architecture approaches.</span></span> <span data-ttu-id="45932-160">Ad esempio, un'architettura a più livelli può usare i microservizi per il livello intermedio.</span><span class="sxs-lookup"><span data-stu-id="45932-160">For example, an N-Tier architecture may use microservices for the middle tier.</span></span> <span data-ttu-id="45932-161">È anche possibile implementare i microservizi in svariati modi, dalle directory virtuali in host IIS per i contenitori.</span><span class="sxs-lookup"><span data-stu-id="45932-161">It's also possible to implement microservices in a variety of ways, from virtual directories on IIS hosts to containers.</span></span> <span data-ttu-id="45932-162">Caratteristiche dei microservizi li rendono ideali in particolare per le implementazioni senza server.</span><span class="sxs-lookup"><span data-stu-id="45932-162">The characteristics of microservices make them especially ideal for serverless implementations.</span></span>

![Architettura di microservizi](./media/microservices-architecture.png)

<span data-ttu-id="45932-164">I professionisti di architetture di microservizi includono:</span><span class="sxs-lookup"><span data-stu-id="45932-164">The pros of microservices architectures include:</span></span>

* <span data-ttu-id="45932-165">Spesso il refactoring è isolata e prevede un singolo servizio.</span><span class="sxs-lookup"><span data-stu-id="45932-165">Refactoring is often isolated to a single service.</span></span>
* <span data-ttu-id="45932-166">I servizi possono essere aggiornati indipendentemente uno da altro.</span><span class="sxs-lookup"><span data-stu-id="45932-166">Services can be upgraded independently of each other.</span></span>
* <span data-ttu-id="45932-167">Resilienza e l'elasticità possono essere ottimizzate per le esigenze dei singoli servizi.</span><span class="sxs-lookup"><span data-stu-id="45932-167">Resiliency and elasticity can be tuned to the demands of individual services.</span></span>
* <span data-ttu-id="45932-168">Sviluppo può verificarsi in parallelo tra le piattaforme e diversi team.</span><span class="sxs-lookup"><span data-stu-id="45932-168">Development can happen in parallel across disparate teams and platforms.</span></span>
* <span data-ttu-id="45932-169">È più semplice scrivere i test completi per i servizi di tipo isolati.</span><span class="sxs-lookup"><span data-stu-id="45932-169">It's easier to write comprehensive tests for isolated services.</span></span>

<span data-ttu-id="45932-170">I Microservizi sono dotate di proprie problematiche, tra cui:</span><span class="sxs-lookup"><span data-stu-id="45932-170">Microservices come with their own challenges, including:</span></span>

* <span data-ttu-id="45932-171">Determinare quali servizi sono disponibili e come chiamarle.</span><span class="sxs-lookup"><span data-stu-id="45932-171">Determining what services are available and how to call them.</span></span>
* <span data-ttu-id="45932-172">Gestire il ciclo di vita dei servizi.</span><span class="sxs-lookup"><span data-stu-id="45932-172">Managing the lifecycle of services.</span></span>
* <span data-ttu-id="45932-173">Comprendere come i servizi si integrino in applicazione globale.</span><span class="sxs-lookup"><span data-stu-id="45932-173">Understanding how services fit together in the overall application.</span></span>
* <span data-ttu-id="45932-174">Test di sistema completo delle chiamate effettuate tra i diversi servizi.</span><span class="sxs-lookup"><span data-stu-id="45932-174">Full system testing of calls made across disparate services.</span></span>

<span data-ttu-id="45932-175">In definitiva sono disponibili soluzioni per soddisfare tutti questi problemi, tra cui attingere ai vantaggi degli strumenti senza server che verranno trattati più avanti.</span><span class="sxs-lookup"><span data-stu-id="45932-175">Ultimately there are solutions to address all of these challenges, including tapping into the benefits of serverless that are discussed later.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="45932-176">[Precedente](index.md)
[Successivo](architecture-deployment-approaches.md)</span><span class="sxs-lookup"><span data-stu-id="45932-176">[Previous](index.md)
[Next](architecture-deployment-approaches.md)</span></span>