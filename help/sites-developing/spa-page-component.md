---
title: Componente pagina SPA
description: In un’applicazione a pagina singola, il componente pagina non fornisce gli elementi HTML dei suoi componenti secondari, ma lo delega al framework dell’applicazione a pagina singola. Questo documento spiega come questo renda univoco il componente Pagina di un’applicazione a pagina singola.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 470636ce-3934-4aac-80ff-1fe6bd84455e
index: false
source-git-commit: f6a3d16c55a6b62aea9a374904339e16d30f0a75
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 6%

---


# Componente pagina SPA{#spa-page-component}

In un’applicazione a pagina singola, il componente pagina non fornisce gli elementi HTML dei suoi componenti secondari, ma lo delega al framework dell’applicazione a pagina singola. Questo documento spiega come questo renda univoco il componente Pagina di un’applicazione a pagina singola.

{{ue-over-spa}}

## Introduzione {#introduction}

Il componente page di un’applicazione a pagina singola non fornisce gli elementi HTML dei suoi componenti secondari tramite un file JSP o HTL e oggetti risorsa. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti figlio viene recuperata come struttura di dati JSON (ovvero come modello). I componenti SPA vengono quindi aggiunti alla pagina in base al modello JSON fornito. Di conseguenza, la composizione del corpo iniziale del componente Pagina è diversa dalle controparti di HTML sottoposte a rendering preliminare.

## Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a un modulo [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) fornito. L&#39;applicazione a pagina singola deve interagire con il modulo `PageModelManager` quando viene inizializzato per recuperare il modello della pagina iniziale e registrarsi per gli aggiornamenti del modello, per lo più prodotti quando l&#39;autore modifica la pagina tramite l&#39;Editor pagina. `PageModelManager` è accessibile dal progetto SPA come pacchetto npm. Essendo un interprete tra AEM e l&#39;applicazione a pagina singola, `PageModelManager` deve accompagnare l&#39;applicazione a pagina singola.

Per consentire la creazione della pagina, è necessario aggiungere una libreria client denominata `cq.authoring.pagemodel.messaging` per fornire un canale di comunicazione tra l&#39;applicazione a pagina singola e l&#39;editor di pagine. Se il componente pagina di applicazioni a pagina singola eredita dal componente wcm/core della pagina, sono disponibili le seguenti opzioni per rendere disponibile la categoria di librerie client `cq.authoring.pagemodel.messaging`:

* Se il modello è modificabile, aggiungi la categoria della libreria client al criterio della pagina.
* Aggiungi la categoria della libreria client utilizzando `customfooterlibs.html` del componente pagina.

Non dimenticare di limitare l&#39;inclusione della categoria `cq.authoring.pagemodel.messaging` al contesto dell&#39;editor pagina.

## Tipo di dati di comunicazione {#communication-data-type}

Il tipo di dati di comunicazione è impostato come elemento HTML all&#39;interno del componente AEM Page utilizzando l&#39;attributo `data-cq-datatype`. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste GET raggiungono gli endpoint del modello Sling di un componente. Dopo che si verifica un aggiornamento nell’editor di pagine, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello di pagina. La libreria Modello pagina avvisa quindi l’applicazione a pagina singola dell’esistenza di aggiornamenti.

**Componente pagina SPA -`body.html`**

```
<div id="page"></div>
```

Oltre a essere una buona pratica per non ritardare la generazione DOM, il framework SPA richiede che gli script vengano aggiunti alla fine del corpo.

**Componente pagina SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Le proprietà della metarisorsa che descrivono il contenuto dell’applicazione a pagina singola:

**Componente pagina SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Il selettore del modello di default è impostato in modo statico quando si richiede la rappresentazione del modello Sling di un componente.

## Metaproprietà {#meta-properties}

* `cq:wcmmode`: modalità WCM degli editor (ad esempio, pagina, modello)
* `cq:pagemodel_root_url`: URL del modello radice dell&#39;app. Fondamentale quando si accede direttamente a una pagina figlio, poiché il modello di pagina figlio è un frammento del modello principale dell’app. ` [PageModelManager](/help/sites-developing/spa-page-component.md)` ricompone quindi in modo sistematico il modello iniziale dell&#39;applicazione immettendo l&#39;applicazione dal relativo punto di ingresso radice.

* `cq:pagemodel_router`: abilitare o disabilitare ` [ModelRouter](/help/sites-developing/spa-routing.md)` della libreria `PageModelManager`

* `cq:pagemodel_route_filters`: elenco separato da virgole o espressioni regolari per fornire route che ` [ModelRouter](/help/sites-developing/spa-routing.md)` deve ignorare.

>[!CAUTION]
>
>Questo documento utilizza l&#39;app We.Retail Journal solo a scopo dimostrativo. Non utilizzare per alcun lavoro di progetto.
>
>Qualsiasi progetto AEM deve utilizzare l&#39;[Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta i progetti SPA tramite React o Angular e utilizza l&#39;SPA SDK. Tutti i progetti SPA in AEM devono essere basati sull&#39;Archetipo Maven per l&#39;SPA Starter Kit.

## Sincronizzazione sovrapposizione editor pagina {#page-editor-overlay-synchronization}

La sincronizzazione delle sovrapposizioni è garantita dallo stesso Mutation Observer fornito dalla categoria `cq.authoring.page`.

## Configurazione della struttura esportata JSON del modello Sling {#sling-model-json-exported-structure-configuration}

Quando le funzionalità di routing sono abilitate, si presume che l’esportazione JSON dell’applicazione a pagina singola contenga le diverse route dell’applicazione grazie all’esportazione JSON del componente di navigazione AEM. L’output JSON del componente di navigazione AEM può essere configurato nel criterio del contenuto della pagina principale dell’applicazione a pagina singola tramite le due proprietà seguenti:

* `structureDepth`: numero corrispondente alla profondità dell&#39;albero esportato
* `structurePatterns`: Regex dell&#39;array di regex corrispondenti alla pagina da esportare

È possibile visualizzarlo nel contenuto di esempio dell&#39;applicazione a pagina singola in `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
