---
title: Sviluppo e differenze tra pagine
description: Scopri come sviluppare e utilizzare la funzione di differenze tra pagine in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 10%

---

# Sviluppo e differenze tra pagine{#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. L’autore vuole poter confrontare la pagina corrente con una versione precedente evidenziando le differenze.

La differenza di pagina consente a un utente di confrontare la pagina corrente con lanci, versioni precedenti e così via. Per informazioni dettagliate su questa funzionalità utente, vedere [Differenze tra pagine](/help/sites-authoring/page-diff.md).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l’utente desidera confrontare viene ricreata da AEM in background per facilitare le differenze. Questo è necessario per poter eseguire il rendering del contenuto [per il confronto affiancato](/help/sites-developing/pagediff.md#operation-details).

Questa operazione di ricreazione viene eseguita internamente da AEM, è trasparente per l’utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l’archivio, ad esempio, in CRXDE Lite vedrebbe queste versioni ricreate all’interno della struttura del contenuto.

Quando si confronta il contenuto, l’intera struttura fino alla pagina da confrontare viene ricreata nella seguente posizione:

`/tmp/versionhistory/`

Un’attività di pulizia viene eseguita automaticamente per pulire questo contenuto temporaneo.

## Autorizzazioni {#permissions}

In precedenza, nell’interfaccia classica, era necessario prestare particolare attenzione allo sviluppo per facilitare la differenziazione di AEM (ad esempio utilizzando la libreria di tag `cq:text` o integrando in modo personalizzato il servizio OSGi `DiffService` nei componenti). Questa funzione non è più necessaria per la nuova funzione di differenze, poiché la differenza si verifica lato client tramite il confronto DOM.

Tuttavia, ci sono alcune limitazioni che devono essere considerate dallo sviluppatore.

* Questa funzione utilizza classi CSS che non fanno parte del namespace per il prodotto AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione delle differenze potrebbe esserne influenzata.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Poiché la differenze è lato client ed viene eseguita al caricamento della pagina, eventuali modifiche apportate al DOM dopo l’esecuzione del servizio differenze lato client non verranno contabilizzate. Questo può influire

   * Componenti che utilizzano AJAX per includere i contenuti
   * Applicazioni a pagina singola
   * Componenti basati su JavaScript che manipolano il DOM in base all’interazione dell’utente.

>[!NOTE]
>
>Il confronto delle differenze di pagina funziona solo per i componenti che hanno nodi cq:editConfig validi.
