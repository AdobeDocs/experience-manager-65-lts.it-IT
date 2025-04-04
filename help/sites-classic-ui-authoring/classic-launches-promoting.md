---
title: Promozione dei lanci
description: Con la promozione delle pagine di lancio si sposta il contenuto nell’origine (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 1167735d-a13a-438e-bef8-205e27f59f4e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# Promozione dei lanci{#promoting-launches}

Con la promozione delle pagine di lancio si sposta il contenuto nell’origine (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa. Quando promuovi una pagina di lancio sono disponibili le seguenti opzioni:

* Promuovere solo la pagina corrente o l’intero lancio.
* Promuovere le pagine figlie della pagina corrente.
* Promuovere il lancio completo o solo le pagine che sono state modificate.

## Promozione delle pagine di lancio {#promoting-launch-pages}

Per promuovere le pagine, effettua le seguenti operazioni durante la modifica della pagina di lancio che desideri promuovere:

1. Nella scheda **Pagina** di Sidekick, fai clic su **Promuovi lancio**.
1. Specifica le pagine da promuovere:

   * Impostazione predefinita. Per promuovere solo la pagina corrente, selezionare **Promuovi modifiche pagina alla versione di produzione**.
   * Per promuovere anche le pagine figlie della pagina corrente, seleziona **Includi sottopagine**.
   * Per promuovere tutte le pagine del lancio, selezionare **Promuovi lancio completo alla versione produzione**.

1. Per aggiungere le pagine di produzione a un pacchetto flusso di lavoro, selezionare **Aggiungi al pacchetto flusso di lavoro**, quindi selezionare il pacchetto flusso di lavoro.
1. Fai clic su **Promuovi**.

## Elaborazione di pagine promosse tramite Flusso di lavoro AEM {#processing-promoted-pages-using-aem-workflow}

Utilizza i modelli di flusso di lavoro per eseguire l’elaborazione in blocco delle pagine di lanci promosse:

1. Crea un pacchetto flusso di lavoro.
1. Quando gli autori promuovono le pagine di lanci, queste vengono memorizzate nel pacchetto flusso di lavoro.
1. Avvia un modello di flusso di lavoro utilizzando il pacchetto come payload.

Per avviare automaticamente un flusso di lavoro quando le pagine vengono promosse, [configura un modulo di avvio del flusso di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) per il nodo del pacchetto.

Ad esempio, puoi generare automaticamente le richieste di attivazione pagina non appena un autore promuove una pagina di lancio. Configura un modulo di avvio del flusso di lavoro per avviare il flusso di lavoro Richiesta attivazione quando viene modificato il nodo del pacchetto.

![chlimage_1-136](assets/chlimage_1-136.png)
