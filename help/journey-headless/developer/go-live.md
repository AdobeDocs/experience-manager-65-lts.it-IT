---
title: Come pubblicare con la tua applicazione headless
description: In questa sezione del Percorso per sviluppatori AEM Headless, scopri come distribuire un’applicazione headless in tempo reale.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
exl-id: 8837e7cd-c949-46cc-9c39-3c7a82cc1daf
source-git-commit: 84ef35149332330e040b8d94cae151708e3c6829
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 53%

---

# Come pubblicare con la tua applicazione headless {#go-live}

In questa sezione del [Percorso di sviluppatori AEM Headless](overview.md), scopri come distribuire un&#39;applicazione headless live.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come aggiornare i contenuti tramite le API di AEM Assets](update-your-content.md) hai imparato ad aggiornare il contenuto headless esistente in AEM tramite API e ora dovresti:

* Comprendere l’API HTTP di AEM Assets.

Questo articolo si basa sulle nozioni di base che ti faranno capire come preparare il progetto AEM headless da pubblicare.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la pipeline di pubblicazione headless AEM e le considerazioni sulle prestazioni di cui devi tener conto prima di pubblicare l’applicazione.

* Scopri AEM SDK e gli strumenti di sviluppo necessari
* Imposta un runtime di sviluppo locale per simulare i contenuti prima della pubblicazione
* Nozioni di base sulla replica e il caching dei contenuti AEM
* Proteggi e ridimensiona l’applicazione prima del lancio
* Monitoraggio dei problemi di prestazioni e debug

## L’SDK di AEM {#the-aem-sdk}

L’SDK di AEM viene utilizzato per generare e distribuire il codice personalizzato. È lo strumento principale che devi sviluppare e testare la tua applicazione headless prima di andare &quot;live&quot;. Contiene i seguenti artefatti:

* Il file jar Quickstart: un file jar eseguibile che può essere utilizzato per impostare sia un’istanza di authoring che di pubblicazione
* Strumenti Dispatcher: il modulo Dispatcher e le sue dipendenze per i sistemi basati su Windows e UNIX
* Jar API Java™ - La dipendenza Java™ Jar/Maven che espone tutte le API Java™ consentite che possono essere utilizzate per lo sviluppo rispetto ad AEM
* Jar Javadoc: i javadoc per il jar API Java™

## Strumenti di sviluppo aggiuntivi {#additional-development-tools}

Oltre ad AEM SDK, è necessario disporre di strumenti aggiuntivi che facilitino lo sviluppo e il test locale del codice e del contenuto:

* Java™
* Git
* Apache Maven
* La libreria Node.js
* L’IDE che preferisci

Poiché AEM è un’applicazione Java™, è necessario installare Java™ e Java™ SDK per supportare lo sviluppo di AEM as a Cloud Service.

Git è ciò che utilizzerai per gestire il controllo del codice sorgente e per tenere traccia delle modifiche a Cloud Manager e, quindi, distribuirle su un’istanza di produzione.

AEM utilizza Apache Maven per creare progetti generati dall’archetipo del progetto Maven di AEM. Tutti gli IDE principali forniscono supporto per l’integrazione per Maven.

Node.js è un ambiente runtime di JavaScript utilizzato per lavorare con le risorse front-end del sottoprogetto `ui.frontend` di un progetto AEM. Node.js è distribuito con npm, che è de facto il gestore di pacchetti Node.js, utilizzato per gestire le dipendenze di JavaScript.

## Panoramica dei componenti di un sistema AEM {#components-of-an-aem-system-at-a-glance}

Ora, osserviamo le parti costitutive di un ambiente AEM.

Un ambiente AEM completo è costituito da authoring, pubblicazione e Dispatcher. Questi stessi componenti sono resi disponibili nel runtime di sviluppo locale per semplificare l’anteprima del codice e del contenuto prima della pubblicazione.

* Il **servizio di authoring** è il luogo in cui gli utenti interni creano, gestiscono e visualizzano in anteprima i contenuti.

* **Il servizio di pubblicazione** è considerato l&#39;ambiente &quot;live&quot; ed è normalmente ciò con cui gli utenti finali interagiscono. I contenuti, dopo essere stati modificati e approvati nel servizio di authoring, vengono distribuiti (replicati) nel servizio di pubblicazione. Il modello di implementazione più comune per le applicazioni headless AEM consiste nella connessione della versione di produzione dell’applicazione a un servizio di pubblicazione AEM.

* **Il Dispatcher** è un server web statico potenziato con il modulo Dispatcher di AEM. Memorizza nella cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

## Flusso di lavoro di sviluppo locale {#the-local-development-workflow}

Il progetto di sviluppo locale è basato su Apache Maven e utilizza Git per il controllo del codice sorgente. Per aggiornare il progetto, gli sviluppatori possono utilizzare, tra gli altri, il proprio ambiente di sviluppo integrato preferito, ad esempio Eclipse, Visual Studio Code o IntelliJ.

Per testare gli aggiornamenti del codice o del contenuto acquisiti dall’applicazione headless, distribuisci gli aggiornamenti nel runtime AEM locale. tra cui istanze locali dei servizi di authoring e pubblicazione di AEM.

Assicurati di prendere nota delle distinzioni tra ogni componente nel runtime AEM locale, in quanto è importante testare gli aggiornamenti dove contano di più. Ad esempio, prova gli aggiornamenti del contenuto sull’authoring o testa il nuovo codice sull’istanza di pubblicazione.

In un sistema di produzione, un Dispatcher e un server http Apache saranno sempre posti davanti a un’istanza di pubblicazione AEM. Fornisce servizi di caching e sicurezza per il sistema AEM, pertanto è fondamentale testare il codice e gli aggiornamenti di contenuto anche in Dispatcher.

## Anteprima del codice e del contenuto localmente con l’ambiente di sviluppo locale {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Per preparare il tuo progetto AEM headless per il lancio, assicurati che tutte le parti costitutive del progetto funzionino correttamente.

Per farlo, devi mettere insieme tutto: codice, contenuto e configurazione, e testarlo in un ambiente di sviluppo locale per la disponibilità alla pubblicazione.

L&#39;ambiente di sviluppo locale è costituito da tre aree principali:

1. Progetto AEM: contiene tutto il codice personalizzato, la configurazione e il contenuto su cui gli sviluppatori AEM stanno lavorando
1. Local AEM Runtime: versioni locali dei servizi di authoring e pubblicazione AEM utilizzati per distribuire il codice dal progetto AEM
1. Esecuzione del Dispatcher locale: una versione locale del server Web Apache httpd che include il modulo Dispatcher

Dopo aver configurato l’ambiente di sviluppo locale, puoi simulare il contenuto da distribuire all’app React distribuendo localmente un server Nodo statico.

Per informazioni più approfondite sulla configurazione di un ambiente di sviluppo locale e su tutte le dipendenze necessarie per l&#39;anteprima del contenuto, consulta [Documentazione sulla distribuzione di produzione](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=it).

## Prepara la tua applicazione AEM headless per il lancio {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Ora è il momento di preparare la tua applicazione headless AEM per il lancio, seguendo le best practice descritte di seguito.

### Protezione dell&#39;applicazione headless prima dell&#39;avvio {#secure-and-scale-before-launch}

1. Prepara [Autenticazione](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) per le richieste GraphQL

### Struttura del modello e output GraphQL {#structure-vs-output}

* Evita la creazione di query che generano più di 15 KB di JSON (gzip compresso). I file JSON lunghi richiedono un uso intensivo delle risorse per l’analisi da parte dell’applicazione client.
* Evita più di cinque livelli nidificati di gerarchie di frammenti. Livelli aggiuntivi rendono difficile per gli autori dei contenuti valutare l’impatto delle loro modifiche.
* Utilizza query con più oggetti invece di modellare query con gerarchie di dipendenza all’interno dei modelli. In questo modo si offre una flessibilità a lungo termine per ristrutturare l’output JSON senza dover apportare molte modifiche al contenuto.

### Massimizza il rapporto Hit-cache CDN {#maximize-cdn}

* Non utilizzare query GraphQL dirette, a meno che stia richiedendo contenuto in tempo reale dalla superficie.
   * Utilizza le query persistenti quando possibile.
   * Fornisci valori TTL CDN superiori a 600 secondi in modo che la CDN possa memorizzarli nella cache.
   * AEM può calcolare l’impatto di una modifica del modello sulle query esistenti.
* Suddividi le query JSON su file/GraphQL tra il tasso di modifica dei contenuti basso e alto per ridurre il traffico client su CDN e assegna un TTL più alto. In questo modo la rete CDN che riconvalida il JSON con il server di origine viene ridotta a icona.
* Per annullare attivamente la validità del contenuto dalla rete CDN, utilizza Soft Purge. In questo modo la rete CDN può scaricare nuovamente il contenuto senza causare un errore nella cache.

>[!NOTE]
>
>Consulta [Risorse aggiuntive](#additional-resources) per ulteriori informazioni su CDN e caching.

### Migliora il tempo di download dei contenuti headless {#improve-download-time}

* Assicurati che i client HTTP utilizzino HTTP/2.
* Assicurati che i client HTTP accettino la richiesta di intestazioni per gzip.
* Riduci al minimo il numero di domini utilizzati per ospitare JSON e gli artefatti di riferimento.
* Utilizza `Last-modified-since` per aggiornare le risorse.
* Utilizza l’output `_reference` nel file JSON per iniziare a scaricare risorse senza dover analizzare file JSON completi.

<!-- End of CDN Review -->

## Distribuzione alla produzione {#deploy-to-production}

La distribuzione in Produzione può dipendere dal fatto che tu disponga di un&#39;istanza di AEM *tradizionale* che distribuisce utilizzando Maven oppure di Adobe Managed Services (AMS) e quindi di Cloud Manager.

## Implementare in produzione utilizzando Maven {#deploy-to-production-maven}

Per una distribuzione *tradizionale* (non AMS) tramite Maven, consulta l&#39;[esercitazione WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=it#build) per una panoramica.

## Implementare in produzione utilizzando Cloud Manager {#deploy-to-production-cloud-manager}

Se sei un cliente AMS che utilizza Cloud Manager, dopo aver verificato che tutto sia stato testato e funzioni correttamente, puoi inviare gli aggiornamenti del codice a un [archivio Git centralizzato in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=it).

Dopo aver caricato gli aggiornamenti in Cloud Manager, distribuiscili in AEM utilizzando [la pipeline CI/CD di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=it).

<!-- Cannot find a parallel link -->
<!--
You can start deploying your code by using the Cloud Manager CI/CD pipeline, which is covered extensively - see the [Overview](/help/implementing/deploying/overview.md) to start.
-->

## Monitoraggio delle prestazioni {#performance-monitoring}

Per garantire agli utenti la migliore esperienza possibile quando utilizzano l’applicazione AEM headless, è importante monitorare le metriche delle prestazioni chiave, come illustrato di seguito:

* Convalida delle versioni di anteprima e di produzione dell’app
* Verifica delle pagine di stato di AEM per lo stato di disponibilità del servizio corrente
* Accesso ai rapporti sulle prestazioni
   * Prestazioni della distribuzione
      * Server di origine - numero di chiamate, tassi di errore, carichi della CPU, traffico del payload
   * Prestazioni dell’authoring
      * Verifica il numero di utenti, richieste e caricamento
* Accedere ai rapporti sulle prestazioni specifici per app e spazio
   * Una volta che il server è attivo, controllare se le metriche generali sono verde/arancione/rosso, quindi identificare problemi specifici dell’app
   * Aprire i rapporti di cui sopra, filtrati per app o spazio (ad esempio Photoshop per desktop, paywall)
   * Utilizzare le API del registro Splunk per accedere alle prestazioni del servizio e dell’applicazione
   * Contattare l’Assistenza clienti in caso di altri problemi.

## Risoluzione dei problemi {#troubleshooting}

### Debugging {#debugging}

Segui queste best practice come approccio generale al debug:

* Convalida funzionalità e prestazioni con la versione di anteprima dell’applicazione
* Convalida funzionalità e prestazioni con la versione di produzione dell’applicazione
* Convalida con JSON l’anteprima dell’Editor di frammento di contenuto
* Per verificare la presenza di problemi di consegna o applicazione client, esamina il JSON nell’applicazione client
* Per verificare la presenza di problemi relativi al contenuto memorizzato in cache o ad AEM, controlla il JSON utilizzando GraphQL

### Registrazione di un bug con Support {#logging-a-bug-with-support}

Per segnalare in modo efficiente un bug con il supporto, nel caso sia necessaria ulteriore assistenza, completa i passaggi seguenti:

* Se necessario, acquisisci le schermate del problema
* Documenta un modo per riprodurre il problema
* Documenta il contenuto con cui il problema si ripresenta
* Segnala un problema tramite il portale di supporto AEM con la priorità appropriata

## Il percorso è terminato - Davvero? {#journey-ends}

Congratulazioni. Hai completato il Percorso per sviluppatori AEM headless! Ora dovresti aver appreso quanto segue:

* La differenza tra distribuzione headless e headful dei contenuti.
* Le funzionalità headless di AEM.
* Come organizzare un progetto AEM headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come pubblicare con un progetto AEM headless.
* Cosa fare dopo il completamento del go-live.

Hai già avviato il tuo primo progetto AEM Headless o ora disponi di tutte le conoscenze necessarie per farlo. Ottimo lavoro!

### Esplora le applicazioni a pagina singola {#explore-spa}

Tuttavia, non è necessario arrestare i negozi headless in AEM. Nella sezione [Guida introduttiva del percorso](getting-started.md#integration-levels), è stato discusso il modo in cui AEM non solo supporta la distribuzione headless e i modelli full stack tradizionali, ma supporta anche modelli ibridi che combinano i vantaggi di entrambi.

Se questo tipo di flessibilità è necessario per il progetto, passare alla sezione facoltativa aggiuntiva del percorso [Come creare applicazioni a pagina singola con AEM.](create-spa.md)

## Risorse aggiuntive {#additional-resources}

* [Guida allo sviluppo di AEM](/help/sites-developing/the-basics.md)

* [Esercitazione WKND](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview)

* [Cloud Manager per AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it)

* Cache CDN

   * [Controllo di una cache CDN](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it#controlling-a-cdn-cache)

   * Configurazione del [rewriter CDN](/help/sites-deploying/osgi-configuration-settings.md) (*cerca rewriter CDN*)

* [Introduzione ad AEM come CMS headless](/help/sites-developing/headless/introduction.md)
* [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorial per contenuti headless in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it)
