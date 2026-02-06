---
title: L’editor universale
description: Scopri la flessibilità di Universal Editor e come può aiutare a potenziare le esperienze headless utilizzando AEM 6.5 LTS.
feature: Developing
role: Developer
exl-id: 495df631-5bdd-456b-b115-ec8561f33488
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 42%

---

# Informazioni sull’editor universale {#universal-editor}

Scopri la flessibilità di Universal Editor e come può aiutare a potenziare le esperienze headless utilizzando AEM 6.5 LTS.

## Panoramica {#overview}

L’editor universale è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di modificare ciò che si vede è ciò che si ottiene (WYSIWYG) di qualsiasi esperienza headless.

* Gli autori possono trarre vantaggio dalla flessibilità di Universal Editor. Supporta lo stesso editing visivo coerente per tutte le forme di contenuti headless AEM.
* Gli sviluppatori traggono vantaggio dalla versatilità dell’editor universale, che supporta un vero e proprio disaccoppiamento dell’implementazione. Consente agli sviluppatori di utilizzare virtualmente qualsiasi framework o architettura a loro scelta, senza imporre alcun vincolo di SDK o tecnologia.

Per maggiori dettagli, consulta la [documentazione di AEM as a Cloud Service nell&#39;editor universale](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction).

## Architettura {#architecture}

L’editor universale è un servizio che funziona insieme ad AEM per creare contenuti in modo headless.

* L&#39;editor universale è ospitato in `https://experience.adobe.com/#/aem/editor/canvas` e può modificare le pagine sottoposte a rendering da AEM 6.5 LTS.
* L’editor universale legge la pagina AEM tramite Dispatcher dall’istanza di authoring AEM.
* Il servizio Editor universale, che viene eseguito sullo stesso host di Dispatcher, riscrive le modifiche nell’istanza di authoring di AEM.

![Flusso di creazione di contenuti con l’editor universale](assets/author-flow.png)

## Requisiti {#requirements}

Di seguito è riportato il supporto di Universal Editor:

* AEM 6.5 LTS GA
   * Sono supportati sia l’hosting on-premise che Adobe Managed Services (AMS).
* [AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * Sono supportati sia l’hosting on-premise che AMS.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) (versione `2023.8.13099` o successiva)

Questo documento si concentra sul supporto AEM 6.5 LTS di Universal Editor. Per utilizzare l’Editor universale con AEM 6.5 LTS, è necessario quanto segue:

* AEM 6.5 LTS GA
* Dispatcher configurato correttamente

## Configurazione {#setup}

Per utilizzare l&#39;Editor universale, effettuare le seguenti operazioni:

1. [Configura i servizi nell’istanza di authoring di AEM.](#configure-aem)
1. [Configurare un servizio di editor universale locale.](#set-up-ue)
1. [Regolare il Dispatcher per consentire il servizio Universal Editor.](#update-dispatcher)

Dopo aver completato la configurazione, puoi [dotare le applicazioni per l’uso dell’editor universale.](#instrumentation)

### Configurare i servizi {#configure-aem}

L’editor universale si basa su una serie di servizi che devono essere configurati.

#### Imposta l’attributo SameSite per il cookie `login-token`. {#samesite-attribute}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua la voce **Adobe Granite Token Authentication Handler** nell’elenco e fai clic su **Modifica i valori di configurazione**
1. Nella finestra di dialogo, modifica l’**attributo SameSite per il cookie del token di accesso** (`token.samesite.cookie.attr`) in `Partitioned`.
1. Fai clic su **Salva**.

#### Rimuovi l’opzione X-Frame delle intestazioni `SAMEORIGIN`. {#sameorigin}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua il **servlet principale di Apache Sling** nell’elenco e fai clic su **Modifica i valori di configurazione**.
1. Elimina il valore `X-Frame-Options=SAMEORIGIN` dall’attributo **Altre intestazioni di risposta** (`sling.additional.response.headers`) se esistente.
1. Fai clic su **Salva**.

#### Configurare il gestore di autenticazione dei parametri di query di Adobe Granite {#query-parameter}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua il **Gestore di autenticazione dei parametri di query di Adobe Granite** nell’elenco e fai clic su **Modifica i valori di configurazione**.
1. Nel campo **Percorso** (`path`), aggiungi `/` per abilitare.
   * Un valore vuoto disattiva il gestore di autenticazione.
1. Fai clic su **Salva**.

#### Definire i percorsi di contenuto o `sling:resourceTypes` da aprire nell&#39;editor universale {#paths}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua **Servizio URL editor universale** nell’elenco e fai clic su **Modifica i valori di configurazione**.
1. Definisci i percorsi di contenuto o `sling:resourceTypes` per cui aprire l’editor universale.
   * Nel campo **Mappatura apertura editor universale**, specifica i percorsi per i quali è aperto l’editor universale.
   * Nel campo **Sling:resourceTypes che deve essere aperto da Universal Editor**, immettere un elenco di risorse che Universal Editor apre direttamente.
1. Fai clic su **Salva**.
1. Controlla la [configurazione di Externalizer](/help/sites-developing/externalizer.md) e assicurati almeno di avere gli ambienti locali, di authoring e di pubblicazione impostati come nell&#39;esempio seguente:

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una volta completati questi passaggi di configurazione, AEM apre l’Editor universale per le pagine nell’ordine seguente:

1. AEM controlla le mappature in `Universal Editor Opening Mapping` e se il contenuto si trova in uno dei percorsi qui definiti, viene aperto l&#39;Editor universale.

1. Per il contenuto non compreso nei percorsi definiti in `Universal Editor Opening Mapping`, AEM controlla se il contenuto `resourceType` corrisponde a una voce in **Sling:resourceTypes che verrà aperta da Universal Editor**. Se corrisponde, AEM apre il contenuto nell&#39;editor universale in `${author}${path}.html`.
1. In caso contrario, AEM apre l’Editor pagina.

Per definire le mappature sono disponibili le seguenti variabili in `Universal Editor Opening Mapping`.

* `path`: percorso del contenuto della risorsa da aprire
* `localhost`: voce esternalizzazione per `localhost` senza schema, ad esempio `localhost:4502`
* `author`: voce esternalizzazione per autore senza schema, ad esempio `localhost:4502`
* `publish`: voce esternalizzazione per pubblicazione senza schema, ad esempio `localhost:4503`
* `preview`: voce esternalizzatore per l&#39;anteprima senza schema, ad esempio `localhost:4504`
* `env`: `prod`, `stage`, `dev` in base alle modalità di esecuzione di Sling definite
* `token`: token di query richiesto per `QueryTokenAuthenticationHandler`

Esempi di mappature:

* Apri tutte le pagine in `/content/foo` in AEM Author:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Risultati nell&#39;apertura di `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Apri tutte le pagine in `/content/bar` su un server NextJS remoto, fornendo come informazioni tutte le variabili
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Risultati nell&#39;apertura di `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configurazione del servizio Editor universale {#set-up-ue}

Con AEM aggiornato e configurato, puoi impostare un servizio editor universale locale per le attività locali di sviluppo e testing.

1. Installa Node.js versione >=20.
1. Scarica e decomprimi il servizio Universal Editor più recente da [Software Distribution](https://experienceleague.adobe.com/it/docs/experience-cloud/software-distribution/home)
1. Configurare il servizio Universal Editor tramite variabili di ambiente o file `.env`.
   * [Per informazioni dettagliate, consulta la documentazione dell’editor universale di AEM as a Cloud Service.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Nota che potresti dover utilizzare l’opzione `UES_MAPPING` se è richiesta la riscrittura interna dell’IP.
1. Eseguire `universal-editor-service.cjs`

### Aggiornare Dispatcher {#update-dispatcher}

Con AEM configurato e un servizio Universal Editor locale in esecuzione, è necessario consentire un proxy inverso per il nuovo servizio [in Dispatcher.](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher)

1. Regola il file vhost dell’istanza di authoring in modo da includere un proxy inverso.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >La porta predefinita è 8080. Se hai modificato questo elemento usando il parametro `UES_PORT` nel [tuo file`.env`,](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) devi modificare di conseguenza il valore della porta qui.

1. Riavvia Apache.

## Strumentazione dell’app {#instrumentation}

Con AEM aggiornato e un servizio editor universale locale in esecuzione, puoi iniziare a modificare contenuti headless utilizzando l’editor universale.

Tuttavia, l’app deve essere dotata di strumenti che consentano di sfruttare i vantaggi dell’editor universale. Comporta l’inclusione di metatag per indicare all’editor come e dove mantenere il contenuto. I dettagli di questa dotazione di strumenti sono disponibili nella [documentazione dell’editor universale per AEM as a Cloud Service.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Quando si segue la documentazione di Universal Editor con AEM as a Cloud Service, vengono applicate le seguenti modifiche quando si utilizza con AEM 6.5 LTS.

* Il protocollo nel tag meta deve essere `aem65` invece di `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* L’endpoint del servizio editor universale deve essere annunciato tramite un tag meta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* Nella sezione `plugins` della definizione dei componenti, è necessario utilizzare `aem65` invece di `aem`.

>[!TIP]
>
>Per una guida completa per gli sviluppatori di Universal Editor, vedi [Panoramica di Universal Editor per sviluppatori AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) nella documentazione di AEM as a Cloud Service. Osserva le modifiche AEM 6.5 LTS descritte in questa sezione.

## Differenze tra AEM 6.5 LTS e AEM as a Cloud Service {#differences}

L’editor universale in AEM 6.5 LTS funziona in generale come in AEM as a Cloud Service, inclusa l’interfaccia utente e gran parte della configurazione. Ci sono, tuttavia, delle differenze che dovresti notare.

* Universal Editor in 6.5 LTS supporta solo il caso d’uso headless.
* La configurazione di Universal Editor varia leggermente per 6,5 LTS ([come descritto](#setup) nel documento corrente).
* L’editor universale in 6.5 LTS utilizza un selettore di risorse diverso e un selettore di frammenti di contenuto diverso da AEM as a Cloud Service.
