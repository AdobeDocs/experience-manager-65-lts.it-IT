---
title: Invio asincrono di moduli adattivi
description: Scopri come configurare l’invio asincrono per i moduli adattivi.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: df2621db-59a1-4031-8856-7c2de766c099
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Invio asincrono di moduli adattivi{#asynchronous-submission-of-adaptive-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html?lang=it) |
| AEM 6.5 | Questo articolo |

In genere, i moduli web sono configurati per l’invio sincrono. Nell’invio sincrono, quando gli utenti inviano un modulo, vengono reindirizzati a una pagina di conferma, a una pagina di ringraziamento oppure, se l’invio non riesce, a una pagina di errore. Tuttavia, le moderne esperienze web come le applicazioni a pagina singola stanno guadagnando popolarità, dove la pagina web rimane statica mentre l’interazione client-server avviene in background. Ora puoi fornire questa esperienza con i moduli adattivi configurando l’invio asincrono.

Nell’invio asincrono, quando un utente invia un modulo, lo sviluppatore del modulo inserisce un’esperienza separata, ad esempio il reindirizzamento verso un altro modulo o una sezione separata del sito web. L’autore può anche inserire servizi separati come l’invio di dati a un altro archivio dati o aggiungere un motore di analisi personalizzato. In caso di invio asincrono, un modulo adattivo si comporta come un’applicazione a pagina singola poiché il modulo non viene ricaricato o il suo URL non cambia quando i dati del modulo inviati vengono convalidati sul server.

Continua a leggere per informazioni dettagliate sull’invio asincrono nei moduli adattivi.

## Configurare l’invio asincrono {#configure}

Per configurare l’invio asincrono per un modulo adattivo:

1. In modalità di creazione di moduli adattivi, seleziona l’oggetto Contenitore modulo e seleziona ![cmppr1](assets/cmppr1.png) per aprirne le proprietà.
1. Nella sezione delle proprietà **[!UICONTROL Invio]**, abilita **[!UICONTROL Usa invio asincrono]**.
1. Nella sezione **[!UICONTROL All&#39;invio]**, selezionare una delle opzioni seguenti da eseguire in caso di invio del modulo corretto.

   * **[!UICONTROL Reindirizza all&#39;URL]**: reindirizza all&#39;URL o alla pagina specificata all&#39;invio del modulo. Puoi specificare un URL o sfogliare per scegliere il percorso di una pagina nel campo **[!UICONTROL URL/percorso di reindirizzamento]**.
   * **[!UICONTROL Mostra messaggio]**: visualizza un messaggio all&#39;invio del modulo. Puoi scrivere un messaggio nel campo di testo sotto l’opzione Mostra messaggio. Il campo di testo supporta la formattazione RTF.

1. Selezionare ![check-button1](assets/check-button1.png) per salvare le proprietà.

## Funzionamento dell’invio asincrono {#how-asynchronous-submission-works}

AEM Forms fornisce gestori predefiniti di successo e di errori per l’invio di moduli. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un modulo viene inviato, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento di successo o errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione.

Inoltre, gli autori e gli sviluppatori di moduli possono scrivere regole a livello di modulo per ignorare i gestori predefiniti. Per ulteriori informazioni, vedere [Sostituire i gestori predefiniti tramite le regole](#custom).

Esaminiamo innanzitutto la risposta del server per gli eventi di successo e di errore.

### Risposta del server per l’evento di successo dell’invio {#server-response-for-submission-success-event}

La struttura della risposta del server per l’evento di successo dell’invio è la seguente:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

La risposta del server in caso di invio corretto del modulo include:

* Tipo di formato dati modulo: XML o JSON
* Dati modulo in formato XML o JSON
* Opzione selezionata per reindirizzare a una pagina o visualizzare un messaggio come configurato nel modulo
* Contenuto dell’URL della pagina o del messaggio configurato nel modulo

Il gestore dei processi riusciti legge la risposta del server e di conseguenza reindirizza all’URL della pagina configurato o visualizza un messaggio.

### Risposta del server per l’evento di errore di invio {#server-response-for-submission-error-event}

La struttura della risposta del server per l’evento di errore di invio è la seguente:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La risposta del server in caso di errore nell’invio del modulo include:

* Motivo dell’errore, convalida CAPTCHA o lato server non riuscita
* Elenco di oggetti errore, che include l&#39;espressione SOM del campo che non ha superato la convalida e il messaggio di errore corrispondente

Il gestore degli errori legge la risposta del server e visualizza di conseguenza il messaggio di errore nel modulo.

## Ignora gestori predefiniti tramite regole {#custom}

Gli sviluppatori e gli autori di moduli possono scrivere regole, a livello di modulo, nell’editor di codice per ignorare i gestori predefiniti. La risposta del server per eventi di successo ed errore è esposta a livello di modulo, a cui gli sviluppatori possono accedere utilizzando `$event.data` nelle regole.

Per scrivere regole nell’editor di codice per gestire gli eventi di successo e di errore, effettua le seguenti operazioni.

1. Apri il modulo adattivo in modalità di creazione, seleziona un oggetto modulo qualsiasi, quindi seleziona ![modifica-regole1](assets/edit-rules1.png) per aprire l’editor di regole.
1. Selezionare **[!UICONTROL Modulo]** nella struttura Oggetti modulo e selezionare **[!UICONTROL Crea]**.
1. Seleziona **[!UICONTROL Editor di codice]** dal menu a discesa per la selezione della modalità.
1. Nell&#39;editor di codice, selezionare **[!UICONTROL Modifica codice]**. Seleziona **[!UICONTROL Modifica]** nella finestra di conferma.
1. Scegliere **[!UICONTROL Invio riuscito]** o **[!UICONTROL Errore nell&#39;invio]** dal menu a discesa **[!UICONTROL Evento]**.
1. Scrivere una regola per l&#39;evento selezionato e selezionare **[!UICONTROL Fine]** per salvare la regola.
