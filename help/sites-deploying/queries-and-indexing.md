---
title: Query e indicizzazione Oak
description: Scopri come configurare gli indici in Adobe Experience Manager (AEM) 6.5 LTS.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 432fc767-a6b8-48f8-b124-b13baca51fe8
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 1%

---

# Query e indicizzazione Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>Questo articolo riguarda la configurazione degli indici in AEM 6.5 LTS. Per le best practice sull&#39;ottimizzazione delle prestazioni di query e indicizzazione, vedere [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introduzione {#introduction}

A differenza di Jackrabbit 2, Oak non indicizza il contenuto per impostazione predefinita. Gli indici personalizzati devono essere creati quando necessario, come con i database relazionali tradizionali. Se non esiste un indice per una query specifica, è possibile che vengano attraversati molti nodi. La query potrebbe ancora funzionare, ma è probabilmente lenta.

Se Oak rileva una query senza un indice, viene stampato un messaggio di registro di livello WARN:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Lingue di query supportate {#supported-query-languages}

Il motore di query di Oak supporta le seguenti lingue:

* XPath (consigliato)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipi di indicizzatore e calcolo dei costi {#indexer-types-and-cost-calculation}

Il backend basato su Apache Oak consente di collegare diversi indicizzatori all’archivio.

Un indicizzatore è l&#39;**Indice proprietà**, per il quale la definizione dell&#39;indice è archiviata nell&#39;archivio stesso.

L&#39;implementazione per **Apache Lucene** è disponibile per impostazione predefinita e supporta l&#39;indicizzazione full-text.

Se non è disponibile alcun altro indicizzatore, viene utilizzato l&#39;**Indice trasversale**. Ciò significa che il contenuto non è indicizzato e che i nodi di contenuto vengono attraversati per trovare corrispondenze alla query.

Se per una query sono disponibili più indicizzatori, ogni indicizzatore disponibile stima il costo dell&#39;esecuzione della query. Oak sceglie quindi l’indicizzatore con il costo stimato più basso.

![chlimage_1-148](assets/chlimage_1-148.png)

Il diagramma precedente è una rappresentazione di alto livello del meccanismo di esecuzione delle query di Apache Oak.

Innanzitutto, la query viene analizzata in una struttura ad albero della sintassi astratta. Quindi, la query viene controllata e trasformata in SQL-2, che è la lingua nativa per le query Oak.

Successivamente, ogni indice viene consultato per stimare il costo della query. Una volta completato, vengono recuperati i risultati dall’indice più economico. Infine, i risultati vengono filtrati, sia per garantire che l’utente corrente abbia accesso in lettura al risultato sia che il risultato corrisponda alla query completa.

## Configurazione degli indici {#configuring-the-indexes}

>[!NOTE]
>
>Per un archivio di grandi dimensioni, la creazione di un indice è un’operazione che richiede tempo. Questo vale sia per la creazione iniziale di un indice che per la reindicizzazione (ricostruzione di un indice dopo la modifica della definizione). Vedere anche [Risoluzione dei problemi relativi agli indici Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) e [Prevenzione della reindicizzazione lenta](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Se la reindicizzazione è necessaria in archivi di grandi dimensioni, specialmente quando si utilizza MongoDB e per gli indici full-text, considera la pre-estrazione del testo e l’utilizzo di oak-run per creare l’indice iniziale e reindicizzare.

Gli indici sono configurati come nodi nell&#39;archivio nel nodo **Oak:index**.

Il tipo del nodo indice deve essere **oak:QueryIndexDefinition.** Per ogni indicizzatore sono disponibili diverse opzioni di configurazione come proprietà del nodo. Per ulteriori informazioni, consulta i dettagli di configurazione per ogni tipo di indicizzatore riportati di seguito.

### Indice proprietà {#the-property-index}

L&#39;indice delle proprietà è utile per le query che hanno vincoli di proprietà ma non sono full-text. Può essere configurato seguendo la procedura seguente:

1. Apri CRXDE andando su `http://localhost:4502/crx/de/index.jsp`
1. Crea un nodo in **oak:index**
1. Denomina il nodo **PropertyIndex** e imposta il tipo di nodo su **oak:QueryIndexDefinition**
1. Imposta le seguenti proprietà per il nuovo nodo:

   * **tipo:** `property` (di tipo Stringa)
   * **propertyNames:** `jcr:uuid` (di tipo Name)

   In questo esempio particolare viene indicizzata la proprietà `jcr:uuid`, il cui processo consiste nell&#39;esporre l&#39;identificatore univoco universale (UUID) del nodo a cui è associata.

1. Salva le modifiche.

L’indice delle proprietà dispone delle seguenti opzioni di configurazione:

* La proprietà **type** specifica il tipo di indice e in questo caso deve essere impostata su **property**

* La proprietà **propertyNames** indica l&#39;elenco delle proprietà memorizzate nell&#39;indice. Se manca, il nome del nodo viene utilizzato come valore di riferimento del nome di proprietà. In questo esempio, la proprietà **jcr:uuid** il cui processo consiste nell&#39;esporre l&#39;identificatore univoco (UUID) del relativo nodo viene aggiunta all&#39;indice.

* Il flag **unique** che, se impostato su **true**, aggiunge un vincolo di univocità nell&#39;indice della proprietà.

* La proprietà **DeclaringNodeTypes** consente di specificare un determinato tipo di nodo a cui si applica solo l&#39;indice.
* Il flag **reindex** che, se impostato su **true**, attiva una reindicizzazione del contenuto completo.

### Indice ordinato {#the-ordered-index}

L&#39;indice Ordinato è un&#39;estensione dell&#39;indice Proprietà. Tuttavia, è stato dichiarato obsoleto. Gli indici di questo tipo devono essere sostituiti con [Indice proprietà Lucene](#the-lucene-property-index).

### Indice full-text Lucene {#the-lucene-full-text-index}

Un indicizzatore full-text basato su Apache Lucene è disponibile in AEM 6.5 LTS.

Se è configurato un indice full-text, tutte le query con una condizione full-text utilizzano l&#39;indice full-text, indipendentemente dall&#39;esistenza di altre condizioni indicizzate e da eventuali restrizioni di percorso.

Se non è configurato alcun indice full-text, le query con condizioni full-text non funzionano come previsto.

Poiché l’indice viene aggiornato tramite un thread in background asincrono, alcune ricerche full-text non sono disponibili per una piccola finestra di tempo fino al completamento dei processi in background.

Per configurare un indice full-text Lucene, attenersi alla procedura descritta di seguito.

1. Apri CRXDE e crea un nodo in **oak:index**.
1. Denomina il nodo **LuceneIndex** e imposta il tipo di nodo su **oak:QueryIndexDefinition**
1. Aggiungi le seguenti proprietà al nodo:

   * **tipo:** `lucene` (di tipo Stringa)
   * **asincrono:** `async` (di tipo String)

1. Salva le modifiche.

L’indice Lucene dispone delle seguenti opzioni di configurazione:

* La proprietà **type** che specifica il tipo di indice deve essere impostata su **lucene**
* La proprietà **async** che deve essere impostata su **async**. In questo modo il processo di aggiornamento dell’indice viene inviato a un thread in background.
* La proprietà **includePropertyTypes**, che definisce il sottoinsieme dei tipi di proprietà inclusi nell&#39;indice.
* La proprietà **excludePropertyNames** che definisce un elenco di nomi di proprietà, ovvero proprietà da escludere dall&#39;indice.
* Il flag **reindex** che, se impostato su **true**, attiva una reindicizzazione del contenuto completo.

### Ricerca full-text {#understanding-fulltext-search}

La documentazione di questa sezione si applica, ad esempio, agli indici Apache Lucene, Elasticsearch e full-text di PostgreSQL, SQLite e MySQL. L’esempio seguente è per AEM/Oak/Lucene.

<b>Dati da indicizzare</b>

Il punto di partenza sono i dati che devono essere indicizzati. Prendi ad esempio i seguenti documenti:

| <b>ID documento</b> | <b>Percorso</b> | <b>Testo completo</b> |
| --- | --- | --- |
| 100 | /content/rubik | &quot;Rubik è un marchio finlandese.&quot; |
| 200 | /content/rubiksCube | &quot;Il cubo di Rubik è stato inventato nel 1974.&quot; |
| 300 | /content/cube | &quot;Un cubo è un oggetto tridimensionale.&quot; |


<b>Indice invertito</b>

Il meccanismo di indicizzazione suddivide il testo completo in parole chiamate &quot;token&quot; e crea un indice denominato &quot;indice invertito&quot;. Questo indice contiene l&#39;elenco dei documenti in cui viene visualizzato per ogni parola.

Le parole brevi e comuni (dette anche &quot;parole non significative&quot;) non sono indicizzate. Tutti i token vengono convertiti in minuscolo e viene applicato lo stemming.

I caratteri speciali come *&quot;-&quot;* non sono indicizzati.

| <b>Token</b> | <b>ID documento</b> |
| --- | --- |
| 194 | ..., 200,... |
| brand | ..., 100,... |
| cubo | ..., 200, 300,... |
| dimensione | 300 |
| fine | ..., 100,... |
| inventare | 200 |
| oggetto | ..., 300... |
| rubik | ..., 100, 200,... |

L&#39;elenco dei documenti è ordinato. Questo è utile quando si esegue una query.

<b>Ricerca in corso</b>

Di seguito è riportato un esempio di query. Tutti i caratteri speciali (ad esempio *&#39;*) sono stati sostituiti da uno spazio:

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

Le parole vengono tokenizzate e filtrate nello stesso modo in cui vengono indicizzate (le parole a carattere singolo vengono rimosse, ad esempio). In questo caso, la ricerca è per:

```
+:fulltext:rubik +:fulltext:cube
```

L&#39;indice consulta l&#39;elenco dei documenti per tali parole. Se sono presenti molti documenti, l&#39;elenco può essere di grandi dimensioni. Ad esempio, supponiamo che contengano quanto segue:


| <b>Token</b> | <b>ID documento</b> |
| --- | --- |
| rubik | 10, 100, 200, 1000 |
| cubo | 30, 200, 300, 2000 |


Lucene si sposta avanti e indietro tra i due elenchi (o elenchi round robin `n`, durante la ricerca di `n` parole):

* Leggi nel &quot;rubik&quot; ottiene la prima voce: trova 10
* La lettura nel &quot;cubo&quot; ottiene la prima voce `>` = 10. 10 non è stato trovato, quindi quello successivo è 30.
* Leggi in &quot;rubik&quot; ottiene la prima voce `>` = 30: ne trova 100.
* Letto nel &quot;cubo&quot; ottiene la prima voce `>` = 100: ne trova 200.
* Leggere in &quot;rubik&quot; ottiene la prima voce `>` = 200. 200. Quindi il documento 200 corrisponde a entrambi i termini. Questo viene ricordato.
* Leggi nella &quot;rubik&quot; ottiene la prossima voce: 1000.
* Letto nel &quot;cubo&quot; ottiene la prima voce `>` = 1000: trova 2000.
* Leggi in &quot;rubik&quot; ottiene la prima voce `>` = 2000: fine dell&#39;elenco.
* Infine, puoi interrompere la ricerca.

L’unico documento trovato che contiene entrambi i termini è 200, come nell’esempio seguente:

| 200 | /content/rubiksCube | &quot;Il cubo di Rubik è stato inventato nel 1974.&quot; |
| --- | --- | --- |

Quando vengono trovate più voci, queste vengono ordinate in base al punteggio.

### Indice della proprietà Lucene {#the-lucene-property-index}

A partire da **Oak 1.0.8**, Lucene può essere utilizzato per creare indici che comportano vincoli di proprietà che non sono full-text.

Per ottenere un indice della proprietà Lucene, la proprietà **fulltextEnabled** deve essere sempre impostata su false.

Prendi il seguente esempio di query:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Per definire un indice delle proprietà Lucene per la query precedente, è possibile aggiungere la seguente definizione creando un nodo in **`oak:index`:**

* **Nome:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Una volta creato il nodo, aggiungi le seguenti proprietà:

* **tipo:**

  ```xml
  lucene (of type String)
  ```

* **asincrono:**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled:**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>Rispetto all&#39;indice proprietà regolare, l&#39;indice proprietà Lucene è sempre configurato in modalità asincrona. Pertanto, i risultati restituiti dall’indice potrebbero non riflettere sempre lo stato più aggiornato dell’archivio.

>[!NOTE]
>
>Per informazioni più specifiche sull&#39;indice delle proprietà Lucene, consulta la [pagina della documentazione di Apache Jackrabbit Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analizzatori Lucene {#lucene-analyzers}

A partire dalla versione 1.2.0, Oak supporta gli analizzatori Lucene.

Gli analizzatori vengono utilizzati sia quando un documento viene indicizzato che al momento della query. Un analizzatore esamina il testo dei campi e genera un flusso di token. Gli analizzatori Lucene sono composti da una serie di classi di tokenizzatore e filtro.

Gli analizzatori possono essere configurati tramite il nodo `analyzers` (di tipo `nt:unstructured`) nella definizione `oak:index`.

L&#39;analizzatore predefinito per un indice è configurato nell&#39;elemento figlio `default` del nodo analizzatori.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Per un elenco degli analizzatori disponibili, consulta la documentazione API della versione Lucene in uso.

#### Specifica diretta della classe dell&#39;analizzatore {#specifying-the-analyzer-class-directly}

Se desideri utilizzare un analizzatore predefinito, puoi configurarlo seguendo la procedura seguente:

1. Individuare l&#39;indice con cui si desidera utilizzare l&#39;analizzatore sotto il nodo `oak:index`.

1. Nell&#39;indice creare un nodo figlio denominato `default` di tipo `nt:unstructured`.

1. Aggiungi una proprietà al nodo predefinito con le seguenti proprietà:

   * **Nome:** `class`
   * **Tipo:** `String`
   * **Valore:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   Il valore è il nome della classe dell&#39;analizzatore che si desidera utilizzare.

   È inoltre possibile impostare l&#39;analizzatore da utilizzare con una versione specifica di Lucene utilizzando la proprietà stringa facoltativa `luceneMatchVersion`. Una sintassi valida per utilizzarlo con Lucene 4.7 sarebbe:

   * **Nome:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valore:** `LUCENE_47`

   Se `luceneMatchVersion` non viene fornito, Oak utilizza la versione di Lucene con cui è stato fornito.

1. Se desideri aggiungere un file di parole non significative alle configurazioni dell&#39;analizzatore, puoi creare un nodo sotto `default` con le seguenti proprietà:

   * **Nome:** `stopwords`
   * **Tipo:** `nt:file`

#### Creazione di analizzatori tramite la composizione {#creating-analyzers-via-composition}

Gli analizzatori possono essere composti anche in base a `Tokenizers`, `TokenFilters` e `CharFilters`. Per farlo, specifica un analizzatore e crea nodi secondari dei suoi tokenizer e filtri opzionali applicati nell’ordine elencato.

Considera questa struttura di nodi come un esempio:

* **Nome:** `analyzers`

   * **Nome:** `default`

      * **Nome:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nome:** `HTMLStrip`
         * **Nome:** `Mapping`

      * **Nome:** `tokenizer`

         * **Nome proprietà:** `name`

            * **Tipo:** `String`
            * **Valore:** `Standard`

      * **Nome:** `filters`
      * **Tipo:** `nt:unstructured`

         * **Nome:** `LowerCase`
         * **Nome:** `Stop`

            * **Nome proprietà:** `words`

               * **Tipo:** `String`
               * **Valore:** `stop1.txt, stop2.txt`

            * **Nome:** `stop1.txt`

               * **Tipo:** `nt:file`

            * **Nome:** `stop2.txt`

               * **Tipo:** `nt:file`

Il nome dei filtri, charFilters e dei token viene formato rimuovendo i suffissi di fabbrica. Pertanto:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` diventa `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` diventa `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` diventa `Stop`

Qualsiasi parametro di configurazione richiesto per la factory viene specificato come proprietà del nodo in questione.

In casi quali il caricamento di parole non significative in cui è necessario caricare contenuto da file esterni, il contenuto può essere fornito creando un nodo figlio di tipo `nt:file` per il file in questione.

### Strumenti di indicizzazione di AEM {#aem-indexing-tools}

AEM 6.1 integra anche due strumenti di indicizzazione presenti in AEM 6.0 come parte del set di strumenti Adobe Consulting Services Commons:

1. **Spiega query**, uno strumento progettato per aiutare gli amministratori a comprendere il modo in cui vengono eseguite le query;
1. **Oak Index Manager**, interfaccia utente Web per la gestione degli indici esistenti.

Ora puoi raggiungerli da **Strumenti - Operazioni - Dashboard - Diagnosi** nella schermata iniziale di AEM.

Per ulteriori informazioni su come utilizzarli, consulta la [documentazione di Operations Dashboard](/help/sites-administering/operations-dashboard.md).

#### Creazione di indici di proprietà tramite OSGi {#creating-property-indexes-via-osgi}

Il pacchetto ACS Commons espone anche configurazioni OSGi che possono essere utilizzate per creare indici di proprietà.

Puoi accedervi dalla console Web cercando &quot;**Assicurarsi che Oak Property Index**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Risoluzione dei problemi di indicizzazione {#troubleshooting-indexing-issues}

Possono verificarsi situazioni in cui l’esecuzione delle query richiede molto tempo e il tempo di risposta generale del sistema è lento.

Questa sezione presenta una serie di raccomandazioni su ciò che deve essere fatto per rintracciare la causa di tali problemi e consigli su come risolverli.

#### Preparazione delle informazioni di debug per l&#39;analisi {#preparing-debugging-info-for-analysis}

Il modo più semplice per ottenere le informazioni richieste per la query in esecuzione è tramite lo strumento [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query). Questo consente di raccogliere le informazioni precise necessarie per eseguire il debug di una query lenta senza dover consultare le informazioni a livello di registro. Ciò è utile se si conosce la query di cui viene eseguito il debug.

Se questo non è possibile per qualsiasi motivo, puoi raccogliere i registri di indicizzazione in un singolo file e utilizzarli per risolvere il problema specifico.

#### Abilita registrazione {#enable-logging}

Per abilitare la registrazione, devi abilitare i registri di livello **DEBUG** per le categorie relative alle query e all&#39;indicizzazione di Oak. Tali categorie sono:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

La categoria **com.day.cq.search** è applicabile solo se si utilizza l&#39;utilità QueryBuilder fornita da AEM.

>[!NOTE]
>
>È importante che i registri siano impostati su DEBUG solo per la durata di esecuzione della query che si desidera risolvere. In caso contrario, nel tempo nei registri vengono generati molti eventi. Per questo motivo, una volta raccolti i registri richiesti, torna alla registrazione a livello INFO per le categorie sopra menzionate.

Per abilitare la registrazione, segui questa procedura:

1. Puntare il browser a `https://serveraddress:port/system/console/slinglog`
1. Fare clic sul pulsante **Aggiungi nuovo logger** nella parte inferiore della console.
1. Nella riga appena creata, aggiungi le categorie sopra indicate. È possibile utilizzare il segno **+** per aggiungere più di una categoria a un singolo logger.
1. Scegliere **DEBUG** dall&#39;elenco a discesa **Livello di registro**.
1. Impostare il file di output su `logs/queryDebug.log`. In questo modo tutti gli eventi DEBUG vengono correlati in un unico file di registro.
1. Esegui la query o esegui il rendering della pagina che utilizza la query su cui desideri eseguire il debug.
1. Dopo aver eseguito la query, torna alla console di registrazione e modifica il livello del registro appena creato in **INFO**.

#### Configurazione indice {#index-configuration}

Il modo in cui la query viene valutata è influenzato in gran parte dalla configurazione dell’indice. È importante che la configurazione dell’indice sia analizzata o inviata al supporto. Puoi ottenere la configurazione come pacchetto di contenuti o una rappresentazione JSON.

In genere, la configurazione dell’indicizzazione viene memorizzata nel nodo `/oak:index` in CRXDE. Puoi ottenere la versione JSON in:

`https://serveraddress:port/oak:index.tidy.-1.json`

Se l’indice è configurato in una posizione diversa, modifica di conseguenza il percorso.

#### Uscita MBean {#mbean-output}

A volte è utile fornire l’output di MBean correlati all’indice per il debug. Per farlo, segui questi passaggi:

1. Vai alla console JMX all’indirizzo:
   `https://serveraddress:port/system/console/jmx`

1. Cerca i seguenti MBean:

   * Statistiche indice Lucene
   * Statistiche di supporto CopyOnRead
   * Statistiche query Oak
   * IndexStats

1. Fare clic su ogni MBean per ottenere statistiche sulle prestazioni. Crea uno screenshot o annotali nel caso sia necessario un invio di supporto.

Puoi ottenere la variante JSON di queste statistiche anche dai seguenti URL:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

È inoltre possibile fornire output JMX consolidato tramite `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Questo includerebbe tutti i dettagli MBean relativi ad Oak in formato JSON.

#### Altri dettagli {#other-details}

Puoi raccogliere ulteriori dettagli per risolvere il problema, ad esempio:

1. La versione di Oak su cui è in esecuzione l’istanza. Per visualizzarlo, apri CRXDE e osserva la versione nell&#39;angolo inferiore destro della pagina di benvenuto oppure controlla la versione del bundle `org.apache.jackrabbit.oak-core`.
1. L’output di QueryBuilder Debugger della query problematica. È possibile accedere al debugger in: `https://serveraddress:port/libs/cq/search/content/querydebug.html`
