---
title: Architettura dei contenuti
description: 'Suggerimenti per l’architettura dei contenuti (suggerimento: tutto è contenuto)'
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: eb47f730-ac26-47a0-9bd7-3b7e94c79ecd
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Architettura dei contenuti{#content-architecture}

## Segui il modello di David {#follow-david-s-model}

David Nuescheler ha scritto il modello di David anni fa, ma le sue idee sono ancora vere oggi. I principi principali del modello di David sono i seguenti:

* I dati vengono prima, struttura dopo. Forse.
* Guidare la gerarchia dei contenuti; evitare che ciò accada.
* Le aree di lavoro sono per `clone()`, `merge()` e `update()`.
* Attenzione agli stessi fratelli e sorelle.
* I riferimenti possono essere considerati dannosi.
* I file sono file.
* Gli ID sono malvagi.

Il modello di David si trova nel wiki Jackrabbit all&#39;indirizzo [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Tutto è contenuto {#everything-is-content}

Tutto deve essere archiviato nell’archivio anziché affidarsi a origini dati separate di terze parti, come i database. Un approccio di questo tipo si applica ai contenuti creati, ai dati binari come immagini, codice e configurazioni. Ci consente di utilizzare un unico set di API per gestire tutti i contenuti e per gestirne la promozione tramite la replica. Inoltre, è possibile ottenere un&#39;unica fonte di backup, registrazione e così via.

### Utilizza il principio di progettazione &quot;prima il modello di contenuto&quot; {#use-the-content-model-first-design-principle}

Quando crei una nuova funzione, inizia sempre progettando prima la struttura del contenuto JCR, quindi cerca di leggere e scrivere il contenuto utilizzando i servlet Sling predefiniti. Tale approccio consente di garantire il corretto funzionamento dell’implementazione con meccanismi di controllo dell’accesso predefiniti, evitando di generare servlet di tipo CRUD non necessari.

### Essere RESTful {#be-restful}

Definisci i servlet in base a resourceTypes anziché ai percorsi. Questo approccio consente di utilizzare i controlli di accesso JCR, rispettare i principi REST e utilizzare le risorse e il risolutore risorse forniti nella richiesta. Questo approccio consente di modificare gli script che eseguono il rendering degli URL sul lato server senza modificare gli URL lato client. Inoltre, nasconde al client i dettagli di implementazione lato server per una maggiore sicurezza.

### Evita di definire nuovi tipi di nodo {#avoid-defining-new-node-types}

I tipi di nodo funzionano a un livello basso nel livello dell’infrastruttura. La maggior parte dei requisiti viene soddisfatta utilizzando un `sling:resourceType` assegnato a un tipo di nodo `nt:unstructured`, `oak:Unstructured`, `sling:Folder` o `cq:Page`. I tipi di nodo equivalgono allo schema nell’archivio e la modifica dei tipi di nodo può risultare costosa in qualsiasi momento.

### Rispettare le convenzioni di denominazione nel JCR {#adhere-to-naming-conventions-in-the-jcr}

Il rispetto delle convenzioni di denominazione aggiunge coerenza alla base di codice, riducendo il tasso di incidenza dei difetti e aumentando la velocità degli sviluppatori che lavorano nel sistema. Adobe utilizza le seguenti convenzioni per lo sviluppo di AEM:

* Nomi di nodo

   * Tutte minuscole.
   * Separazione delle parole mediante trattini.

* Nomi di proprietà

   * Camel case, a partire da una lettera minuscola.

* Componenti (JSP/HTML)

   * Tutte minuscole.
   * Separazione delle parole mediante trattini.
