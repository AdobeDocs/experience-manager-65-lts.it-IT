---
title: Riferimento predicato di Query Builder
description: Riferimento predicato completo per l’API Query Builder.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: c044d541-24d6-4975-9b38-6a4317a16358
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---

# Riferimento predicato di Query Builder{#query-builder-predicate-reference}

>[!CAUTION]
>
>Le informazioni su questa pagina non sono esaustive.
>
>Per informazioni complete, vedere l&#39;elenco in **Predicati disponibili** nella console di Query Builder Debugger, ad esempio in:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>Ad esempio, consulta:
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## Generale {#general}

* [radice](#root)
* [gruppo](#group)
* [orderby](#orderby)

## Predicati {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [intervallo di date](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [full-text](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [lingua](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [risorsa principale](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [non scaduto](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [percorso](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [proprietà](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [simile](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### `boolproperty` {#boolproperty}

Corrisponde alle proprietà BOOLEAN di JCR. Accetta solo i valori &quot; `true`&quot; e &quot; `false`&quot;.&quot; Se è impostato su &quot; `false`&quot;, corrisponde se la proprietà ha il valore &quot; `false`&quot; o se non esiste affatto. Utile per verificare la presenza di flag booleani impostati solo se attivati.

Il parametro ereditato &quot; `operation`&quot; non ha alcun significato.

Supporta l’estrazione dei facet. Fornisce bucket per ogni valore `true` o `false`, ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **boolproperty**
Percorso relativo alla proprietà, ad esempio `myFeatureEnabled` o `jcr:content/myFeatureEnabled`.

* **valore**
Valore per cui verificare la proprietà, &quot; `true`&quot; o &quot; `false`&quot;.&quot;

### `contentfragment` {#contentfragment}

Limita il risultato ai frammenti di contenuto.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-1}

* **contentfragment**
Può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### `dateComparison` {#datecomparison}

Confronta due proprietà DATA JCR tra loro. Puoi verificare se sono uguali, ineguali, maggiori o maggiori o uguali.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

#### Proprietà {#properties-2}

* **proprietà1**

  Percorso della prima proprietà data.

* **proprietà2**

  Percorso della seconda proprietà data.

* **operazione**

  &quot; `equals`&quot; per corrispondenza esatta, &quot; `!=`&quot; per confronto disuguaglianza, &quot; `greater`&quot; per proprietà1 maggiore di proprietà2, &quot; `>=`&quot; per proprietà1 maggiore o uguale a proprietà2. Il valore predefinito è &quot; `equals`&quot;.

### `daterange` {#daterange}

Confronta le proprietà DATA JCR con un intervallo di data e ora. Utilizza ISO8601
formato per data e ora ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come il numero di millisecondi dal 1970 nel fuso orario UTC, il formato ora UNIX®.

Puoi cercare qualsiasi cosa tra due marche temporali, qualsiasi cosa più recente o più vecchia di una determinata data e anche scegliere tra intervalli inclusivi e aperti.

Supporta l’estrazione dei facet. Fornisce contenitori &quot;oggi&quot;, &quot;questa settimana&quot;, &quot;questo mese&quot;, &quot;ultimi 3 mesi&quot;, &quot;quest&#39;anno&quot;, &quot;ultimo anno&quot; e &quot;prima dello scorso anno&quot;.

Non supporta il filtro.

#### Proprietà {#properties-3}

* **proprietà**

  Percorso relativo di una proprietà `DATE`, ad esempio `jcr:lastModified`.

* **lowerBound**

  Limite di data inferiore per la verifica della proprietà, ad esempio `2014-10-01`.

* **lowerOperation**

  &quot; `>`&quot; (più recente) o &quot; `>=`&quot; (più recente), si applica a `lowerBound`. Il valore predefinito è &quot; `>`&quot;.

* **upperBound**

  Limite superiore per la verifica della proprietà, ad esempio `2014-10-01T12:15:00`.

* **upperOperation**

  &quot; `<`&quot; (più vecchio) o &quot; `<=`&quot; (più o meno), si applica a `upperBound`. Il valore predefinito è &quot; `<`&quot;.

* **fuso orario**

  ID del fuso orario da utilizzare quando non è specificato come stringa di data ISO-8601. Il fuso orario predefinito è quello del sistema.

### `excludepaths` {#excludepaths}

Esclude i nodi dal risultato in cui il loro percorso corrisponde a un’espressione regolare.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-4}

* **excludepaths**

  Espressione regolare associata ai percorsi dei risultati, escludendo quelli corrispondenti dal risultato.

### `fulltext` {#fulltext}

Cerca i termini nell&#39;indice full-text.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-5}

* **full-text**

  I termini di ricerca full-text.

* **relPath**

  Percorso relativo per la ricerca nella proprietà o nel sottonodo. Questa proprietà è facoltativa.

### `group` {#group}

Consente di creare le condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto ciò che si trova in una query di Query Builder è implicitamente in un gruppo radice, che può avere anche `p.or` e `p.not` parametri.

Esempio per associare una delle due proprietà a un valore:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Concettualmente `(1_property` O `2_property)`.

Esempio di gruppi nidificati:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Cerca il termine &quot;**Gestione**&quot; nelle pagine di `/content/geometrixx/en` o nelle risorse di `/content/dam/geometrixx`.

Concettualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tali join OR necessitano di indici validi per le prestazioni.

#### Proprietà {#properties-6}

* **p.or**

  Se è impostato su &quot; `true`&quot;, solo un predicato nel gruppo deve corrispondere. Il valore predefinito è &quot; `false`&quot;, il che significa che tutti devono corrispondere

* **p.not**

  Se è impostato su &quot; `true`&quot;, il gruppo verrà ignorato (impostazione predefinita: &quot; `false`&quot;).

* **&lt;predicato>**

  Aggiunge predicati nidificati.

* **N_&lt;predicato>**

  Aggiunge più predicati nidificati contemporaneamente, ad esempio `1_property, 2_property, ...`.

### hasPermission {#haspermission}

Limita il risultato agli elementi in cui la sessione corrente dispone dei privilegi [JCR specificati.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-7}

* **hasPermission**

  I privilegi JCR separati da virgole che la sessione utente corrente deve avere TUTTO il nodo in questione. Ad esempio, `jcr:write`, `jcr:modifyAccessControl`.

### `language` {#language}

Trova le pagine CQ in una lingua specifica. Vengono esaminate sia la proprietà lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni locali in una struttura del sito principale.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Supporta l’estrazione dei facet. Fornisce bucket per ogni codice lingua univoco.

#### Proprietà {#properties-8}

* **lingua**

  Codice della lingua ISO, ad esempio &quot;`de`&quot;.

### `mainasset` {#mainasset}

Controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica, ogni nodo non si trova all’interno di un nodo &quot;risorse secondarie&quot;. Non controlla il tipo di nodo `dam:Asset`. Per utilizzare questo predicato, impostare &quot; `mainasset=true`&quot; o &quot; `mainasset=false`&quot;, non sono disponibili altre proprietà.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Supporta l’estrazione facet e fornisce due bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **risorsa principale**

  Booleano, &quot; `true`&quot; per le risorse principali, &quot; `false`&quot; per le risorse secondarie.

### memberOf {#memberof}

Trova elementi che sono membri di una raccolta di risorse [sling specifica](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-10}

* **memberOf**

  Percorso della raccolta di risorse Sling.

### `nodename` {#nodename}

Corrisponde ai nomi dei nodi JCR.

Supporta l’estrazione dei facet. Fornisce bucket per ogni nome di nodo univoco (nome file).

#### Proprietà {#properties-11}

* **nodename**

  Pattern nome nodo che consente caratteri jolly: `*` = any o no char, `?` = any char, `[abc]` = only chars in brackets.

### `notexpired` {#notexpired}

Corrisponde agli elementi controllando se una proprietà DATA JCR è maggiore o uguale all’ora corrente del server. Può essere utilizzato per controllare una proprietà &quot; `expiresAt`&quot; come data e limitare solo a quelle non ancora scadute ( `notexpired=true`) o che sono già scadute ( `notexpired=false`).

Non supporta il filtro.

Supporta l’estrazione di sfaccettatura allo stesso modo del predicato dell’intervallo di dati.

#### Proprietà {#properties-12}

* **non scaduto**

  Booleano, &quot;`true`&quot; per non ancora scaduto (data futura o uguale), &quot; `false`&quot; per scaduto (data passata) (obbligatorio).

* **proprietà**

  Percorso relativo della proprietà `DATE` da verificare (obbligatorio).

### `orderby` {#orderby}

Consente di ordinare i risultati. Se è necessario ordinare per più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso numerico, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **orderby**

  Il nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, o da un altro predicato nella query, ad esempio `2_property`, su cui eseguire l&#39;ordinamento.

* **ordina**

  Direzione di ordinamento, &quot; `desc`&quot; per decrescente o &quot; `asc`&quot; per crescente (impostazione predefinita).

* **caso**

  Se è impostato su `ignore`, l&#39;ordinamento non fa distinzione tra maiuscole e minuscole, ovvero &quot;a&quot; precede &quot;B&quot;; se è vuoto o non viene specificato, l&#39;ordinamento fa distinzione tra maiuscole e minuscole, ovvero &quot;B&quot; precede &quot;a&quot;

### `path` {#path}

Esegue ricerche all&#39;interno di un determinato percorso.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-14}

* **percorso**

  Schema del percorso. Quando `exact=false` (impostazione predefinita), la ricerca corrisponde all&#39;intera sottostruttura nel percorso specificato, in modo analogo all&#39;aggiunta di `//*` in XPath, ma non include il percorso di base stesso. Quando `exact=true`, la ricerca corrisponde solo al percorso esatto, che può includere `*` caratteri jolly. Se `self` è impostato, la ricerca include il nodo di base e l&#39;intera sottostruttura.


* **esatto**

  Se `exact` è true (attivato), il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici ( `*`) che corrispondono ai nomi, ma non &quot; `/`&quot;; se è false (impostazione predefinita) tutti i discendenti sono inclusi (facoltativo).

* **piatto**

  Cerca solo gli elementi figlio diretti (ad esempio aggiungendo &quot;`/*`&quot; in `xpath`) (utilizzato solo se &quot;`exact`&quot; non è true, facoltativo).

* **self**

  Esegue la ricerca nella sottostruttura ma include il nodo di base indicato come percorso (nessun carattere jolly).

### `property` {#property}

Corrisponde alle proprietà JCR e ai relativi valori.

Supporta l’estrazione dei facet. Fornisce bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **proprietà**

  Percorso relativo alla proprietà, ad esempio `jcr:title`.

* **valore**

  Valore di cui controllare la proprietà; segue il tipo di proprietà JCR per le conversioni di stringhe.

* **N_value**

  Utilizza `1_value`, `2_value`, ... per verificare la presenza di più valori (combinati con `OR` per impostazione predefinita, con `AND` se e=true) (dalla versione 5.3).

* **e**

  Impostare su true per combinare più valori ( `N_value`) con AND (dalla versione 5.3).

* **operazione**

  Utilizza `equals` per una corrispondenza esatta (impostazione predefinita) e `unequals` per un confronto delle disuguaglianze. Utilizzare `like` per applicare la funzione XPath `jcr:like` facoltativa. Utilizzare `not` per nessuna corrispondenza (ad esempio, `not(@prop)` in XPath); in questo caso, il parametro `value` viene ignorato. Utilizzare `exists` per verificare se una proprietà esiste: `true` (impostazione predefinita) richiede la proprietà e `false` equivale a `not`.

* **profondità**

  Numero di livelli di caratteri jolly sotto i quali possono esistere la proprietà e il percorso relativo. Ad esempio, `property=size depth=2` controlla il nodo e le dimensioni, node/&amp;ast;/size e node/&amp;ast;/&amp;ast;/size.

### `rangeproperty` {#rangeproperty}

Corrisponde a una proprietà JCR rispetto a un intervallo. Si applica alle proprietà con tipi lineari, ad esempio `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE`, vedere il predicato dell&#39;intervallo di dati con input in formato data ottimizzato.

È possibile definire un limite inferiore e un limite superiore o solo uno di essi. L’operazione (ad esempio, &quot;minore di&quot; o &quot;minore o uguale a&quot;) può essere specificata anche per i limiti inferiore e superiore, singolarmente.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-16}

* **proprietà**

  Percorso relativo alla proprietà.

* **lowerBound**

  Limite inferiore per cui verificare la proprietà.

* **lowerOperation**

  &quot; `>`&quot; (impostazione predefinita) o &quot; `>=`&quot; si applica a `lowerValue`

* **upperBound**

  Limite superiore per cui verificare la proprietà.

* **upperOperation**

  &quot; `<`&quot; (impostazione predefinita) o &quot; `<=`&quot; si applica a `lowerValue`

* **decimale**

  &quot; `true`&quot; se la proprietà selezionata è di tipo Decimal

### `relativedaterange` {#relativedaterange}

Corrisponde a `JCR DATE` proprietà rispetto a un intervallo di data e ora utilizzando scostamenti di ora relativi all&#39;ora corrente del server. È possibile specificare `lowerBound` e `upperBound` utilizzando un valore di millisecondi o la sintassi bugzilla `1s 2m 3h 4d 5w 6M 7y`. Aggiungi il prefisso &quot;`-`&quot; per indicare uno scostamento negativo prima dell&#39;ora corrente. Se si specifica solo `lowerBound` o `upperBound`, l&#39;altro valore predefinito è 0, ovvero l&#39;ora corrente.

Ad esempio:

* `upperBound=1h` (e nessun `lowerBound`) selezionerebbe nulla nell&#39;ora successiva
* `lowerBound=-1d` (e nessun `upperBound`) avrebbe selezionato nulla nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` potrebbero selezionare qualsiasi elemento che abbia tra i 6 e i 3 mesi
* `lowerBound=-1500` e `upperBound=5500` potrebbero selezionare un valore compreso tra 1500 millisecondi nel passato e 5500 millisecondi nel futuro
* `lowerBound=1d` e `upperBound=2d` selezionerebbero qualsiasi elemento nel giorno successivo a domani

Non prende in considerazione anni bisestili e tutti i mesi sono 30 giorni.

Non supporta il filtro.

Supporta l’estrazione di sfaccettatura allo stesso modo del predicato dell’intervallo di dati.

#### Proprietà {#properties-17}

* **upperBound**

  Limite di data superiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto al tempo del server corrente, utilizzare &quot;-&quot; per offset negativo.

* **lowerBound**

  Limite di data inferiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto al tempo server corrente. Utilizzare &quot;-&quot; per ottenere un offset negativo.

### `root` {#root}

Gruppo di predicati radice. Supporta tutte le funzioni di un gruppo e consente di impostare i parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query, è implicito.

#### Proprietà {#properties-18}

* **p.offset**

  Numero che indica l&#39;inizio della pagina dei risultati, ovvero il numero di elementi da saltare.

* **p.limit**

  Numero che indica le dimensioni della pagina.

* **p.guessTotal**

  Per evitare il costo del calcolo di un totale completo dei risultati, non contare tutte le corrispondenze. Impostare invece un totale massimo per il conteggio fino a (ad esempio, `1000`) per fornire agli utenti una dimensione approssimativa e totali esatti per risultati più piccoli. Oppure impostarlo su `true` per contare solo fino al minimo richiesto: `p.offset + p.limit`.


* **p.excerpt**

  Se è impostato su &quot; `true`&quot;, includi un estratto di testo completo nel risultato.

* **p.hits**

  (solo per il servlet JSON) seleziona il modo in cui gli hit vengono scritti come JSON, con questi standard (estensibili tramite il servizio ResultHitWriter):

   * **semplice**:

     Elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostato).

   * **completo**:

     I risultati vengono visualizzati come JSON Sling per ogni nodo, con `jcr:path` che mostra il percorso hit. Per impostazione predefinita, la risposta include solo le proprietà dirette del nodo; utilizza `p.nodedepth=N` per includere contenuto più approfondito, dove `0` restituisce l&#39;intera sottostruttura. Impostare `p.acls=true` per includere le autorizzazioni JCR della sessione corrente per ogni elemento (`create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).


   * **selettivo**:

     La risposta include solo le proprietà elencate in `p.properties`, che è un elenco separato da spazi di percorsi relativi (utilizzare `+` negli URL). Se un percorso relativo ha una profondità maggiore di 1, l&#39;output lo nidifica come oggetto figlio. La proprietà speciale `jcr:path` include sempre il percorso hit.


### `savedquery` {#savedquery}

Include tutti i predicati di una query di generazione query persistente nella query corrente come predicato di sottogruppo.

Non esegue una query aggiuntiva, ma estende la query corrente.

Le query possono essere rese persistenti a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere una proprietà Stringa su più righe o un nodo `nt:file` che contiene la query come file di testo in formato proprietà Java™.

Non supporta l’estrazione dei facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **savedquery**

  Percorso della query salvata (proprietà String o nodo `nt:file`).

### `similar` {#similar}

Ricerca per affinità utilizzando JCR XPath `rep:similar()`.

Non supporta il filtro. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-20}

* **simili**
Percorso assoluto del nodo per il quale trovare nodi simili.

* **locale**
Percorso relativo di un nodo discendente o `.` per il nodo corrente (facoltativo, l&#39;impostazione predefinita è &quot; `.`&quot;).

### `tag` {#tag}

Cerca il contenuto con uno o più tag, specificando i percorsi dei titoli dei tag.

Supporta l’estrazione dei facet. Fornisce bucket per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **tag**

  Percorso del titolo del tag da cercare, ad esempio &quot;Proprietà risorsa: orientamento/orizzontale&quot;.

* **N_value**

  Utilizza `1_value`, `2_value`, ... per verificare la presenza di più tag (combinati con `OR` per impostazione predefinita, con `AND` se e=true) (dalla versione 5.6).

* **proprietà**

  Proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;)

### `tagid` {#tagid}

Cerca il contenuto con uno o più tag, specificando gli ID tag.

Supporta l’estrazione dei facet. Fornisce bucket per ogni tag univoco, utilizzando il relativo ID tag corrente.

#### Proprietà {#properties-22}

* **tagid**

  ID tag che consente di cercare, ad esempio, &quot; `properties:orientation/landscape`&quot;.

* **N_value**

  Utilizzare `1_value`, `2_value`, ... per verificare la presenza di più `tagids` (combinati con `OR` per impostazione predefinita, con `AND` se e=true) (dalla versione 5.6).

* **proprietà**

  Proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita &quot; `cq:tags`&quot;).

### `tagsearch` {#tagsearch}

Cerca il contenuto con uno o più tag, specificando le parole chiave. Cerca innanzitutto i tag che contengono queste parole chiave nei titoli, quindi limita il risultato solo agli elementi con tag.

Non supporta l’estrazione dei facet.

#### Proprietà {#Properties-1}

* **tagsearch**

  Parola chiave da cercare nei titoli dei tag.

* **proprietà**

  Proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita `cq:tags`).

* **lang**

  Per eseguire la ricerca solo in un determinato titolo di tag localizzato (ad esempio, `de`).

* **tutti**

  (bool) Cerca l&#39;intero testo completo del tag, ovvero tutti i titoli, la descrizione e così via. Ha la precedenza su &quot;l `ang`&quot;.

### `type` {#type}

Limita i risultati a un tipo di nodo JCR specifico, sia il tipo di nodo principale che il tipo mixin, e trova sottotipi di quel tipo di nodo. Gli indici di ricerca dell’archivio devono coprire i tipi di nodo per un’esecuzione efficiente.

Supporta l’estrazione dei facet. Fornisce bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **tipo**

  Tipo di nodo o nome mixin da cercare, ad esempio `cq:Page`.
