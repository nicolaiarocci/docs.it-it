---
title: 'Procedura: Comprimere ed estrarre file'
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET Framework], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9a4ea4c32f5b73b283a5982f16e55a4d078171c1
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55255003"
---
# <a name="how-to-compress-and-extract-files"></a>Procedura: Comprimere ed estrarre file

Lo spazio dei nomi <xref:System.IO.Compression> contiene i tipi seguenti per la compressione e la decompressione di file e flussi. È possibile usare questi tipi anche per leggere e modificare il contenuto di un file compresso.

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

Gli esempi seguenti mostrano alcune delle operazioni che è possibile eseguire con i file compressi.

## <a name="example-1-create-and-extract-a-zip-file"></a>Esempio 1: creare ed estrarre un file con estensione zip

Nell'esempio seguente viene illustrato come creare ed estrarre un file *ZIP* compresso usando la classe <xref:System.IO.Compression.ZipFile>. L'esempio comprime il contenuto di una cartella in un nuovo file *ZIP* e quindi estrae il contenuto in una nuova cartella. 

Per eseguire l'esempio, creare una cartella *start* nella cartella del programma e copiarvi i file da comprimere. 

Se viene visualizzato l'errore di compilazione "Il nome 'ZipFile' non esiste nel contesto corrente", aggiungere un riferimento all'assembly `System.IO.Compression.FileSystem` nel progetto.

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a>Esempio 2: estrarre estensioni di file specifiche

Il prossimo esempio mostra come eseguire l'iterazione del contenuto di un file *ZIP* esistente ed estrarre i file con estensione *txt*. Usa la classe <xref:System.IO.Compression.ZipArchive> per accedere al file ZIP e la classe <xref:System.IO.Compression.ZipArchiveEntry> per controllare le singole voci. Il metodo di estensione <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> per l'oggetto <xref:System.IO.Compression.ZipArchiveEntry> è disponibile nella classe <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType>. 

Per eseguire l'esempio, inserire un file *ZIP* denominato *result.zip* nella cartella del programma. Quando richiesto, specificare un nome di cartella in cui estrarre i file. 

Se viene visualizzato l'errore di compilazione "Il nome 'ZipFile' non esiste nel contesto corrente", aggiungere un riferimento all'assembly `System.IO.Compression.FileSystem` nel progetto.

Se viene visualizzato l'errore "Il tipo 'ZipArchive' è definito in un assembly di cui manca il riferimento", aggiungere un riferimento all'assembly `System.IO.Compression` al progetto. 

> [!IMPORTANT]
> Quando si decomprimono i file, è necessario cercare percorsi dannosi che possono sfuggire alla directory in cui si esegue la decompressione. Si tratta di un attacco noto come attacco path traversal. L'esempio seguente illustra come verificare la presenza di percorsi file dannosi e offre un metodo sicuro per la decompressione.

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a>Esempio 3: Aggiungere un file a un file ZIP esistente

L'esempio seguente usa la classe <xref:System.IO.Compression.ZipArchive> per accedere a un file *ZIP* esistente e aggiunge un nuovo file al file compresso. Il nuovo file viene compresso quando lo si aggiunge al file ZIP esistente.

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a>Esempio 4: Comprimere e decomprimere file con estensione gz

È possibile usare anche le classi <xref:System.IO.Compression.GZipStream> e <xref:System.IO.Compression.DeflateStream> per comprimere e decomprimere dati. Queste due classi usano lo stesso algoritmo di compressione. È possibile decomprimere gli oggetti <xref:System.IO.Compression.GZipStream> scritti in un file con estensione *gz* con molti strumenti comuni. L'esempio seguente illustra come comprimere e decomprimere una directory di file usando la classe <xref:System.IO.Compression.GZipStream>:

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a>Vedere anche

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [I/O di file e di flussi](../../../docs/standard/io/index.md)
