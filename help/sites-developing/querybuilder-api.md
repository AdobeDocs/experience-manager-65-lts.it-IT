---
title: API Query Builder
description: La funzionalità di Asset Share Query Builder è esposta tramite un'API Java&trade; e un'API REST.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
pagetitle: Query Builder API
tagskeywords: querybuilder
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: a87c571e-7afb-42e7-836c-170dcfb0d03b
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '2032'
ht-degree: 0%

---

# API Query Builder{#query-builder-api}

La funzionalità di [Asset Share Query Builder](/help/assets/assets-finder-editor.md) è esposta tramite un&#39;API Java™ e un&#39;API REST. Questa sezione descrive queste API.

Il generatore di query lato server ( [`QueryBuilder`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/QueryBuilder.html)) accetta una descrizione della query, crea ed esegue una query XPath, facoltativamente filtra il set di risultati ed estrae i facet, se necessario.

La descrizione della query è semplicemente un set di predicati ([`Predicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/Predicate.html)). Gli esempi includono un predicato full-text, che corrisponde alla funzione `jcr:contains()` in XPath.

Per ogni tipo di predicato, esiste un componente valutatore ([`PredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) che sa come gestire il predicato specifico per XPath, il filtro e l&#39;estrazione facet. È facile creare valutatori personalizzati, che sono collegati tramite il runtime del componente OSGi.

L’API REST consente di accedere alle stesse funzioni tramite HTTP con risposte inviate in JSON.

>[!NOTE]
>
>L’API QueryBuilder viene creata utilizzando l’API JCR. Puoi anche eseguire query sul JCR di Adobe Experience Manager utilizzando l’API JCR all’interno di un bundle OSGi. Per informazioni, consulta [Adobe Experience Manager utilizzando l&#39;API JCR](/help/sites-developing/access-jcr.md).

## Sessione Gem {#gem-session}

[Adobe Experience Manager (AEM) Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/overview.html?lang=it) è una serie di approfondimenti tecnici su Adobe Experience Manager forniti da esperti Adobe. Questa sessione dedicata al generatore di query è utile per una panoramica e per l’utilizzo dello strumento.

>[!NOTE]
>
>La sessione Gem di AEM [Moduli di ricerca è stata semplificata con AEM querybuilder](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-search-forms-using-querybuilder.html?lang=it) per ottenere una panoramica dettagliata del generatore di query.

## Query di esempio {#sample-queries}

Questi esempi sono forniti nella notazione di stile delle proprietà Java™. Per utilizzarli con l&#39;API Java™, utilizzare un Java™ `HashMap` come nell&#39;esempio di API seguente.

Per il servlet JSON `QueryBuilder`, ogni esempio include un collegamento all&#39;installazione locale di CQ (nel percorso predefinito, `http://localhost:4502`). Accedi all’istanza CQ prima di utilizzare questi collegamenti.

>[!CAUTION]
>
>Per impostazione predefinita, il servlet json del generatore di query visualizza un massimo di dieci hit.
>
>L’aggiunta del seguente parametro consente al servlet di visualizzare tutti i risultati della query:
>
>**`p.limit=-1`**

>[!NOTE]
>
>Per visualizzare i dati JSON restituiti nel browser, puoi usare un plug-in come JSONView per Firefox.

### Restituzione di tutti i risultati {#returning-all-results}

La seguente query **restituisce dieci risultati** (o, per essere precisi, un massimo di dieci), ma ti informa del **numero di hit:** che sono disponibili:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

La stessa query (con il parametro `p.limit=-1`) **restituirà tutti i risultati** (potrebbe essere un numero elevato a seconda dell&#39;istanza):

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### Utilizzo di p.guessTotal per restituire i risultati {#using-p-guesstotal-to-return-the-results}

Lo scopo del parametro `p.guessTotal` è restituire il numero appropriato di risultati che possono essere visualizzati combinando i valori p.offset e p.limit vitali minimi. L&#39;utilizzo di questo parametro offre il vantaggio di migliorare le prestazioni con set di risultati di grandi dimensioni. Questo evita di calcolare il totale completo (ad esempio, chiamando result.getSize()) e di leggere l’intero set di risultati, ottimizzato fino al motore e all’indice di Oak. Questa può essere una differenza significativa quando ci sono 100 migliaia di risultati, sia nel tempo di esecuzione che nell&#39;utilizzo della memoria.

Lo svantaggio del parametro è che gli utenti non vedono il totale esatto. Ma puoi impostare un numero minimo come p.guessTotal=1000 in modo che legga sempre fino a 1000, così da ottenere i totali esatti per set di risultati più piccoli, ma se è più di quello, puoi solo mostrare &quot;e altro&quot;.

Aggiungi `p.guessTotal=true` alla query per vedere come funziona:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

La query restituisce il valore predefinito `p.limit` di `10` risultati con un offset `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

A partire da AEM 6.0 SP2, è anche possibile utilizzare un valore numerico per contare fino a un numero personalizzato di risultati massimi. Utilizzare la stessa query di cui sopra, ma modificare il valore di `p.guessTotal` in `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

Restituisce un numero con lo stesso limite predefinito di dieci risultati con un offset pari a 0, ma visualizza solo un massimo di 50 risultati:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementazione della paginazione {#implementing-pagination}

Per impostazione predefinita, Query Builder fornisce anche il numero di hit. A seconda della dimensione del risultato, l’operazione potrebbe richiedere molto tempo, poiché per determinare il conteggio accurato è necessario verificare ogni risultato per il controllo degli accessi. La maggior parte del totale viene utilizzata per implementare la paginazione per l’interfaccia utente dell’utente finale. Poiché la determinazione del conteggio esatto può essere lenta, si consiglia di utilizzare la funzione guessTotal per implementare l’impaginazione.

Ad esempio, l’interfaccia utente può adattare il seguente approccio:

* Ottieni e visualizza il conteggio accurato del numero di hit totali ([SearchResult.getTotalMatches()](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) o totali nella risposta querybuilder.json) minori o uguali a 100;
* Impostare `guessTotal` su 100 durante la chiamata al Generatore di query.

* La risposta può avere il seguente risultato:

   * `total=43`, `more=false` - Indica che il numero totale di hit è 43. L’interfaccia utente può visualizzare fino a dieci risultati come parte della prima pagina e fornire l’impaginazione per le tre pagine successive. È inoltre possibile utilizzare questa implementazione per visualizzare un testo descrittivo come **&quot;43 risultati trovati&quot;**.
   * `total=100`, `more=true` - Indica che il numero totale di hit è maggiore di 100 e il conteggio esatto non è noto. L’interfaccia utente può visualizzare fino a dieci pagine come parte della prima pagina e fornire l’impaginazione per le dieci pagine successive. È inoltre possibile utilizzare questa proprietà per visualizzare un testo come **&quot;più di 100 risultati trovati&quot;**. Quando l&#39;utente passa alle pagine successive, le chiamate effettuate al Generatore di query aumentano il limite di `guessTotal` e anche dei parametri `offset` e `limit`.

`guessTotal` deve essere utilizzato nei casi in cui l&#39;interfaccia utente deve utilizzare lo scorrimento infinito per evitare che Query Builder determini il conteggio esatto degli hit.

### Trova i file jar e ordinali, prima i più recenti {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Trova tutte le pagine e ordinale per ultima modifica {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Trova tutte le pagine e ordinale in base all’ultima modifica, ma decrescente {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Ricerca full-text, ordinata per punteggio {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Cerca le pagine con un tag specifico {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

Utilizza il predicato `tagid` come nell&#39;esempio se conosci l&#39;ID tag esplicito.

Utilizza il predicato `tag` per il percorso del titolo del tag (senza spazi).

Nell&#39;esempio precedente, poiché si stanno cercando pagine ( `cq:Page` nodi), utilizzare il percorso relativo di tale nodo per il predicato `tagid.property`, ovvero `jcr:content/cq:tags`. Per impostazione predefinita, `tagid.property` è semplicemente `cq:tags`.

### Cerca in più percorsi (utilizzando i gruppi) {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

Questa query utilizza un *gruppo* (denominato &quot; `group`&quot;), che agisce per delimitare le sottoespressioni all&#39;interno di una query, proprio come fanno le parentesi nelle notazioni più standard. Ad esempio, la query precedente potrebbe essere espressa in uno stile più familiare come:

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

All&#39;interno del gruppo nell&#39;esempio, il predicato `path` viene utilizzato più volte. Per differenziare e ordinare le due istanze del predicato (per alcuni predicati è richiesto l&#39;ordinamento), è necessario anteporre ai predicati il prefisso *N* `_ where`*N* è l&#39;indice dell&#39;ordinamento. Nell&#39;esempio precedente, i predicati risultanti sono `1_path` e `2_path`.

`p` in `p.or` è un delimitatore speciale che indica che il seguente (in questo caso un `or`) è un *parametro* del gruppo, anziché un subpredicato del gruppo, ad esempio `1_path`.

Se non viene fornito alcun `p.or`, tutti i predicati sono AND insieme, ovvero ogni risultato deve soddisfare tutti i predicati.

>[!NOTE]
>
>Non è possibile utilizzare lo stesso prefisso numerico in una singola query, anche per predicati diversi.

### Cerca proprietà {#search-for-properties}

Qui si stanno cercando tutte le pagine di un dato modello, utilizzando la proprietà `cq:template`:

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

Ciò presenta lo svantaggio che vengono restituiti i nodi `jcr:content` delle pagine, non le pagine stesse. Per risolvere questo problema, puoi eseguire ricerche per percorso relativo:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### Cerca più proprietà {#search-for-multiple-properties}

Quando utilizzi più volte il predicato proprietà, devi aggiungere nuovamente i prefissi numerici:

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Cerca più valori di proprietà {#search-for-multiple-property-values}

Per evitare gruppi di grandi dimensioni quando si desidera cercare più valori di una proprietà ( `"A" or "B" or "C"`), è possibile fornire più valori al predicato `property`:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

Per le proprietà con più valori, è inoltre possibile richiedere che più valori corrispondano ( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## Ottimizzazione di ciò che viene restituito {#refining-what-is-returned}

Per impostazione predefinita, il servlet JSON QueryBuilder restituisce un insieme predefinito di proprietà per ogni nodo del risultato della ricerca (ad esempio, percorso, nome e titolo). Per ottenere il controllo sulle proprietà restituite, effettuare una delle seguenti operazioni:

Specifica

```
p.hits=full
```

In questo caso, tutte le proprietà sono incluse per ciascun nodo:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

Utilizzare

```
p.hits=selective
```

E specifica le proprietà che desideri inserire

```
p.properties
```

Separato da uno spazio:

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[`http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Triangle) [p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.nodedepth=5&p.properties=sling%3aresourceType%20jcr%3apath&property=jcr%3atitle&property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

È inoltre possibile includere nodi figlio nella risposta QueryBuilder. A questo scopo, devi specificare

```
p.nodedepth=n
```

Dove `n` è il numero di livelli che si desidera vengano restituiti dalla query. Per restituire un nodo figlio, è necessario specificarlo con il selettore delle proprietà

```
p.hits=full
```

Esempio:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## Altri predicati {#morepredicates}

Per ulteriori predicati, vedere la [pagina di riferimento del predicato di Query Builder](/help/sites-developing/querybuilder-predicate-reference.md).

Puoi anche controllare [Javadoc per le `PredicateEvaluator` classi](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). Il codice Javadoc per queste classi contiene l’elenco delle proprietà che puoi utilizzare.

Il prefisso del nome della classe (ad esempio, &quot; `similar`&quot; in [`SimilarityPredicateEvaluator`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) è la *proprietà entità* della classe. Questa proprietà è anche il nome del predicato da utilizzare nella query (in minuscolo).

Per tali proprietà di entità, è possibile ridurre la query e utilizzare &quot; `similar=/content/en`&quot; invece della variante completa &quot; `similar.similar=/content/en`&quot;. Il modulo completo deve essere utilizzato per tutte le proprietà non principali di una classe.

## Esempio di utilizzo API di Query Builder {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>Per informazioni su come creare un bundle OSGi che utilizza l&#39;API QueryBuilder e utilizza tale bundle OSGi all&#39;interno di un&#39;applicazione Adobe Experience Manager, consulta [Creazione di bundle OSGi Adobe CQ che utilizzano l&#39;AP](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)I di Query Builder.

La stessa query viene eseguita su HTTP utilizzando il servlet Query Builder (JSON):

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Memorizzazione e caricamento delle query {#storing-and-loading-queries}

Le query possono essere archiviate nel repository in modo da poterle utilizzare in un secondo momento. `QueryBuilder` fornisce al metodo &quot;`storeQuery` la firma seguente:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Quando si utilizza il metodo [`QueryBuilder#storeQuery`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession), l&#39;elemento `Query` specificato viene archiviato nel repository come file o come proprietà in base al valore dell&#39;argomento `createFile`. Nell&#39;esempio seguente viene illustrato come salvare un `Query` nel percorso `/mypath/getfiles` come file:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Tutte le query archiviate in precedenza possono essere caricate dal repository utilizzando il metodo [`QueryBuilder#loadQuery`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Ad esempio, un `Query` archiviato nel percorso `/mypath/getfiles` può essere caricato dal seguente snippet:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Test e debug {#testing-and-debugging}

Per eseguire il gioco e il debug delle query di querybuilder, puoi utilizzare la console del debugger di QueryBuilder all’indirizzo

`http://localhost:4502/libs/cq/search/content/querydebug.html`

Oppure, in alternativa, il servlet json querybuilder in

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` è solo un esempio).

### Consigli generali sul debug {#general-debugging-recommendations}

### Ottenere XPath esplicativo tramite la registrazione {#obtain-explain-able-xpath-via-logging}

Spiega **tutte** le query durante il ciclo di sviluppo rispetto al set di indici di destinazione.

* Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile

   * Passa a https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Crea un logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.

* Dopo aver abilitato DEBUG per la classe precedente, nei registri viene visualizzato l&#39;XPath generato da Query Builder.
* Copiare la query XPath dalla voce di registro per la query QueryBuilder associata, ad esempio:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Incolla la query XPath in [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) come XPath per ottenere il piano di query

### Ottenere XPath esplicativo tramite il debugger di Query Builder {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* Utilizza il debugger di AEM QueryBuilder per generare una query XPath spiegabile:

Spiega **tutte** le query durante il ciclo di sviluppo rispetto al set di indici di destinazione.

**Ottieni XPath esplicativo tramite registrazione**

* Abilita i registri DEBUG per QueryBuilder per ottenere la query XPath sottostante e spiegabile

   * Passa a https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog. Crea un logger per `com.day.cq.search.impl.builder.QueryImpl` in **DEBUG**.

* Dopo aver abilitato DEBUG per la classe precedente, nei registri viene visualizzato l&#39;XPath generato da Query Builder.
* Copiare la query XPath dalla voce di registro per la query QueryBuilder associata, ad esempio:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Incolla la query XPath in [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) come XPath per ottenere il piano di query

**Ottieni XPath esplicativo tramite il debugger di Query Builder**

* Utilizza il debugger di AEM QueryBuilder per generare una query XPath spiegabile:

![chlimage_1-66](assets/chlimage_1-66a.png)

1. Fornisci la query di Query Builder nel debugger di Query Builder
1. Eseguire la ricerca
1. Ottenere l&#39;XPath generato
1. Incollare la query XPath in Explain Query come XPath per ottenere il piano di query

>[!NOTE]
>
>Le query non querybuilder (XPath, JCR-SQL2) possono essere fornite direttamente in Explain Query.

Per un sommario su come eseguire il debug delle query con QueryBuilder, guarda il video seguente.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## Eseguire il debug delle query con la registrazione {#debugging-queries-with-logging}

>[!NOTE]
>
>La configurazione dei logger è descritta nella sezione [Creazione di logger e writer personalizzati](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

L’output del registro (livello INFO) dell’implementazione del generatore di query durante l’esecuzione della query descritta in Test e debug:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Se una query utilizza valutatori di predicati che filtrano o che utilizzano un ordine personalizzato per comparatore, nella query verrà annotato anche quanto segue:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Collegamenti Javadoc {#javadoc-links}

| **Javadoc** | **Descrizione** |
|---|---|
| [com.day.cq.search](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/package-summary.html) | QueryBuilder di base e API di query |
| [com.day.cq.search.result](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/result/package-summary.html) | API dei risultati |
| [com.day.cq.search.facets](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.bucket](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Bucket (contenuti all’interno di facet) |
| [com.day.cq.search.eval](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/eval/package-summary.html) | Valutatori predicato |
| [com.day.cq.search.facets.extractors](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Estrattori sfaccettatura (per valutatori) |
| [com.day.cq.search.writer](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/writer/package-summary.html) | Hit writer di risultati JSON per il servlet Querybuilder (/bin/querybuilder.json) |
