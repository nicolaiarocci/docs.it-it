### <a name="blockingcollectionlttgttrytakefromany-does-not-throw-anymore"></a>BlockingCollection&lt;T&gt;.TryTakeFromAny non genera più eccezioni

|   |   |
|---|---|
|Dettagli|Se una delle raccolte di input viene contrassegnata come completata, <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)> non restituisce più -1 e <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)> non genera più un'eccezione. Tale modifica consente di usare le raccolte quando una di esse è vuota o completata, ma l'altra contiene ancora elementi che possono essere recuperati.|
|Suggerimento|Se il metodo TryTakeFromAny con restituzione di -1 o con generazione di un'eccezione è stato usato per scopi di controllo di flusso in caso di completamento di una raccolta di blocco, tale codice deve ora essere modificato per usare <code>.Any(b =&gt; b.IsCompleted)</code> per rilevare tale condizione.|
|Ambito|Secondario|
|Versione|4.5|
|Tipo|Runtime|
|API interessate|<ul><li><xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.TimeSpan)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.TimeSpan)?displayProperty=nameWithType></li></ul>|
