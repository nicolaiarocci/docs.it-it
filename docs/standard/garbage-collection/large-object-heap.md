---
title: Heap oggetti grandi nei sistemi Windows
ms.date: 05/02/2018
helpviewer_keywords:
- large object heap (LOH)"
- LOH
- garbage collection, large object heap
- GC [.NET ], large object heap
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: abb1f72a10a4aff448dea22b5c9415111c25eaab
ms.sourcegitcommit: 43924acbdbb3981d103e11049bbe460457d42073
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2018
---
# <a name="the-large-object-heap-on-windows-systems"></a><span data-ttu-id="ad555-102">Heap oggetti grandi nei sistemi Windows</span><span class="sxs-lookup"><span data-stu-id="ad555-102">The large object heap on Windows systems</span></span>

<span data-ttu-id="ad555-103">.NET Garbage Collector (GC) suddivide gli oggetti in oggetti piccoli e grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-103">The .NET Garbage Collector (GC) divides objects up into small and large objects.</span></span> <span data-ttu-id="ad555-104">Nel caso di un oggetto grande, alcuni attributi associati assumono un'importanza maggiore rispetto a quando sono associati a un oggetto piccolo.</span><span class="sxs-lookup"><span data-stu-id="ad555-104">When an object is large, some of its attributes become more significant than if the object is small.</span></span> <span data-ttu-id="ad555-105">Ad esempio la compattazione, ovvero la copia in memoria dell'oggetto in un altro punto dell'heap, può risultare dispendiosa.</span><span class="sxs-lookup"><span data-stu-id="ad555-105">For instance, compacting it -- that is, copying it in memory elsewhere on the heap -- can be expensive.</span></span> <span data-ttu-id="ad555-106">Per questo motivo .NET Garbage Collector inserisce gli oggetti di grandi dimensioni nell'heap oggetti grandi (LOH, Large Object Heap).</span><span class="sxs-lookup"><span data-stu-id="ad555-106">Because of this, the .NET Garbage Collector places large objects on the large object heap (LOH).</span></span> <span data-ttu-id="ad555-107">In questo argomento viene esaminato in modo approfondito l'heap oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-107">In this topic, we'll look at the large object heap in depth.</span></span> <span data-ttu-id="ad555-108">Si analizzano gli elementi che qualificano un oggetto come oggetto grande, come vengono raccolti gli oggetti grandi e il tipo di implicazioni di questi oggetti sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ad555-108">We'll discuss what qualifies an object as a large object, how these large objects are collected, and what kind of performance implications large objects impose.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad555-109">Questo argomento illustra l'heap oggetti grandi in .NET Framework e .NET Core in esecuzione solo nei sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="ad555-109">This topic discusses the large object heap in the .NET Framework and .NET Core running on Windows systems only.</span></span> <span data-ttu-id="ad555-110">Non riguarda l'heap oggetti grandi in esecuzione in implementazioni di .NET su altre piattaforme.</span><span class="sxs-lookup"><span data-stu-id="ad555-110">It does not cover the LOH running on .NET implementations on other platforms.</span></span>

## <a name="how-an-object-ends-up-on-the-large-object-heap-and-how-gc-handles-them"></a><span data-ttu-id="ad555-111">Come un oggetto raggiunge l'heap oggetti grandi e come viene gestito da GC</span><span class="sxs-lookup"><span data-stu-id="ad555-111">How an object ends up on the large object heap and how GC handles them</span></span>

<span data-ttu-id="ad555-112">Se le dimensioni di un oggetto sono superiori o uguali a 85.000 byte, l'oggetto viene considerato un oggetto grande.</span><span class="sxs-lookup"><span data-stu-id="ad555-112">If an object is greater than or equal to 85,000 bytes, it’s considered a large object.</span></span> <span data-ttu-id="ad555-113">Questo valore è stato determinato dall'ottimizzazione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ad555-113">This number was determined by performance tuning.</span></span> <span data-ttu-id="ad555-114">Quando la richiesta di allocazione di un oggetto supera gli 85.000 byte, il runtime destina l'oggetto all'heap oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-114">When an object allocation request is for 85,000 or more bytes, the runtime allocates it on the large object heap.</span></span>

<span data-ttu-id="ad555-115">Per comprendere il significato di questa impostazione, è utile esaminare alcuni principi fondamentali di GC in .NET.</span><span class="sxs-lookup"><span data-stu-id="ad555-115">To understand what this means, it's useful to examine some fundamentals about the .NET GC.</span></span>

<span data-ttu-id="ad555-116">Il Garbage Collector di .NET è un collector generazionale.</span><span class="sxs-lookup"><span data-stu-id="ad555-116">The .NET Garbage Collector is a generational collector.</span></span> <span data-ttu-id="ad555-117">Le generazioni sono tre: generazione 0, generazione 1 e generazione 2.</span><span class="sxs-lookup"><span data-stu-id="ad555-117">It has three generations: generation 0, generation 1, and generation 2.</span></span> <span data-ttu-id="ad555-118">La presenza di 3 generazioni deriva dal fatto che in un'app ottimizzata la maggior parte degli oggetti viene eliminata nella generazione 0.</span><span class="sxs-lookup"><span data-stu-id="ad555-118">The reason for having 3 generations is that, in a well-tuned app, most objects die in gen0.</span></span> <span data-ttu-id="ad555-119">In un'applicazione server, ad esempio, le allocazioni associate a ogni richiesta dovrebbero essere eliminate al termine della richiesta.</span><span class="sxs-lookup"><span data-stu-id="ad555-119">For example, in a server app, the allocations associated with each request should die after the request is finished.</span></span> <span data-ttu-id="ad555-120">Le richieste di allocazione durante l'esecuzione raggiungono la generazione 1 e vengono eliminate in questa generazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-120">The in-flight allocation requests will make it into gen1 and die there.</span></span> <span data-ttu-id="ad555-121">In pratica la generazione 1 fa da buffer tra le aree degli oggetti recenti e quelle degli oggetti con durata maggiore.</span><span class="sxs-lookup"><span data-stu-id="ad555-121">Essentially, gen1 acts as a buffer between young object areas and long-lived object areas.</span></span>

<span data-ttu-id="ad555-122">Gli oggetti piccoli vengono sempre allocati nella generazione 0 e a seconda della loro ciclo di vita possono passare alla generazione 1 o alla generazione 2.</span><span class="sxs-lookup"><span data-stu-id="ad555-122">Small objects are always allocated in generation 0 and, depending on their lifetime, may be promoted to generation 1 or generation2.</span></span> <span data-ttu-id="ad555-123">Gli oggetti grandi vengono sempre allocati nella generazione 2.</span><span class="sxs-lookup"><span data-stu-id="ad555-123">Large objects are always allocated in generation 2.</span></span>

<span data-ttu-id="ad555-124">Gli oggetti grandi appartengono alla generazione 2 perché vengono raccolti solo durante una raccolta di generazione 2.</span><span class="sxs-lookup"><span data-stu-id="ad555-124">Large objects belong to generation 2 because they are collected only during a generation 2 collection.</span></span> <span data-ttu-id="ad555-125">Quando viene raccolta una generazione, vengono raccolte anche le generazioni più giovani corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="ad555-125">When a generation is collected, all its younger generation(s) are also collected.</span></span> <span data-ttu-id="ad555-126">Ad esempio quando si verifica un'operazione GC di generazione 1 vengono raccolte sia la generazione 1 che la generazione 0.</span><span class="sxs-lookup"><span data-stu-id="ad555-126">For example, when a generation 1 GC happens, both generation 1 and 0 are collected.</span></span> <span data-ttu-id="ad555-127">Quando si verifica un'operazione GC di generazione 2 viene raccolto l'intero heap.</span><span class="sxs-lookup"><span data-stu-id="ad555-127">And when a generation 2 GC happens, the whole heap is collected.</span></span> <span data-ttu-id="ad555-128">Per questo motivo un'operazione GC di generazione 2 è anche detta *operazione GC completa*.</span><span class="sxs-lookup"><span data-stu-id="ad555-128">For this reason, a generation 2 GC is also called a *full GC*.</span></span> <span data-ttu-id="ad555-129">L'articolo cita l'operazione GC di generazione 2 anziché l'operazione GC completa, ma i termini sono intercambiabili.</span><span class="sxs-lookup"><span data-stu-id="ad555-129">This article refers to generation 2 GC instead of full GC, but the terms are interchangeable.</span></span>

<span data-ttu-id="ad555-130">Le generazioni offrono una visualizzazione logica dell'heap GC.</span><span class="sxs-lookup"><span data-stu-id="ad555-130">Generations provide a logical view of the GC heap.</span></span> <span data-ttu-id="ad555-131">A livello fisico gli oggetti si trovano in segmenti gestiti dell'heap.</span><span class="sxs-lookup"><span data-stu-id="ad555-131">Physically, objects live in managed heap segments.</span></span> <span data-ttu-id="ad555-132">Un *segmento gestito dell'heap* è una parte di memoria che l'operazione GC riserva nel sistema operativo (chiamando la [funzione VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx)) per conto del codice gestito.</span><span class="sxs-lookup"><span data-stu-id="ad555-132">A *managed heap segment* is a chunk of memory that the GC reserves from the OS by calling the [VirtualAlloc function](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx) on behalf of managed code.</span></span> <span data-ttu-id="ad555-133">Quando viene caricato il CLR, l'operazione GC alloca due segmenti di heap iniziali, l'heap oggetti piccoli (SOH, Small Object Heap) e l'heap oggetti grandi (LOH, Large Object Heap).</span><span class="sxs-lookup"><span data-stu-id="ad555-133">When the CLR is loaded, the GC allocates two initial heap segments: one for small objects (the Small Object Heap, or SOH), and one for large objects (the Large Object Heap).</span></span>

<span data-ttu-id="ad555-134">Le richieste di allocazione vengono quindi soddisfatte inserendo gli oggetti gestiti in uno di questi segmenti di heap gestiti.</span><span class="sxs-lookup"><span data-stu-id="ad555-134">The allocation requests are then satisfied by putting managed objects on these managed heap segments.</span></span> <span data-ttu-id="ad555-135">Se l'oggetto ha dimensioni inferiori a 85.000 byte viene inserito in un segmento SOH; in caso contrario viene inserito in un segmento LOH.</span><span class="sxs-lookup"><span data-stu-id="ad555-135">If the object is less than 85,000 bytes, it is put on the segment for the SOH; otherwise, it is put on an LOH segment.</span></span> <span data-ttu-id="ad555-136">Man mano che nei segmenti vengono allocati gli oggetti, tali segmenti vengono impegnati (in blocchi più piccoli).</span><span class="sxs-lookup"><span data-stu-id="ad555-136">Segments are committed (in smaller chunks) as more and more objects are allocated onto them.</span></span>
<span data-ttu-id="ad555-137">Per l'heap oggetti piccoli, gli oggetti ancora attivi dopo un'operazione GC vengono promossi alla generazione successiva.</span><span class="sxs-lookup"><span data-stu-id="ad555-137">For the SOH, objects that survive a GC are promoted to the next generation.</span></span> <span data-ttu-id="ad555-138">Gli oggetti esclusi da una raccolta di generazione 0 sono ora considerati oggetti di generazione 1 e così via.</span><span class="sxs-lookup"><span data-stu-id="ad555-138">Objects that survive a generation 0 collection are now considered generation 1 objects, and so on.</span></span> <span data-ttu-id="ad555-139">Gli oggetti che raggiungono la generazione di grado superiore si considerano come appartenenti a tale generazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-139">However, objects that survive the oldest generation are still considered to be in the oldest generation.</span></span> <span data-ttu-id="ad555-140">In altri termini gli oggetti che rimangono nella generazione 2 sono oggetti di generazione 2 e gli oggetti che rimangono nel segmento LOH sono oggetti LOH (raccolti con la generazione 2).</span><span class="sxs-lookup"><span data-stu-id="ad555-140">In other words, survivors from generation 2 are generation 2 objects; and survivors from the LOH are LOH objects (which are collected with gen2).</span></span> 

<span data-ttu-id="ad555-141">Il codice utente può effettuare allocazioni solo nella generazione 0 (oggetti piccoli) o nell'heap oggetti grandi (LOH).</span><span class="sxs-lookup"><span data-stu-id="ad555-141">User code can only allocate in generation 0 (small objects) or the LOH (large objects).</span></span> <span data-ttu-id="ad555-142">Soltanto l'operazione GC può "allocare" gli oggetti nella generazione 1 (promuovendo i superstiti della generazione 0) e nella generazione 2 (promuovendo i superstiti delle generazioni 1 e 2).</span><span class="sxs-lookup"><span data-stu-id="ad555-142">Only the GC can “allocate” objects in generation 1 (by promoting survivors from generation 0) and generation 2 (by promoting survivors from generations 1 and 2).</span></span>

<span data-ttu-id="ad555-143">Quando viene attivata una Garbage Collection, il Garbage Collector rintraccia gli oggetti ancora attivi e li compatta.</span><span class="sxs-lookup"><span data-stu-id="ad555-143">When a garbage collection is triggered, the GC traces through the live objects and compacts them.</span></span> <span data-ttu-id="ad555-144">Tuttavia, dato che la compattazione è dispendiosa in termini di risorse, il GC *effettua lo sweep* dell'heap oggetti grandi e crea un elenco degli oggetti inattivi che possono essere riusati successivamente per soddisfare le richieste di allocazione di oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-144">But because compaction is expensive, the GC *sweeps* the LOH; it makes a free list out of dead objects that can be reused later to satisfy large object allocation requests.</span></span> <span data-ttu-id="ad555-145">Gli oggetti inattivi adiacenti vengono trasformati in un unico oggetto libero.</span><span class="sxs-lookup"><span data-stu-id="ad555-145">Adjacent dead objects are made into one free object.</span></span>

<span data-ttu-id="ad555-146">.NET core e .NET Framework (a partire da .NET Framework 4.5.1) includono la proprietà <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode?displayProperty="fullname"> che consente agli utenti di specificare che l'heap oggetti grandi dovrà essere compresso durante la successiva operazione GC completa e bloccante.</span><span class="sxs-lookup"><span data-stu-id="ad555-146">.NET Core and .NET Framework (starting with .NET Framework 4.5.1) include the <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode?displayProperty="fullname"> property that allows users to specify that the LOH should be compacted during the next full blocking GC.</span></span> <span data-ttu-id="ad555-147">In futuro è possibile che .NET scelga di compattare automaticamente l'heap oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-147">And in the future, .NET may decide to compact the LOH automatically.</span></span> <span data-ttu-id="ad555-148">Quindi se si allocano oggetti grandi e si vuole essere certi che non verranno spostati, è ancora necessario bloccarli.</span><span class="sxs-lookup"><span data-stu-id="ad555-148">This means that, if you allocate large objects and want to make sure that they don’t move, you should still pin them.</span></span>

<span data-ttu-id="ad555-149">La figura 1 illustra uno scenario in cui GC forma la generazione 1 dopo la prima operazione GC di generazione 0 in cui `Obj1` e `Obj3` sono inattivi e forma la generazione 2 dopo la prima operazione GC di generazione 1 in cui `Obj2` e `Obj5` sono inattivi.</span><span class="sxs-lookup"><span data-stu-id="ad555-149">Figure 1 illustrates a scenario where the GC forms generation 1 after the first generation 0 GC where `Obj1` and `Obj3` are dead, and it forms generation 2 after the first generation 1 GC where `Obj2` and `Obj5` are dead.</span></span> <span data-ttu-id="ad555-150">Si noti che questa figura e le successive sono incluse a semplice scopo illustrativo e contengono pochissimi oggetti per illustrare meglio cosa accade nell'heap.</span><span class="sxs-lookup"><span data-stu-id="ad555-150">Note that this and the following figures are only for illustration purposes; they contain very few objects to better show what happens on the heap.</span></span> <span data-ttu-id="ad555-151">In realtà un'operazione GC include in genere un numero di oggetti molto più elevato.</span><span class="sxs-lookup"><span data-stu-id="ad555-151">In reality, many more objects are typically involved in a GC.</span></span>

![Figura 1: GC generazione 0 e GC generazione 1](media/loh/loh-figure-1.jpg)   
<span data-ttu-id="ad555-153">Figura 1: GC generazione 0 e GC generazione 1.</span><span class="sxs-lookup"><span data-stu-id="ad555-153">Figure 1: A generation 0 and a generation 1 GC.</span></span>

<span data-ttu-id="ad555-154">Nella figura 2, dopo un'operazione GC di generazione 2 in cui viene rilevato che `Obj1` e `Obj2` sono inattivi, il Garbage Collector crea spazio libero contiguo con la memoria occupata in precedenza da `Obj1` e `Obj2` e tale memoria viene usata per soddisfare una richiesta di allocazione per `Obj4`.</span><span class="sxs-lookup"><span data-stu-id="ad555-154">Figure 2 shows that after a generation 2 GC which saw that `Obj1` and `Obj2` are dead, the GC forms contiguous free space out of memory that used to be occupied by `Obj1` and `Obj2`, which then was used to satisfy an allocation request for `Obj4`.</span></span> <span data-ttu-id="ad555-155">Anche lo spazio dopo l'ultimo oggetto, `Obj3`, e fino alla fine del segmento può essere usato per soddisfare richieste di allocazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-155">The space after the last object, `Obj3`, to end of the segment can also be used to satisfy allocation requests.</span></span>
 
![Figura 2: Dopo un'operazione GC di generazione 2](media/loh/loh-figure-2.jpg)  
<span data-ttu-id="ad555-157">Figura 2: Dopo un'operazione GC di generazione 2</span><span class="sxs-lookup"><span data-stu-id="ad555-157">Figure 2: After a generation 2 GC</span></span>

<span data-ttu-id="ad555-158">Se lo spazio libero non è sufficiente ad accogliere le richieste di allocazione di oggetti grandi, inizialmente GC prova a ottenere altri segmenti dal sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ad555-158">If there isn't enough free space to accommodate the large object allocation requests, the GC first attempts to acquire more segments from the OS.</span></span> <span data-ttu-id="ad555-159">Se il problema persiste, attiva un'operazione GC di generazione 2 per liberare spazio.</span><span class="sxs-lookup"><span data-stu-id="ad555-159">If that fails, it triggers a generation 2 GC in the hope of freeing up some space.</span></span>

<span data-ttu-id="ad555-160">Durante un'operazione GC di generazione 1 o 2 il Garbage Collector rilascia i segmenti privi di oggetti attivi al sistema operativo chiamando la [funzione VirtualFree](https://msdn.microsoft.com/library/windows/desktop/aa366892(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="ad555-160">During a generation 1 or generation 2 GC, the garbage collector releases segments that have no live objects on them back to the OS by calling the [VirtualFree function](https://msdn.microsoft.com/library/windows/desktop/aa366892(v=vs.85).aspx).</span></span> <span data-ttu-id="ad555-161">Viene annullato il commit dello spazio dopo l'ultimo oggetto attivo alla fine del segmento (salvo per il segmento effimero in cui risiedono gen0/gen1 e dove il Garbage Collector mantiene spazio con commit, perché l'applicazione lo alloca quasi immediatamente).</span><span class="sxs-lookup"><span data-stu-id="ad555-161">Space after the last live object to the end of the segment is decommitted (except on the ephemeral segment where gen0/gen1 live, where the garbage collector does keep some committed because your application will be allocating in it right away).</span></span> <span data-ttu-id="ad555-162">Gli spazi liberi mantengono il commit anche se vengono reimpostati, a indicare che il sistema operativo non ha bisogno di riscrivere su disco i dati in essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="ad555-162">And the free spaces remain committed though they are reset, meaning that the OS doesn’t need to write data in them back to disk.</span></span>

<span data-ttu-id="ad555-163">Dato che l'heap oggetti grandi viene raccolto solo durante operazioni GC di generazione 2, il segmento LOH può essere liberato solo durante un' operazione GC di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="ad555-163">Since the LOH is only collected during generation 2 GCs, the LOH segment can only be freed during such a GC.</span></span> <span data-ttu-id="ad555-164">La figura 3 illustra uno scenario in cui il Garbage Collector rilascia un segmento (segmento 2) al sistema operativo e annulla il commit di altro spazio nei segmenti rimanenti.</span><span class="sxs-lookup"><span data-stu-id="ad555-164">Figure 3 illustrates a scenario where the garbage collector releases one segment (segment 2) back to the OS and decommits more space on the remaining segments.</span></span> <span data-ttu-id="ad555-165">Se il Garbage Collector deve usare lo spazio liberato alla fine del segmento per soddisfare nuove richieste di allocazione di oggetti grandi, esegue di nuovo il commit della memoria.</span><span class="sxs-lookup"><span data-stu-id="ad555-165">If it needs to use the decommitted space at the end of the segment to satisfy large object allocation requests, it commits the memory again.</span></span> <span data-ttu-id="ad555-166">Per una spiegazione del commit e dell'annullamento del commit, vedere la documentazione relativa a [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="ad555-166">(For an explanation of commit/decommit, see the documentation for [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx).</span></span>
 
![Figura 3: LOH dopo un'operazione GC di generazione 2](media/loh/loh-figure-3.jpg)  
<span data-ttu-id="ad555-168">Figura 3: LOH dopo un'operazione GC di generazione 2</span><span class="sxs-lookup"><span data-stu-id="ad555-168">Figure 3: The LOH after a generation 2 GC</span></span>

## <a name="when-is-a-large-object-collected"></a><span data-ttu-id="ad555-169">Quando viene raccolto un oggetto di grandi dimensioni?</span><span class="sxs-lookup"><span data-stu-id="ad555-169">When is a large object collected?</span></span>

<span data-ttu-id="ad555-170">In genere un'operazione GC avviene quando si verifica una delle 3 condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad555-170">In general, a GC occurs when one of the following following 3 conditions happens:</span></span>

- <span data-ttu-id="ad555-171">L'allocazione supera la soglia della generazione 0 o degli oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-171">Allocation exceeds the generation 0 or large object threshold.</span></span>

   <span data-ttu-id="ad555-172">La soglia è una proprietà di una generazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-172">The threshold is a property of a generation.</span></span> <span data-ttu-id="ad555-173">Una soglia per una generazione viene impostata quando il Garbage Collector alloca oggetti al suo interno.</span><span class="sxs-lookup"><span data-stu-id="ad555-173">A threshold for a generation is set when the garbage collector allocates objects into it.</span></span> <span data-ttu-id="ad555-174">Quando la soglia viene superata viene attivata un'operazione GC su questa generazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-174">When the threshold is exceeded, a GC is triggered on that generation.</span></span> <span data-ttu-id="ad555-175">Pertanto, quando si allocano oggetti piccoli o grandi, si consumano rispettivamente le soglie della generazione 0 e dell'heap oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-175">When you allocate small or large objects, you consume generation 0 and the LOH’s thresholds, respectively.</span></span> <span data-ttu-id="ad555-176">Quando il Garbage Collector effettua allocazioni nelle generazioni 1 e 2, consuma le soglie di queste generazioni.</span><span class="sxs-lookup"><span data-stu-id="ad555-176">When the garbage collector allocates into generation 1 and 2, it consumes their thresholds.</span></span> <span data-ttu-id="ad555-177">Queste soglie vengono regolate dinamicamente mentre viene eseguito il programma.</span><span class="sxs-lookup"><span data-stu-id="ad555-177">These thresholds are dynamically tuned as the program runs.</span></span>

   <span data-ttu-id="ad555-178">Questo è lo scenario tipico: la maggior parte delle operazioni GC si verifica come conseguenza delle allocazioni nell'heap gestito.</span><span class="sxs-lookup"><span data-stu-id="ad555-178">This is the typical case; most GCs happen because of allocations on the managed heap.</span></span>

- <span data-ttu-id="ad555-179">Viene chiamato il metodo <xref:System.GC.Collect%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ad555-179">The <xref:System.GC.Collect%2A?displayProperty=nameWithType> method is called.</span></span>

   <span data-ttu-id="ad555-180">Se viene chiamato il metodo senza parametri <xref:System.GC.Collect?displayProperty=nameWithType> o se <xref:System.GC.MaxGeneration?displayProperty=nameWithType> viene passato come argomento a un altro overload, l'heap oggetti grandi viene raccolto insieme al resto dell'heap gestito.</span><span class="sxs-lookup"><span data-stu-id="ad555-180">If the parameterless <xref:System.GC.Collect?displayProperty=nameWithType> method is called or another overload is passed <xref:System.GC.MaxGeneration?displayProperty=nameWithType> as an argument, the LOH is collected along with the rest of the managed heap.</span></span>

- <span data-ttu-id="ad555-181">La memoria del sistema è insufficiente.</span><span class="sxs-lookup"><span data-stu-id="ad555-181">The system is in low memory situation.</span></span>

   <span data-ttu-id="ad555-182">Questo si verifica quando il Garbage Collector riceve una notifica di uso di memoria elevato dal sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ad555-182">This occurs when the garbage collector receives a high memory notification from the OS.</span></span> <span data-ttu-id="ad555-183">Se il Garbage Collector rileva condizioni produttive per un'operazione GC di generazione 2, attiva tale operazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-183">If the garbage collector thinks that doing a generation 2 GC will be productive, it triggers one.</span></span>

## <a name="loh-performance-implications"></a><span data-ttu-id="ad555-184">Implicazioni a livello di prestazioni dell'heap oggetti grandi</span><span class="sxs-lookup"><span data-stu-id="ad555-184">LOH Performance Implications</span></span>

<span data-ttu-id="ad555-185">Le allocazioni nell'heap oggetti grandi influiscono sulle prestazioni nei modi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ad555-185">Allocations on the large object heap impact performance in the following ways.</span></span>

- <span data-ttu-id="ad555-186">Costo di allocazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-186">Allocation cost.</span></span>

   <span data-ttu-id="ad555-187">Il CLR garantisce che la memoria per ogni nuovo oggetto inattivo venga liberata.</span><span class="sxs-lookup"><span data-stu-id="ad555-187">The CLR makes the guarantee that the memory for every new object it gives out is cleared.</span></span> <span data-ttu-id="ad555-188">Ciò significa che il costo di allocazione di un oggetto grande è totalmente determinato dalla liberazione della memoria (a meno che non attivi un'operazione GC).</span><span class="sxs-lookup"><span data-stu-id="ad555-188">This means the allocation cost of a large object is completely dominated by memory clearing (unless it triggers a GC).</span></span> <span data-ttu-id="ad555-189">Mentre per liberare un byte sono sufficienti due cicli, per liberare il più piccolo degli oggetti grandi sono necessari 170.000 cicli.</span><span class="sxs-lookup"><span data-stu-id="ad555-189">If it takes 2 cycles to clear one byte, it takes 170,000 cycles to clear the smallest large object.</span></span> <span data-ttu-id="ad555-190">La cancellazione della memoria corrispondente a un oggetto di 16 MB su un computer a 2 GHz richiede circa 16 ms.</span><span class="sxs-lookup"><span data-stu-id="ad555-190">Clearing the memmory of a 16MB object on a 2GHz machine takes approximately 16ms.</span></span> <span data-ttu-id="ad555-191">Si tratta di un costo operativo elevato.</span><span class="sxs-lookup"><span data-stu-id="ad555-191">That's a rather large cost.</span></span>

- <span data-ttu-id="ad555-192">Costo dell'operazione di raccolta.</span><span class="sxs-lookup"><span data-stu-id="ad555-192">Collection cost.</span></span>

   <span data-ttu-id="ad555-193">Poiché le operazioni GC per l'heap oggetti grandi e la generazione 2 avvengono insieme, se una delle due soglie viene superata si attiva una raccolta di generazione 2.</span><span class="sxs-lookup"><span data-stu-id="ad555-193">Because the LOH and generation 2 are collected together, if either one's threshold is exceeded, a generation 2 collection is triggered.</span></span> <span data-ttu-id="ad555-194">Se la raccolta di generazione 2 viene attivata a causa dell'heap oggetti grandi, il volume della generazione 2 potrebbe non risultare di molto ridotto dopo l'operazione GC.</span><span class="sxs-lookup"><span data-stu-id="ad555-194">If a generation 2 collection is triggered because of the LOH, generation 2 won't necessarily be much smaller after the GC.</span></span> <span data-ttu-id="ad555-195">Se la generazione 2 non contiene molti dati l'impatto è minimo.</span><span class="sxs-lookup"><span data-stu-id="ad555-195">If there's not much data on generation 2, this has minimal impact.</span></span> <span data-ttu-id="ad555-196">Se tuttavia il volume di dati di generazione 2 è importante, può causare problemi di prestazioni se vengono attivate varie operazioni GC di generazione 2.</span><span class="sxs-lookup"><span data-stu-id="ad555-196">But if generation 2 is large, it can cause performance problems if many generation 2 GCs are triggered.</span></span> <span data-ttu-id="ad555-197">Se molti oggetti grandi vengono allocati su base molto volatile e l'heap oggetti piccoli è molto grande, le operazioni GC potrebbero richiedere un tempo eccessivo.</span><span class="sxs-lookup"><span data-stu-id="ad555-197">If many large objects are allocated on a very temporary basis and you have a large SOH, you could be spending too much time doing GCs.</span></span> <span data-ttu-id="ad555-198">Il costo in termini di allocazione può diventare importante se si allocano e rilasciano continuamente oggetti molto grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-198">In addition, the allocation cost can really add up if you keep allocating and letting go of really large objects.</span></span>

- <span data-ttu-id="ad555-199">Elementi di matrice con tipi di riferimento.</span><span class="sxs-lookup"><span data-stu-id="ad555-199">Array elements with reference types.</span></span>

   <span data-ttu-id="ad555-200">Gli oggetti molto grandi dell'heap oggetti grandi sono normalmente costituiti da matrici (è poco comune che un oggetto istanza sia davvero molto grande).</span><span class="sxs-lookup"><span data-stu-id="ad555-200">Very large objects on the LOH are usually arrays (it's very rare to have an instance object that's really large).</span></span> <span data-ttu-id="ad555-201">Se gli elementi della matrice hanno molti riferimenti, questo comporta un costo che non è presente se gli elementi non includono tali riferimenti.</span><span class="sxs-lookup"><span data-stu-id="ad555-201">If the elements of an array are reference-rich, it incurs a cost that is not present if the elements are not reference-rich.</span></span> <span data-ttu-id="ad555-202">Se l'elemento non contiene nessun riferimento, il Garbage Collector non analizza la matrice.</span><span class="sxs-lookup"><span data-stu-id="ad555-202">If the element doesn’t contain any references, the garbage collector doesn’t need to go through the array at all.</span></span> <span data-ttu-id="ad555-203">Se ad esempio si usa una matrice per memorizzare nodi in un albero binario, un metodo di implementazione è la creazione di un riferimento tra i nodi destro e sinistro di un nodo in base ai nodi effettivi:</span><span class="sxs-lookup"><span data-stu-id="ad555-203">For example, if you use an array to store nodes in a binary tree, one way to implement it is to refer to a node’s right and left node by the actual nodes:</span></span>

   ```csharp
   class Node
   {
      Data d;
      Node left;
      Node right;
   };

   Node[] binary_tr = new Node [num_nodes];
   ```

   <span data-ttu-id="ad555-204">Se `num_nodes` è molto grande, il Garbage Collector deve elaborare almeno due riferimenti per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="ad555-204">If `num_nodes` is large, the garbage collector needs to go through at least two references per element.</span></span> <span data-ttu-id="ad555-205">Un approccio alternativo è la memorizzazione dell'indice dei nodi destro e sinistro:</span><span class="sxs-lookup"><span data-stu-id="ad555-205">An alternative approach is to store the index of the right and the left nodes:</span></span>

   ```csharp
   class Node
   {
      Data d;
      uint left_index;
      uint right_index;
   } ;
   ```

   <span data-ttu-id="ad555-206">Anziché fare riferimento ai dati del nodo sinistro come `left.d` si fa riferimento a tali dati come `binary_tr[left_index].d`.</span><span class="sxs-lookup"><span data-stu-id="ad555-206">Instead of referring the left node’s data as `left.d`, you refer to it as `binary_tr[left_index].d`.</span></span> <span data-ttu-id="ad555-207">Il Garbage Collector non deve verificare riferimenti per i nodi sinistro e destro.</span><span class="sxs-lookup"><span data-stu-id="ad555-207">And the garbage collector doesn’t need to look at any references for the left and right node.</span></span>

<span data-ttu-id="ad555-208">Fra i tre fattori, i primi due sono in genere più significativi del terzo.</span><span class="sxs-lookup"><span data-stu-id="ad555-208">Out of the three factors, the first two are usually more significant than the third.</span></span> <span data-ttu-id="ad555-209">Per questo motivo è consigliabile allocare un pool di oggetti grandi da usare più volte anziché allocare oggetti temporanei.</span><span class="sxs-lookup"><span data-stu-id="ad555-209">Because of this, we recommend that you allocate a pool of large objects that you reuse instead of allocating temporary ones.</span></span> 

## <a name="collecting-performance-data-for-the-loh"></a><span data-ttu-id="ad555-210">Raccolta di dati sulle prestazioni per l'heap oggetti grandi</span><span class="sxs-lookup"><span data-stu-id="ad555-210">Collecting performance data for the LOH</span></span>

<span data-ttu-id="ad555-211">Prima di raccogliere dati sulle prestazioni per un'area specifica, è necessario aver eseguito le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad555-211">Before you collect performance data for a specific area, you should already have done the following:</span></span>

1. <span data-ttu-id="ad555-212">Dimostrare che è necessario analizzare l'area in questione.</span><span class="sxs-lookup"><span data-stu-id="ad555-212">Found evidence that you should be looking at this area.</span></span>

1. <span data-ttu-id="ad555-213">Esaminare altre aree note senza trovare elementi che possono spiegare il problema di prestazioni rilevato.</span><span class="sxs-lookup"><span data-stu-id="ad555-213">Exhausted other areas that you know of without finding anything that could explain the performance problem you saw.</span></span>

<span data-ttu-id="ad555-214">Vedere il blog [Understand the problem before you try to find a solution](https://blogs.msdn.microsoft.com/maoni/2006/09/01/understand-the-problem-before-you-try-to-find-a-solution/) (Comprendere il problema prima di cercare una soluzione) per altre informazioni sui concetti fondamentali della memoria e della CPU.</span><span class="sxs-lookup"><span data-stu-id="ad555-214">See the blog [Understand the problem before you try to find a solution](https://blogs.msdn.microsoft.com/maoni/2006/09/01/understand-the-problem-before-you-try-to-find-a-solution/) for more information on the fundamentals of memory and the CPU.</span></span>

<span data-ttu-id="ad555-215">Per raccogliere dati sulle prestazioni dell'heap oggetti grandi è possibile usare gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad555-215">You can use the following tools to collect data on LOH performance:</span></span>

- [<span data-ttu-id="ad555-216">Contatori delle prestazioni della memoria CLR .NET</span><span class="sxs-lookup"><span data-stu-id="ad555-216">.NET CLR memory performance counters</span></span>](#net-clr-memory-performance-counters)

- [<span data-ttu-id="ad555-217">Eventi ETW</span><span class="sxs-lookup"><span data-stu-id="ad555-217">ETW events</span></span>](#etw-events)

- [<span data-ttu-id="ad555-218">Un debugger</span><span class="sxs-lookup"><span data-stu-id="ad555-218">A debugger</span></span>](#a-debugger)

### <a name="net-clr-memory-performance-counters"></a><span data-ttu-id="ad555-219">Contatori delle prestazioni della memoria CLR .NET</span><span class="sxs-lookup"><span data-stu-id="ad555-219">.NET CLR Memory Performance counters</span></span>

<span data-ttu-id="ad555-220">Questi contatori delle prestazioni sono in genere un buon primo passo nell'analisi dei problemi di prestazioni (anche se Microsoft consiglia l'uso degli [eventi ETW](#etw)).</span><span class="sxs-lookup"><span data-stu-id="ad555-220">These performance counters are usually a good first step in investigating performance issues (although we recommend that you use [ETW events](#etw)).</span></span> <span data-ttu-id="ad555-221">Configurare Performance Monitor aggiungendo i contatori desiderati, come illustrato nella figura 4.</span><span class="sxs-lookup"><span data-stu-id="ad555-221">You configure Performance Monitor by adding the counters that you want, as Figure 4 shows.</span></span> <span data-ttu-id="ad555-222">I contatori importanti per l'heap oggetti grandi sono:</span><span class="sxs-lookup"><span data-stu-id="ad555-222">The ones that are relevant for the LOH are:</span></span>

- <span data-ttu-id="ad555-223">**\# Raccolte di generazione 2**</span><span class="sxs-lookup"><span data-stu-id="ad555-223">**\# Gen 2 Collections**</span></span>

   <span data-ttu-id="ad555-224">Visualizza il numero di operazioni GC di generazione 2 eseguite dall'avvio del processo.</span><span class="sxs-lookup"><span data-stu-id="ad555-224">Displays the number of times generation 2 GCs have occurred since the process started.</span></span> <span data-ttu-id="ad555-225">Il contatore viene incrementato alla fine di una raccolta di generazione 2 (denominata anche Garbage Collection completa).</span><span class="sxs-lookup"><span data-stu-id="ad555-225">The counter is incremented at the end of a generation 2 collection (also called a full garbage collection).</span></span> <span data-ttu-id="ad555-226">Questo contatore visualizza 'ultimo valore osservato.</span><span class="sxs-lookup"><span data-stu-id="ad555-226">This counter displays the last observed value.</span></span>

- <span data-ttu-id="ad555-227">**Dimensione heap oggetti grandi**</span><span class="sxs-lookup"><span data-stu-id="ad555-227">**Large Object Heap size**</span></span>

   <span data-ttu-id="ad555-228">Visualizza la dimensione corrente in byte dell'heap oggetti grandi, incluso lo spazio disponibile.</span><span class="sxs-lookup"><span data-stu-id="ad555-228">Displays the current size, in bytes, including free space, of the LOH.</span></span> <span data-ttu-id="ad555-229">Questo contatore viene aggiornato alla fine di una Garbage Collection, non a ogni allocazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-229">This counter is updated at the end of a garbage collection, not at each allocation.</span></span>

<span data-ttu-id="ad555-230">Un metodo molto comune per il controllo dei contatori è Performance Monitor (perfmon.exe).</span><span class="sxs-lookup"><span data-stu-id="ad555-230">A common way to look at performance counters is with Performance Monitor (perfmon.exe).</span></span> <span data-ttu-id="ad555-231">Usare "Aggiungi contatori" per aggiungere il contatore corrispondente ai processi che interessano.</span><span class="sxs-lookup"><span data-stu-id="ad555-231">Use “Add Counters” to add the interesting counter for processes that you care about.</span></span> <span data-ttu-id="ad555-232">I dati del contatore delle prestazioni possono essere salvati in un file di registro, come indicato nella figura 4.</span><span class="sxs-lookup"><span data-stu-id="ad555-232">You can save the performance counter data to a log file, as Figure 4 shows.</span></span>

![Figura 4: Aggiunta di contatori delle prestazioni.](media/loh/perfcounter.png)    
<span data-ttu-id="ad555-234">Figura 4: LOH dopo un'operazione GC di generazione 2</span><span class="sxs-lookup"><span data-stu-id="ad555-234">Figure 4: The LOH after a generation 2 GC</span></span>

<span data-ttu-id="ad555-235">È anche possibile eseguire query sui contatori delle prestazioni a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="ad555-235">Performance counters can also be queried programmatically.</span></span> <span data-ttu-id="ad555-236">Molti utenti raccolgono i dati con questa modalità come parte del processo di test di routine.</span><span class="sxs-lookup"><span data-stu-id="ad555-236">Many people collect them this way as part of their routine testing process.</span></span> <span data-ttu-id="ad555-237">Se vengono identificati contatori con valori anomali, è possibile usare altri mezzi per ottenere dati più dettagliati ai fini dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="ad555-237">When they spot counters with values that are out of the ordinary, they use other means to get more detailed data to help with the investigation.</span></span>

> [!NOTE]
> <span data-ttu-id="ad555-238">È consigliabile usare gli eventi ETW anziché i contatori delle prestazioni, poiché ETW offre informazioni molto più complete.</span><span class="sxs-lookup"><span data-stu-id="ad555-238">We recommend that you to use ETW events instead of performance counters, because ETW provides much richer information.</span></span>

### <a name="etw"></a><span data-ttu-id="ad555-239">ETW</span><span class="sxs-lookup"><span data-stu-id="ad555-239">ETW</span></span>

<span data-ttu-id="ad555-240">Il Garbage Collector offre vari eventi ETW che favoriscono la comprensione delle operazioni dell'heap e del loro scopo.</span><span class="sxs-lookup"><span data-stu-id="ad555-240">The garbage collector provides a rich set of ETW events to help you understand what the heap is doing and why.</span></span> <span data-ttu-id="ad555-241">I post di blog seguenti illustrano come raccogliere e interpretare gli eventi GC con ETW:</span><span class="sxs-lookup"><span data-stu-id="ad555-241">The following blog posts show how to collect and understand GC events with ETW:</span></span>

- [<span data-ttu-id="ad555-242">Eventi ETW - GC - 1 </span><span class="sxs-lookup"><span data-stu-id="ad555-242">GC ETW Events - 1 </span></span>](http://blogs.msdn.com/b/maoni/archive/2014/12/22/gc-etw-events.aspx)

- [<span data-ttu-id="ad555-243">Eventi ETW - GC - 2</span><span class="sxs-lookup"><span data-stu-id="ad555-243">GC ETW Events - 2</span></span>](http://blogs.msdn.com/b/maoni/archive/2014/12/25/gc-etw-events-2.aspx)

- [<span data-ttu-id="ad555-244">Eventi ETW - GC - 3</span><span class="sxs-lookup"><span data-stu-id="ad555-244">GC ETW Events - 3</span></span>](http://blogs.msdn.com/b/maoni/archive/2014/12/25/gc-etw-events-3.aspx) 

- [<span data-ttu-id="ad555-245">Eventi ETW - GC - 4</span><span class="sxs-lookup"><span data-stu-id="ad555-245">GC ETW Events - 4</span></span>](http://blogs.msdn.com/b/maoni/archive/2014/12/30/gc-etw-events-4.aspx)

<span data-ttu-id="ad555-246">Per identificare un numero eccessivo di operazioni GC di generazione 2 causate da allocazioni di heap oggetti grandi temporanee, esaminare la colonna Motivo trigger per le operazioni GC.</span><span class="sxs-lookup"><span data-stu-id="ad555-246">To identify excessive generation 2 GCs caused by temporary LOH allocations, look at the Trigger Reason column for GCs.</span></span> <span data-ttu-id="ad555-247">Per un test semplice che consente di allocare solo oggetti di grandi dimensioni temporanei, è possibile raccogliere informazioni sugli eventi ETW con la riga di comando [PerfView](https://www.microsoft.com/download/details.aspx?id=28567) seguente:</span><span class="sxs-lookup"><span data-stu-id="ad555-247">For a simple test that only allocates temporary large objects, you can collect information on ETW events with the following [PerfView](https://www.microsoft.com/download/details.aspx?id=28567) command line:</span></span>

```console
perfview /GCCollectOnly /AcceptEULA /nogui collect
```

<span data-ttu-id="ad555-248">Il risultato è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ad555-248">The result is something like this:</span></span>
 
![Figura 5: Esame degli eventi ETW con PerfView](media/loh/perfview.png)  
<span data-ttu-id="ad555-250">Figura 5: Eventi ETW visualizzati mediante PerfView</span><span class="sxs-lookup"><span data-stu-id="ad555-250">Figure 5: ETW events shown using PerfView</span></span>

<span data-ttu-id="ad555-251">Si osservi che tutte le operazioni GCs sono di generazione 2 e tutte sono attivate da AllocLarge. Ciò significa che l'operazione GC è stata attivata da un oggetto grande.</span><span class="sxs-lookup"><span data-stu-id="ad555-251">As you can see, all GCs are generation 2 GCs, and they are all triggered by AllocLarge, which means that allocating a large object triggered this GC.</span></span> <span data-ttu-id="ad555-252">Il fatto che si tratti di allocazioni temporanee è indicato dal valore 1% nella colonna **LOH Survival Rate %** (% heap oggetti grandi attivi).</span><span class="sxs-lookup"><span data-stu-id="ad555-252">We know that these allocations are temporary because the **LOH Survival Rate %** column says 1%.</span></span>

<span data-ttu-id="ad555-253">È possibile raccogliere altri eventi ETW che indicano l'origine di allocazione di questi oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-253">You can collect additional ETW events that tell you who allocated these large objects.</span></span> <span data-ttu-id="ad555-254">La riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ad555-254">The following command line:</span></span>

```console
perfview /GCOnly /AcceptEULA /nogui collect
```

<span data-ttu-id="ad555-255">registra un evento AllocationTick ogni 100 KB circa di allocazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-255">collects an AllocationTick event which is fired approximately every 100k worth of allocations.</span></span> <span data-ttu-id="ad555-256">In altre parole viene generato un evento ogni volta che viene allocato un oggetto grande.</span><span class="sxs-lookup"><span data-stu-id="ad555-256">In other words, an event is fired each time a large object is allocated.</span></span> <span data-ttu-id="ad555-257">È quindi possibile esaminare una delle visualizzazioni di allocazione heap GC che includono gli stack di chiamate che hanno allocato oggetti grandi:</span><span class="sxs-lookup"><span data-stu-id="ad555-257">You can then look at one of the GC Heap Alloc views which show you the callstacks that allocated large objects:</span></span>
 
![Figura 6: Visualizzazione di allocazione heap GC](media/loh/perfview2.png)  
<span data-ttu-id="ad555-259">Figura 6: Visualizzazione di allocazione heap GC</span><span class="sxs-lookup"><span data-stu-id="ad555-259">Figure 6: A GC Heap Alloc view</span></span>
 
<span data-ttu-id="ad555-260">Questo test molto semplice esegue solo l'allocazione di oggetti grandi dal relativo metodo `Main`.</span><span class="sxs-lookup"><span data-stu-id="ad555-260">As you can see, this is a very simple test that just allocates large objects from its `Main` method.</span></span>

### <a name="a-debugger"></a><span data-ttu-id="ad555-261">Un debugger</span><span class="sxs-lookup"><span data-stu-id="ad555-261">A debugger</span></span>

<span data-ttu-id="ad555-262">Se è presente solo di un dump di memoria ed è necessario esaminare quali oggetti sono effettivamente inclusi nell'heap oggetti grandi, è possibile usare l'[estensione del debugger SoS](http://msdn2.microsoft.com/ms404370.aspx) disponibile in .NET.</span><span class="sxs-lookup"><span data-stu-id="ad555-262">If all you have is a memory dump and you need to look at what objects are actually on the LOH, you can use the [SoS debugger extension](http://msdn2.microsoft.com/ms404370.aspx) provided by .NET.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad555-263">I comandi di debug indicati in questa sezione sono applicabili ai [debugger di Windows](http://www.microsoft.com/whdc/devtools/debugging/default.mspx).</span><span class="sxs-lookup"><span data-stu-id="ad555-263">The debugging commands mentioned in this section are applicable to the [Windows Debuggers](http://www.microsoft.com/whdc/devtools/debugging/default.mspx).</span></span>

<span data-ttu-id="ad555-264">Il codice seguente visualizza un output di esempio dell'analisi dell'heap oggetti grandi:</span><span class="sxs-lookup"><span data-stu-id="ad555-264">The following shows sample output from analyzing the LOH:</span></span>

```
0:003> .loadby sos mscorwks
0:003> !eeheap -gc
Number of GC Heaps: 1
generation 0 starts at 0x013e35ec
sdgeneration 1 starts at 0x013e1b6c
generation 2 starts at 0x013e1000
ephemeral segment allocation context: none
segment   begin allocated     size
0018f2d0 790d5588 790f4b38 0x0001f5b0(128432)
013e0000 013e1000 013e35f8 0x000025f8(9720)
Large object heap starts at 0x023e1000
segment   begin allocated     size
023e0000 023e1000 033db630 0x00ffa630(16754224)
033e0000 033e1000 043cdf98 0x00fecf98(16699288)
043e0000 043e1000 05368b58 0x00f87b58(16284504)
Total Size 0x2f90cc8(49876168)
------------------------------
GC Heap Size 0x2f90cc8(49876168)
0:003> !dumpheap -stat 023e1000 033db630
total 133 objects
Statistics:
MT   Count   TotalSize Class Name
001521d0       66     2081792     Free
7912273c       63     6663696 System.Byte[]
7912254c       4     8008736 System.Object[]
Total 133 objects
```

<span data-ttu-id="ad555-265">Le dimensioni dell'heap oggetti grandi sono (16.754.224 + 16.699.288 + 16.284.504) = 49.738.016 byte.</span><span class="sxs-lookup"><span data-stu-id="ad555-265">The LOH heap size is (16,754,224 + 16,699,288 + 16,284,504) = 49,738,016 bytes.</span></span> <span data-ttu-id="ad555-266">Tra gli indirizzi 023e1000 e 033db630, 8.008.736 byte sono occupati da una matrice di oggetti <xref:System.Object?displayProperty=fullName>, 6.663.696 byte sono occupati da una matrice di oggetti <xref:System.Byte?displayProperty=nameWithType> e 2.081.792 byte sono occupati da spazio libero.</span><span class="sxs-lookup"><span data-stu-id="ad555-266">Between addresses 023e1000 and 033db630, 8,008,736 bytes are occupied by an array of <xref:System.Object?displayProperty=fullName> objects, 6,663,696 bytes are occupied by an array of <xref:System.Byte?displayProperty=nameWithType>  objects, and 2,081,792 bytes are occupied by free space.</span></span>

<span data-ttu-id="ad555-267">A volte il debugger indica che le dimensioni totali dell'heap oggetti grandi sono inferiori a 85.000 byte.</span><span class="sxs-lookup"><span data-stu-id="ad555-267">Sometimes, the debugger shows that the total size of the LOH is less than 85,000 bytes.</span></span> <span data-ttu-id="ad555-268">Il motivo è che il runtime stesso usa l'heap oggetti grandi per allocare alcuni oggetti di dimensioni inferiori a quelle di un oggetto grande.</span><span class="sxs-lookup"><span data-stu-id="ad555-268">This happens because the runtime itself uses the LOH to allocate some objects that are smaller than a large object.</span></span>

<span data-ttu-id="ad555-269">Poiché l'heap oggetti grandi non è compattato, si può pensare che sia all'origine della frammentazione.</span><span class="sxs-lookup"><span data-stu-id="ad555-269">Because the LOH is not compacted, sometimes the LOH is thoought to be the source of fragmentation.</span></span> <span data-ttu-id="ad555-270">Frammentazione significa:</span><span class="sxs-lookup"><span data-stu-id="ad555-270">Fragmentation means:</span></span>

- <span data-ttu-id="ad555-271">Frammentazione dell'heap gestito, indicata dalla quantità di spazio disponibile tra gli oggetti gestiti.</span><span class="sxs-lookup"><span data-stu-id="ad555-271">Fragmentation of the managed heap, which is indicated by the amount of free space between managed objects.</span></span> <span data-ttu-id="ad555-272">In SoS il comando `!dumpheap –type Free` visualizza la quantità di spazio disponibile tra gli oggetti gestiti.</span><span class="sxs-lookup"><span data-stu-id="ad555-272">In SoS, the `!dumpheap –type Free` command displays the amount of free space between managed objects.</span></span>

- <span data-ttu-id="ad555-273">Frammentazione dello spazio indirizzi della memoria virtuale (VM), la memoria contrassegnata come `MEM_FREE`.</span><span class="sxs-lookup"><span data-stu-id="ad555-273">Fragmentation of the virtual memory (VM) address space, which is the memory marked as `MEM_FREE`.</span></span> <span data-ttu-id="ad555-274">È possibile ottenerla con vari comandi del debugger in windbg.</span><span class="sxs-lookup"><span data-stu-id="ad555-274">You can get it by using various debugger commands in windbg.</span></span>

   <span data-ttu-id="ad555-275">L'esempio seguente visualizza la frammentazione nello spazio della memoria virtuale:</span><span class="sxs-lookup"><span data-stu-id="ad555-275">The following example shows fragmentation in the VM space:</span></span>

   ```
   0:000> !address
   00000000 : 00000000 - 00010000
   Type     00000000
   Protect 00000001 PAGE_NOACCESS
   State   00010000 MEM_FREE
   Usage   RegionUsageFree
   00010000 : 00010000 - 00002000
   Type     00020000 MEM_PRIVATE
   Protect 00000004 PAGE_READWRITE
   State   00001000 MEM_COMMIT
   Usage   RegionUsageEnvironmentBlock
   00012000 : 00012000 - 0000e000
   Type     00000000
   Protect 00000001 PAGE_NOACCESS
   State   00010000 MEM_FREE
   Usage   RegionUsageFree
   … [omitted]
   -------------------- Usage SUMMARY --------------------------
   TotSize (     KB)   Pct(Tots) Pct(Busy)   Usage
   701000 (   7172) : 00.34%   20.69%   : RegionUsageIsVAD
   7de15000 ( 2062420) : 98.35%   00.00%   : RegionUsageFree
   1452000 (   20808) : 00.99%   60.02%   : RegionUsageImage
   300000 (   3072) : 00.15%   08.86%   : RegionUsageStack
   3000 (     12) : 00.00%   00.03%   : RegionUsageTeb
   381000 (   3588) : 00.17%   10.35%   : RegionUsageHeap
   0 (       0) : 00.00%   00.00%   : RegionUsagePageHeap
   1000 (       4) : 00.00%   00.01%   : RegionUsagePeb
   1000 (       4) : 00.00%   00.01%   : RegionUsageProcessParametrs
   2000 (       8) : 00.00%   00.02%   : RegionUsageEnvironmentBlock
   Tot: 7fff0000 (2097088 KB) Busy: 021db000 (34668 KB)

   -------------------- Type SUMMARY --------------------------
   TotSize (     KB)   Pct(Tots) Usage
   7de15000 ( 2062420) : 98.35%   : <free>
   1452000 (   20808) : 00.99%   : MEM_IMAGE
   69f000 (   6780) : 00.32%   : MEM_MAPPED
   6ea000 (   7080) : 00.34%   : MEM_PRIVATE

   -------------------- State SUMMARY --------------------------
   TotSize (     KB)   Pct(Tots) Usage
   1a58000 (   26976) : 01.29%   : MEM_COMMIT
   7de15000 ( 2062420) : 98.35%   : MEM_FREE
   783000 (   7692) : 00.37%   : MEM_RESERVE

   Largest free region: Base 01432000 - Size 707ee000 (1843128 KB)
   ```

<span data-ttu-id="ad555-276">È più comune osservare la frammentazione della memoria virtuale causata da oggetti grandi temporanei, che richiedono a Garbage Collector di acquisire frequentemente nuovi segmenti di heap gestiti dal sistema operativo e di restituire quelli vuoti e liberati.</span><span class="sxs-lookup"><span data-stu-id="ad555-276">It’s more common to see VM fragmentation caused by temporary large objects that require the garbage collector to frequently acquire new managed heap segments from the OS and to release empty ones back to the OS.</span></span>

<span data-ttu-id="ad555-277">Per verificare se l'heap oggetti grandi è la causa della frammentazione della memoria virtuale, è possibile impostare un punto di interruzione su [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx) e [VirtualFree](https://msdn.microsoft.com/library/windows/desktop/aa366892(v=vs.85).aspx) per vedere quale entità chiama questi processi.</span><span class="sxs-lookup"><span data-stu-id="ad555-277">To verify whether the LOH is causing VM fragmentation, you can set a breakpoint on [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx) and [VirtualFree](https://msdn.microsoft.com/library/windows/desktop/aa366892(v=vs.85).aspx) to see who call them.</span></span> <span data-ttu-id="ad555-278">Ad esempio, per vedere quale entità ha provato ad allocare blocchi di memoria virtuale del sistema operativo di dimensioni superiori a 8 MB, è possibile impostare un punto di interruzione simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ad555-278">For example, to see who tried to allocate virtual memory chunks larger than 8MBB from the OS, you can set a breakpoint like this:</span></span>

```console
bp kernel32!virtualalloc "j (dwo(@esp+8)>800000) 'kb';'g'"
```

<span data-ttu-id="ad555-279">Questo comando apre il debugger e visualizza lo stack di chiamate solo se [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx) viene chiamata con una dimensione di allocazione superiore a 8 MB (0x800000).</span><span class="sxs-lookup"><span data-stu-id="ad555-279">This command breaks into the debugger and shows the callstack only if [VirtualAlloc](https://msdn.microsoft.com/library/windows/desktop/aa366887(v=vs.85).aspx) is called with an allocation size greater than 8MB (0x800000).</span></span>

<span data-ttu-id="ad555-280">In CLR 2.0 la nuova funzionalità *VM Hoarding* (Accumulo in memoria virtuale) può essere utile in situazioni con acquisizione e rilascio frequente di oggetti, ad esempio nell'heap oggetti piccoli e nell'heap oggetti grandi.</span><span class="sxs-lookup"><span data-stu-id="ad555-280">CLR 2.0 added a feature called *VM Hoarding* that can be useful for scenarious where segments (including on the large and small object heaps) are frequently acquired and released.</span></span> <span data-ttu-id="ad555-281">Per impostare VM Hoarding si specifica un flag di avvio chiamato `STARTUP_HOARD_GC_VM` tramite l'API di hosting.</span><span class="sxs-lookup"><span data-stu-id="ad555-281">To specify VM Hoarding, you specify a startup flag called `STARTUP_HOARD_GC_VM` via the hosting API.</span></span> <span data-ttu-id="ad555-282">Invece di rilasciare i segmenti vuoti per restituirli al sistema operativo, CLR libera la memoria in questi segmenti e li inserisce in un elenco di standby.</span><span class="sxs-lookup"><span data-stu-id="ad555-282">Instead of releasing empty segments back to the OS, the CLR decommits the memory on these segments and puts them on a standby list.</span></span> <span data-ttu-id="ad555-283">Si noti che CLR non esegue questa operazione per segmenti troppo grandi. CLR usa i segmenti in un secondo momento per soddisfare nuove richieste di segmenti.</span><span class="sxs-lookup"><span data-stu-id="ad555-283">(Note that the CLR doesn't do this for segments that are too large.) The CLR later uses those segments to satisfy new segment requests.</span></span> <span data-ttu-id="ad555-284">Quando l'app torna a richiedere un nuovo segmento, CLR usa un segmento di questo elenco di standby, se è disponibile un segmento abbastanza grande.</span><span class="sxs-lookup"><span data-stu-id="ad555-284">The next time that your app needs a new segment, the CLR uses one from this standby list if it can find one that’s big enough.</span></span>

<span data-ttu-id="ad555-285">La funzionalità VM Hoarding è anche utile per le applicazioni che desiderano mantenere i segmenti già acquisiti ed evitare eccezioni di memoria insufficiente, ad esempio le applicazioni server essenziali in esecuzione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="ad555-285">VM hoarding is also useful for applications that want to hold onto the segments that they already acquired, such as some server apps that are the dominant apps running on the system, to avoid out of memory exceptions.</span></span>

<span data-ttu-id="ad555-286">Quando si usa questa funzionalità è consigliabile sottoporre a test accurati l'applicazione, per garantire che l'uso della memoria sia sufficientemente stabile.</span><span class="sxs-lookup"><span data-stu-id="ad555-286">We strongly recommend that you carefully test your application when you use this feature to ensure your application has fairly stable memory usage.</span></span>