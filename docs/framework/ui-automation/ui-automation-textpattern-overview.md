---
title: Cenni preliminari sul modello TextPattern di automazione interfaccia utente
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, TextPattern class
- TextPattern class
- classes, TextPattern
ms.assetid: 41787927-df1f-4f4a-aba3-641662854fc4
ms.openlocfilehash: d35e5b5127f335eac04caa8ee95749f45cb870bf
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674003"
---
# <a name="ui-automation-textpattern-overview"></a>Cenni preliminari sul modello TextPattern di automazione interfaccia utente

> [!NOTE]
> Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate sulle [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: Automazione interfaccia utente](https://go.microsoft.com/fwlink/?LinkID=156746).

In questa panoramica viene descritto come usare [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] per esporre il contenuto testuale, inclusi attributi di stile e formato, di controlli di testo in [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], per le piattaforme supportate. Questi controlli includono, ma non sono limitati a, Microsoft .NET Framework <xref:System.Windows.Controls.TextBox> e <xref:System.Windows.Controls.RichTextBox> così come gli [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] equivalenti.

L'esposizione del contenuto testuale di un controllo viene effettuata tramite l'uso del pattern di controllo <xref:System.Windows.Automation.TextPattern> , che rappresenta il contenuto di un contenitore di testo come flusso di testo. A sua volta, l'oggetto <xref:System.Windows.Automation.TextPattern> richiede il supporto della classe <xref:System.Windows.Automation.Text.TextPatternRange> per esporre attributi di stile e formato. <xref:System.Windows.Automation.Text.TextPatternRange> supporta <xref:System.Windows.Automation.TextPattern> rappresentando intervalli di testo contigui e non in un contenitore di testo con una raccolta di endpoint <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> r <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> . <xref:System.Windows.Automation.Text.TextPatternRange> supporta funzionalità, quali la selezione, il confronto, il recupero e l'attraversamento.

> [!NOTE]
> Le classi <xref:System.Windows.Automation.TextPattern> non consentono di inserire o modificare testo. Tuttavia, a seconda del controllo, questo può essere eseguito per il [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] <xref:System.Windows.Automation.ValuePattern> o tramite input diretto della tastiera. Per un esempio, vedere [TextPattern Insert Text Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InsertText) .

La funzionalità descritta in questa panoramica è fondamentale per i fornitori di tecnologie per l'accessibilità e per gli utenti finali. Le tecnologie per l'accessibilità possono usare [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] per raccogliere informazioni complete sulla formattazione del testo per l'utente e fornire spostamento a livello di codice e selezione del testo dall'oggetto <xref:System.Windows.Automation.Text.TextUnit> (carattere, parola, riga o paragrafo).

<a name="UI_Automation_TextPattern_vs__Cicero"></a>

## <a name="ui-automation-textpattern-vs-text-services-framework"></a>TextPattern di automazione interfaccia utente e Text Services Framework

[!INCLUDE[TLA#tla_tsf](../../../includes/tlasharptla-tsf-md.md)] è un framework di sistema semplice e scalabile che abilita servizi per linguaggi naturali e input di testo avanzato sul desktop e all'interno di applicazioni. Oltre a fornire interfacce per consentire alle applicazioni di esporre i relativi archivi di testo, supporta anche i metadati per tali archivi.

Tuttavia, [!INCLUDE[TLA2#tla_tsf](../../../includes/tla2sharptla-tsf-md.md)] è stato progettato per applicazioni che richiedono l'immissione di input in scenari in grado di riconoscere il contesto, mentre <xref:System.Windows.Automation.TextPattern> è una soluzione di sola lettura (con la soluzione alternativa limitata indicata sopra) che ha lo scopo di fornire accesso ottimizzato a un archivio di testo per utilità per la lettura e dispositivi Braille.

In breve, le tecnologie accessibili che richiedono accesso in sola lettura a un archivio di testo possono usare <xref:System.Windows.Automation.TextPattern>, ma sarà necessaria la funzionalità più complessa di [!INCLUDE[TLA2#tla_tsf](../../../includes/tla2sharptla-tsf-md.md)] per input che riconoscano il contesto.

<a name="Control_Types"></a>

## <a name="control-types"></a>Tipi di controllo

#### <a name="text"></a>Testo

Il controllo Text è l'elemento di base che rappresenta una sezione di testo sullo schermo.

Un controllo Text autonomo può essere usato come etichetta o testo statico in un form. I controlli Text possono anche essere contenuti all'interno della struttura di un oggetto <xref:System.Windows.Automation.ControlType.ListItem>, <xref:System.Windows.Automation.ControlType.TreeItem> o <xref:System.Windows.Automation.ControlType.DataItem>.

> [!NOTE]
> Non è possibile visualizzare i controlli Text nella visualizzazione contenuto dell'albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] (vedere [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)). Ciò è dovuto al fatto che i controlli di testo sono spesso visualizzati tramite la proprietà Name di un altro controllo. Ad esempio, il testo usato per etichettare un controllo Edit viene esposto tramite la proprietà Name del controllo Edit. Poiché il controllo Edit si trova nella visualizzazione contenuto della struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , non è necessario che l'elemento di testo stesso si trovi in tale visualizzazione della struttura ad albero di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] . Nella visualizzazione contenuto viene visualizzato solo il testo non ridondante. In questo modo, qualsiasi tecnologia per l’accessibilità è in grado di filtrare rapidamente solo le informazioni necessarie agli utenti.

#### <a name="edit"></a>Modifica

I controlli Edit consentono agli utenti di visualizzare e modificare una sola riga di testo.

> [!NOTE]
> In alcuni scenari di layout, una singola riga di testo può essere interrotta da un ritorno a capo.

#### <a name="document"></a>Documento

I controlli Document consentono a un utente di spostarsi e ottenere informazioni da più pagine di testo.

<a name="TextPattern_Client_API_s"></a>

## <a name="textpattern-client-apis"></a>API Client TextPattern

|||
|-|-|
|`System.Windows.Automation.TextPattern Class`|Il punto di ingresso per il modello di testo di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] <br /><br /> Questa classe contiene inoltre i due listener di eventi di <xref:System.Windows.Automation.TextPattern> , <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent> e <xref:System.Windows.Automation.TextPattern.TextChangedEvent>.|
|`System.Windows.Automation.Text.TextPatternRange Class`|La rappresentazione di una sezione di testo all'interno di un contenitore di testo che supporta <xref:System.Windows.Automation.TextPattern>.<br /><br /> I client di automazione interfaccia utente devono valutare con attenzione la validità corrente di un intervallo di testo creato usando <xref:System.Windows.Automation.Text.TextPatternRange>. Se il testo originale nel controllo di testo è completamente sostituito da testo nuovo, l'intervallo di testo corrente non è più valido. L'intervallo di testo, tuttavia, può essere ancora attendibile se viene modificata solo una parte del testo originale e il controllo di testo sottostante gestisce il "puntatore" di testo con ancoraggi (o endpoint), anziché mediante il posizionamento di carattere assoluto.<br /><br /> I client possono restare in ascolto di un oggetto <xref:System.Windows.Automation.TextPattern.TextChangedEvent> per la notifica di qualsiasi modifica apportata al contenuto testuale usato.|
|`System.Windows.Automation.AutomationTextAttribute Class`|Usato per identificare gli attributi di formattazione di un intervallo di testo.|

<a name="TextPattern_Provider_API_s"></a>

## <a name="textpattern-provider-apis"></a>API del Provider TextPattern

Gli elementi o i controlli dell'interfaccia utente che supportano <xref:System.Windows.Automation.TextPattern> mediante l'implementazione delle interfacce <xref:System.Windows.Automation.Provider.ITextProvider> e <xref:System.Windows.Automation.Provider.ITextRangeProvider> , in modo nativo o tramite i proxy di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] , consentono di esporre informazioni dettagliate sugli attributi per qualsiasi testo contenuto oltre a fornire funzionalità di esplorazione affidabili.

Non è necessario che un provider <xref:System.Windows.Automation.TextPattern> supporti tutti gli attributi di testo se il controllo non offre il supporto per determinati attributi.

Un provider <xref:System.Windows.Automation.TextPattern> deve supportare le funzioni <xref:System.Windows.Automation.TextPattern.GetSelection%2A> e <xref:System.Windows.Automation.Text.TextPatternRange.Select%2A> se il controllo supporta la selezione di testo o il posizionamento del cursore di testo (o cursore di sistema) all'interno dell'area di testo. Se il controllo non supporta questa funzionalità, non è necessario il supporto di questi metodi. Il controllo deve tuttavia esporre il tipo di selezione di testo supportato implementando la proprietà <xref:System.Windows.Automation.Provider.ITextProvider.SupportedTextSelection%2A> .

Un provider <xref:System.Windows.Automation.TextPattern> deve supportare sempre le costanti <xref:System.Windows.Automation.Text.TextUnit> e <xref:System.Windows.Automation.Text.TextUnit.Character> di <xref:System.Windows.Automation.Text.TextUnit.Document> così come qualsiasi altra costante di <xref:System.Windows.Automation.Text.TextUnit> che è in grado di supportare.

> [!NOTE]
> Il provider può ignorare il supporto per un oggetto <xref:System.Windows.Automation.Text.TextUnit> specifico rinviando al successivo oggetto <xref:System.Windows.Automation.Text.TextUnit> più grande supportato nell'ordine seguente: <xref:System.Windows.Automation.Text.TextUnit.Character>, <xref:System.Windows.Automation.Text.TextUnit.Format>, <xref:System.Windows.Automation.Text.TextUnit.Word>, <xref:System.Windows.Automation.Text.TextUnit.Line>, <xref:System.Windows.Automation.Text.TextUnit.Paragraph>, <xref:System.Windows.Automation.Text.TextUnit.Page>e <xref:System.Windows.Automation.Text.TextUnit.Document>.

|||
|-|-|
|`ITextProvider Interface`|Espone metodi, proprietà e attributi che supportano <xref:System.Windows.Automation.TextPattern> nelle applicazioni client (vedere <xref:System.Windows.Automation.Provider.ITextProvider>).|
|`ITextRangeProvider Interface`|Rappresenta una selezione di testo in un provider di testo (vedere <xref:System.Windows.Automation.Provider.ITextRangeProvider>).|
|`System.Windows.Automation.TextPatternIdentifiers Class`|Contiene valori usati come identificatori per i provider di testo (vedere <xref:System.Windows.Automation.TextPatternIdentifiers>).|

<a name="Security"></a>
## <a name="security"></a>Sicurezza
 Le classi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] è stata progettata con l'obiettivo della sicurezza (vedere [UI Automation Security Overview](../../../docs/framework/ui-automation/ui-automation-security-overview.md)). Le classi TextPattern descritte in questa panoramica, tuttavia richiedono alcune considerazioni specifiche relative alla sicurezza.

- I provider di testo di[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] forniscono interfacce di sola lettura, non la possibilità di modificare il testo esistente in un controllo.

- I client di automazione interfaccia utente possono usare [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] solo se sono completamente attendibili. Un esempio è dato da un computer di accesso protetto, in cui è possibile eseguire solo applicazioni note e attendibili.

- È importante che gli sviluppatori di provider di automazione interfaccia utente siano consapevoli che tutte le informazioni esposte nei controlli tramite [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] sono essenzialmente pubbliche e completamente accessibili da altro codice. In[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] non viene determinata in alcun modo l'attendibilità dei client di automazione interfaccia utente; pertanto è importante che il provider di automazione interfaccia utente non esponga contenuto protetto né informazioni testuali sensibili, ad esempio campi password.

- Una delle modifiche più significative in materia di sicurezza introdotte in [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] è nota come "Input sicuro" e include tecnologie quali LUA (account utente con limitazioni) e UIPI (UI Privilege Level Isolation).

    - UIPI impedisce a un programma di controllare e/o monitorare un altro programma con privilegi superiori, impedendo attacchi di messaggi di finestra tra processi che effettuano lo spoofing dell'input dell'utente.

    - Con LUA vengono impostati limiti sui privilegi delle applicazioni eseguite dagli utenti del gruppo Administrators. Alle applicazioni non saranno assegnati privilegi amministratori, ma verranno invece eseguite con i privilegi minimi necessari. Di conseguenza, è possibile che negli scenari LUA vengano applicate alcune restrizioni. Tra le più significative, il troncamento delle stringhe (incluse le stringhe TextPattern) che può prevedere la limitazione delle dimensioni delle stringhe recuperate dalle applicazioni a livello di amministratore, per evitare la necessità di allocare memoria con la conseguente disabilitazione dell'applicazione.

<a name="Performance"></a>

## <a name="performance"></a>Prestazioni

Poiché la maggior parte delle funzionalità di TextPattern si basa sulle chiamate tra processi, non offre un meccanismo di memorizzazione nella cache per migliorare le prestazioni durante l'elaborazione di contenuto. Questa condizione è diversa rispetto ad altri pattern di controllo di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] che consentono l'accesso tramite il metodo <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> o <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> .

Per migliorare le prestazioni, è possibile assicurarsi che i client di automazione interfaccia utente provino a recuperare blocchi di testo di dimensioni moderate tramite il metodo <xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>. Ad esempio, le chiamate GetText(1) generano riscontri tra processi per ogni carattere, mentre una chiamata GetText(-1) genera un riscontro tra processi, ma può avere una latenza elevata a seconda delle dimensioni del provider di testo.

<a name="Glossary"></a>

## <a name="textpattern-terminology"></a>Terminologia di TextPattern

**Attributo** una caratteristica di formattazione di un intervallo di testo (ad esempio <xref:System.Windows.Automation.TextPattern.IsItalicAttribute> o <xref:System.Windows.Automation.TextPattern.FontNameAttribute>).

**Intervallo degenerato** un intervallo degenerato è un intervallo di testo vuoto o con zero caratteri. Ai fini del pattern di controllo TextPattern, il punto di inserimento del testo (o cursore di sistema) è considerato un intervallo degenerato. Se non viene selezionato testo, il metodo <xref:System.Windows.Automation.TextPattern.GetSelection%2A> restituisce un intervallo degenerato in corrispondenza del punto di inserimento del testo e il metodo <xref:System.Windows.Automation.TextPattern.RangeFromPoint%2A> restituisce un intervallo degenerato come endpoint iniziale. I metodi<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> e <xref:System.Windows.Automation.TextPattern.GetVisibleRanges%2A> possono restituire intervalli degenerati quando il provider di testo non è in grado di trovare alcun intervallo di testo corrispondente alla condizione specificata. È possibile usare questo intervallo degenerato come endpoint iniziale all'interno del provider di testo. <xref:System.Windows.Automation.Text.TextPatternRange.FindText%2A> e <xref:System.Windows.Automation.Text.TextPatternRange.FindAttribute%2A> restituire un riferimento null (`Nothing` in Microsoft Visual Basic .NET) per evitare confusione con un intervallo individuato e un intervallo degenere.

**Oggetto incorporato** esistono due tipi di oggetti incorporati nel [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] modello di testo. Sono costituiti da elementi di contenuto basati su testo, quali collegamenti ipertestuali o tabelle, e da elementi di controllo, quali immagini e pulsanti. Per altre informazioni, vedere [Access Embedded Objects Using UI Automation](../../../docs/framework/ui-automation/access-embedded-objects-using-ui-automation.md).

**Endpoint** assoluto <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> o <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> punto di un intervallo di testo all'interno di un contenitore di testo.

![TextPatternRangeEndpoint &#40;iniziare e terminare&#41;. ](../../../docs/framework/ui-automation/media/uia-textpattern-endpoints.PNG "UIA_TextPattern_Endpoints") seguente illustra un gruppo di punti iniziali e finali.

**TextRange** una rappresentazione di un intervallo di testo, con punti iniziale e finale, in un contenitore di testo, inclusi tutti i relativi attributi e funzionalità.

<xref:System.Windows.Automation.Text.TextUnit> Unità di testo (carattere, parola, riga o paragrafo) usata per lo spostamento tramite segmenti logici di un intervallo di testo predefinite.

## <a name="see-also"></a>Vedere anche

- [Pattern di controllo di automazione interfaccia utente per i client](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
- [Panoramica dei pattern di controllo per l'automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)
- [Panoramica dell'albero di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)
- [Usare la memorizzazione nella cache in automazione interfaccia utente](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
- [Supportare pattern di controllo in un provider di automazione interfaccia utente](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)
- [Mapping dei pattern di controllo per client di automazione interfaccia utente](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)
- [Text Services Framework](/windows/desktop/api/_tsf/)
