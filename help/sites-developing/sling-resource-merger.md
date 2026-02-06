---
title: Utilizzare Sling Resource Merger in AEM
description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6fb6e522-fb81-4ba2-90b2-aad68f8bfa9e
source-git-commit: 9bc1cad84bb14b7513ede1fff2c1a37768dac442
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# Utilizzare Sling Resource Merger in AEM{#using-the-sling-resource-merger-in-aem}

## Scopo {#purpose}

Sling Resource Merger fornisce servizi per accedere e unire le risorse. Fornisce meccanismi di differenze per entrambi:

* **[Sovrapposizioni](/help/sites-developing/overlays.md)** di risorse utilizzando [percorsi di ricerca configurati](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Esegue l&#39;override** delle finestre di dialogo dei componenti per l&#39;interfaccia utente touch (`cq:dialog`), utilizzando la gerarchia dei tipi di risorsa (tramite la proprietà `sling:resourceSuperType`).

Sling Resource Merger combina le risorse di sovrapposizione e di sostituzione (e le relative proprietà) con le risorse e le proprietà originali:

* Il contenuto della definizione personalizzata ha una priorità più alta rispetto all’originale. Ciò significa che *sovrappone* o *sovrascrive*.

* Se necessario, [proprietà](#properties) definite nella personalizzazione, indicano come deve essere utilizzato il contenuto unito dall&#39;originale.

>[!CAUTION]
>
>Sling Resource Merger e i metodi correlati possono essere utilizzati solo con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html). Questa situazione significa anche che è appropriata solo per l’interfaccia utente standard touch; in particolare, le sostituzioni definite in questo modo sono applicabili solo alla finestra di dialogo touch di un componente.
>
>Per sovrapporre o sostituire altre aree (incluse altre parti di un componente touch o dell’interfaccia classica), copia il nodo e la struttura appropriati dall’originale. Posizionate la copia nel punto in cui definite la personalizzazione.

### Obiettivi per AEM {#goals-for-aem}

Gli obiettivi per utilizzare Sling Resource Merger in AEM sono i seguenti:

* assicurarsi che le modifiche di personalizzazione non vengano apportate in `/libs`.
* ridurre la struttura replicata da `/libs`.

  Quando si utilizza Sling Resource Merger, non è consigliabile copiare l&#39;intera struttura da `/libs`. Il motivo è che nella personalizzazione vengono conservate troppe informazioni (in genere `/apps`). La duplicazione delle informazioni aumenta inutilmente la possibilità di problemi durante l&#39;aggiornamento del sistema.

>[!NOTE]
>
>Le sostituzioni non dipendono dai percorsi di ricerca. Utilizzano la proprietà `sling:resourceSuperType` per effettuare la connessione.
>
>Tuttavia, le sostituzioni sono spesso definite in `/apps`, poiché in AEM è consigliabile definire le personalizzazioni in `/apps`. Il motivo è che non devi modificare nulla in `/libs`.

>[!CAUTION]
>
>*Non* modificare nulla nel percorso `/libs`.
>
>Il motivo è che il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza. Inoltre, potrebbe anche essere sovrascritto quando si applica un hotfix o un feature pack.
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l&#39;elemento richiesto (ovvero, poiché esiste in `/libs`) in `/apps`
>
>1. Apporta le modifiche in `/apps`
>

### Proprietà {#properties}

La fusione delle risorse fornisce le seguenti proprietà:

* `sling:hideProperties` ( `String` o `String[]`)

  Specifica la proprietà o l&#39;elenco di proprietà da nascondere.

  Il carattere jolly `*` nasconde tutto.

* `sling:hideResource` ( `Boolean`)

  Indica se le risorse sono completamente nascoste, inclusi i relativi elementi secondari.

* `sling:hideChildren` ( `String` o `String[]`)

  Contiene il nodo figlio, o elenco di nodi figlio, da nascondere. Le proprietà del nodo vengono mantenute.

  Il carattere jolly `*` nasconde tutto.

* `sling:orderBefore` ( `String`)

  Contiene il nome del nodo di pari livello su cui è posizionato il nodo corrente.

Queste proprietà influiscono sul modo in cui le risorse/proprietà corrispondenti/originali (da `/libs`) vengono utilizzate dalla sovrapposizione/esclusione (spesso in `/apps`).

### Creare la struttura {#creating-the-structure}

Per creare una sovrapposizione o una sostituzione è necessario ricreare il nodo originale, con la struttura equivalente, nella destinazione (in genere `/apps`). Ad esempio:

* Sovrapposizione

   * La definizione della voce di navigazione per la console Sites, come mostrato nella barra, è definita in:

     `/libs/cq/core/content/nav/sites/jcr:title`

   * Per sovrapporre, crea il seguente nodo:

     `/apps/cq/core/content/nav/sites`

     Quindi aggiornare la proprietà `jcr:title` come richiesto.

* Sostituisci

   * La definizione della finestra di dialogo touch per la console Testi è la seguente:

     `/libs/foundation/components/text/cq:dialog`

   * Per eseguire l’override, crea il seguente nodo. Ad esempio:

     `/apps/the-project/components/text/cq:dialog`

Per creare una di queste, dovete solo ricreare la struttura dell&#39;ossatura. Per semplificare la ricreazione della struttura, tutti i nodi intermedi possono essere di tipo `nt:unstructured` (non devono necessariamente riflettere il tipo di nodo originale. Ad esempio, in `/libs`.

Nell’esempio di sovrapposizione precedente, sono quindi necessari i seguenti nodi:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Quando si utilizza Sling Resource Merger (ovvero quando si tratta dell&#39;interfaccia utente standard touch) non è consigliabile copiare l&#39;intera struttura da `/libs`. Il motivo è che in `/apps` verrebbero conservate troppe informazioni. Di conseguenza, può causare problemi durante l&#39;aggiornamento del sistema.

### Casi d’uso {#use-cases}

Con la funzionalità standard, questi casi d’uso ti consentono di effettuare le seguenti operazioni:

* **Aggiungi una proprietà**

  La proprietà non esiste nella definizione `/libs`, ma è obbligatoria nella sovrapposizione o sostituzione `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea la nuova proprietà su questo nodo &quot;

* **Ridefinire una proprietà (proprietà non create automaticamente)**

  La proprietà è definita in `/libs`, ma è necessario un nuovo valore nella sovrapposizione/esclusione di `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea la proprietà corrispondente su questo nodo (in `apps`)

      * La proprietà ha una priorità in base alla configurazione di Sling Resource Resolver.
      * È supportata la modifica del tipo di proprietà.

        Se si utilizza un tipo di proprietà diverso da quello utilizzato in `/libs`, verrà utilizzato il tipo di proprietà definito.

  >[!NOTE]
  >
  >È supportata la modifica del tipo di proprietà.

* **Ridefinire una proprietà creata automaticamente**

  Per impostazione predefinita, le proprietà create automaticamente (come `jcr:primaryType`) non sono soggette a sovrapposizione/override per garantire che il tipo di nodo attualmente in `/libs` sia rispettato. Per imporre una sovrapposizione/esclusione è necessario ricreare il nodo in `/apps`, nascondere esplicitamente la proprietà e ridefinirla:

   1. Crea il nodo corrispondente in `/apps` con `jcr:primaryType` desiderato
   1. Creare la proprietà `sling:hideProperties` su tale nodo, con il valore impostato su quello della proprietà creata automaticamente, ad esempio `jcr:primaryType`

      Questa proprietà, definita in `/apps`, ha ora la priorità rispetto a quella definita in `/libs`

* **Ridefinire un nodo e i relativi elementi secondari**

  Il nodo e i relativi nodi secondari sono definiti in `/libs`, ma è necessaria una nuova configurazione nella sovrapposizione/esclusione di `/apps`.

   1. Combina le azioni di:

      1. Nascondi elementi figlio di un nodo (mantenendo le proprietà del nodo)
      1. Ridefinisci la proprietà / proprietà

* **Nascondi una proprietà**

  La proprietà è definita in `/libs`, ma non è richiesta nella sovrapposizione o sostituzione `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Creare una proprietà `sling:hideProperties` di tipo `String` o `String[]`. Consente di specificare le proprietà da nascondere o ignorare. È inoltre possibile utilizzare i caratteri jolly. Ad esempio:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Nascondi un nodo e i relativi elementi secondari**

  Il nodo e i relativi nodi secondari sono definiti in `/libs`, ma non sono obbligatori nella sovrapposizione/esclusione di `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea una proprietà `sling:hideResource`

      * tipo: `Boolean`
      * valore: `true`

* **Nascondi elementi figlio di un nodo (mantenendo le proprietà del nodo)**

  Il nodo, le relative proprietà e i relativi elementi figlio sono definiti in `/libs`. Il nodo e le relative proprietà sono obbligatori nella sovrapposizione o sostituzione `/apps`, ma alcuni o tutti i nodi figlio non sono obbligatori nella sovrapposizione o sostituzione `/apps`.

   1. Crea il nodo corrispondente in `/apps`
   1. Creare la proprietà `sling:hideChildren`:

      * tipo: `String[]`
      * valore: elenco dei nodi figlio (come definiti in `/libs`) da nascondere/ignorare

      Il carattere jolly &amp;ast; può essere utilizzato per nascondere o ignorare tutti i nodi figlio.

* **Riordina nodi**

  Nodo e relativi elementi di pari livello definiti in `/libs`. Per modificare l&#39;ordine, ricreare il nodo nella sovrapposizione o sostituzione `/apps`. Definire la nuova posizione facendo riferimento al nodo di pari livello appropriato in `/libs`.


   * Utilizzare la proprietà `sling:orderBefore`:

      1. Crea il nodo corrispondente in `/apps`
      1. Creare la proprietà `sling:orderBefore`:

         Specifica il nodo (come in `/libs`) prima del quale è posizionato il nodo corrente:

         * tipo: `String`
         * valore: `<before-SiblingName>`

### Richiama Sling Resource Merger dal codice {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger include due provider di risorse personalizzati: uno per le sovrapposizioni e l’altro per le sostituzioni. Ciascuno può essere richiamato all’interno del codice utilizzando un punto di montaggio:

>[!NOTE]
>
>Quando si accede alla risorsa, si consiglia di utilizzare il punto di montaggio appropriato.
>
>Questo approccio richiama Sling Resource Merger e restituisce la risorsa completamente unita. Riduce inoltre la quantità di struttura da copiare da `/libs`.

* Sovrapposizione:

   * finalità: unire le risorse in base al relativo percorso di ricerca
   * punto di montaggio: `/mnt/overlay`
   * utilizzo: `mount point + relative path`
   * esempio:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Sostituisci:

   * finalità: unire le risorse in base al loro super tipo
   * punto di montaggio: `/mnt/overide`
   * utilizzo: `mount point + absolute path`
   * esempio:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Esempio di utilizzo {#example-of-usage}

Alcuni esempi sono trattati:

* Sovrapposizione:

   * [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
   * [Personalizzazione dell’authoring pagina](/help/sites-developing/customizing-page-authoring-touch.md)

* Sostituisci:

   * [Configurazione delle proprietà della pagina](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
