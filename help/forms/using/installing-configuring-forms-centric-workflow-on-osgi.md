---
title: Installazione e configurazione di un flusso di lavoro incentrato su Forms su OSGi
description: Installa e configura AEM Forms Interactive Communications per creare corrispondenza aziendale, documenti, rendiconti, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.
topic-tags: installing
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,AEM Forms on OSGi
exl-id: 4b316ade-4431-41fc-bb8a-7262a17fb456
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 2%

---

# Installazione e configurazione di un flusso di lavoro incentrato su Forms su OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introduzione {#introduction}

Le aziende raccolgono ed elaborano dati da più moduli, sistemi back-end e altre origini dati. Il trattamento dei dati comporta procedure di revisione e approvazione, attività ripetitive e archiviazione dati. Ad esempio, la revisione di un modulo e la sua conversione in documento PDF. Se eseguite manualmente, le attività ripetitive possono richiedere molto tempo e numerose risorse.

È possibile utilizzare [workflow incentrate sulla Forms su OSGi](../../forms/using/aem-forms-workflow.md) per versione rapidamente flussi di lavoro adattivi basati su moduli. Questi flussi di lavoro consentono di automatizzare i flussi di lavoro di revisione e approvazione, i flussi di lavoro processo di business e altre attività ripetitive. Questi flussi di lavoro consentono inoltre di elaborare i documenti (creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare accesso ai documenti, decodificare moduli con codice a barre e altro ancora) e utilizzare Adobe Sign workflow di firma con moduli e documenti.

Una volta impostati, questi flussi di lavoro possono essere attivati manualmente per completare un processo definito o eseguiti a livello di programmazione quando gli utenti inviano un modulo o una comunicazione interattiva. La funzionalità è inclusa in AEM Forms pacchetto aggiuntivo.

AEM Forms è una potente piattaforma di classe enterprise. Il flusso di lavoro incentrato su Forms per OSGi è solo una delle funzionalità di AEM Forms. Per l&#39;elenco completo delle funzionalità, vedere [Introduzione ad AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Con un flusso di lavoro incentrato su Forms su OSGi, puoi creare e distribuire rapidamente flussi di lavoro per varie attività sullo stack OSGi, senza dover installare la funzionalità completa di gestione dei processi sullo stack JEE. Consulta un [confronto](capabilities-osgi-jee-workflows.md) dei flussi di lavoro AEM incentrati su Forms su OSGi e Gestione processi su JEE per scoprire la differenza e le analogie nelle funzionalità.
>
>Dopo il confronto, se si sceglie di installare la funzionalità Gestione processi nello stack JEE, vedere [Installare o aggiornare AEM Forms in JEE](/help/forms/using/introduction-aem-forms.md) per informazioni dettagliate sull&#39;installazione e la configurazione dello stack JEE e delle funzionalità di Gestione processi.

## Topologia di distribuzione {#deployment-topology}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata in AEM. Per eseguire il flusso di lavoro incentrato su Forms sulla funzionalità OSGi, è sufficiente almeno un’istanza Autore o Elaborazione di AEM (authoring di produzione). Un&#39;istanza di elaborazione è un&#39;istanza [AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) avanzata. Non eseguire operazioni di authoring effettive, come la creazione di flussi di lavoro o moduli adattivi, sull’autore di produzione.

La topologia riportata di seguito è indicativa per l’esecuzione di comunicazioni interattive AEM Forms, gestione della corrispondenza, acquisizione dati AEM Forms e flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Per informazioni dettagliate sulla topologia, vedere [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

Il flusso di lavoro AEM Forms incentrato su Forms su OSGi esegue la Casella in entrata AEM e l’interfaccia utente per la creazione di modelli di flussi di lavoro AEM nelle istanze di authoring di AEM Forms.

## Requisiti di sistema {#system-requirements}

>[!NOTE]
>
>Passa alla sezione [Passaggi successivi](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) del documento, se hai già installato AEM Forms su OSGi come descritto nell&#39;articolo [installare e configurare le funzionalità di acquisizione dati](../../forms/using/installing-configuring-aem-forms-osgi.md).

Prima di iniziare a installare e configurare il flusso di lavoro incentrato su Forms su OSGi, assicurati di:

* Infrastruttura hardware e software già esistente. Per un elenco dettagliato di hardware e software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza di AEM non contiene spazi vuoti.
* Un’istanza di AEM è attiva e in esecuzione. Nella terminologia di AEM, per &quot;istanza&quot; si intende una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. Per eseguire un flusso di lavoro incentrato su Forms su OSGi è necessaria almeno un’istanza di AEM (authoring o elaborazione):

   * **Autore**: istanza di AEM utilizzata per creare, caricare e modificare contenuti e amministrare il sito Web. Quando il contenuto è pronto per essere pubblicato, viene replicato nell’istanza di pubblicazione.
   * **Elaborazione:** Un&#39;istanza di elaborazione è un&#39;istanza [AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) avanzata. Puoi impostare un’istanza Autore e irrigidirla dopo aver eseguito l’installazione.

   * **Pubblicazione**: istanza di AEM che fornisce il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto del componente aggiuntivo AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni Microsoft basate su Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Requisiti aggiuntivi per i sistemi basati su UNIX: se si utilizza il sistema operativo basato su UNIX, installare i pacchetti seguenti dal supporto di installazione del rispettivo sistema operativo.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuide</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Installare il pacchetto del componente aggiuntivo AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata in AEM. Il pacchetto contiene un flusso di lavoro incentrato su Forms su OSGi e altre funzionalità. Per installare il pacchetto aggiuntivo, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite la collegare diretta elencata nell&#39;articolo sulle [versioni](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Dopo aver installato il pacchetto, viene chiesto di riavviare il istanza AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di apparire nel [file AEM-Installation-Directory]/crx-quickstart/logs/error.log e il registro sia stabile.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare l&#39;SDK. Il riavvio dell&#39;SDK AEM utilizzando metodi alternativi, ad esempio l&#39;arresto dei processi Java, potrebbe lead a incoerenze nell&#39;ambiente di sviluppo AEM.

1. Ripeti i passaggi da 1 a 7 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

AEM Forms dispone di alcune configurazioni obbligatorie e opzionali. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell’agente di serializzazione. Le configurazioni opzionali includono la configurazione di Dispatcher e Adobe Target.

### Configurazioni post-installazione obbligatorie {#mandatory-post-installation-configurations}

#### Configurare RSA e BouncyCastle librerie  {#configure-rsa-and-bouncycastle-libraries}

Per avviare le librerie, esegui i seguenti passaggi su tutte le istanze Author e Publish:

1. Arresta l’istanza AEM sottostante.
1. Apri il file [directory di installazione di AEM]\crx-quickstart\conf\sling.properties per la modifica.

   Se per avviare AEM hai utilizzato la [directory di installazione di AEM]\crx-quickstart\bin\start.bat, modifica il file sling.properties che si trova in [AEM_root]\crx-quickstart\.

1. Aggiungi le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salva e chiudi il file e avvia l’istanza di AEM.
1. Ripeti i passaggi da 1 a 4 su tutte le istanze Author e Publish.

#### Configurare l’agente di serializzazione {#configure-the-serialization-agent}

Per aggiungere il pacchetto al inserisco nell&#39;elenco Consentiti di creazione, effettua le seguenti operazioni su tutte le istanze Author e Publish:

1. Apri AEM Configuration Manager in una finestra del browser. L&#39;URL predefinito è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Cerca e apri **Configurazione firewall deserializzazione**.
1. Aggiungere il pacchetto **sun.util.calendar** al campo **inserisce nell&#39;elenco Consentiti** di un&#39;unità di misura Fai clic su Salva.
1. Ripeti i passaggi 1-3 su tutte le istanze Author e Publish.

### Configurazioni opzionali post-installazione {#optional-post-installation-configurations}

#### Configurare Dispatcher {#configure-dispatcher}

Dispatcher è uno strumento di caching e bilanciamento del carico per AEM. AEM Dispatcher aiuta anche a proteggere il server AEM dagli attacchi. Puoi aumentare la sicurezza della tua istanza di AEM utilizzando Dispatcher insieme a un server web di classe enterprise. Se utilizzi [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), esegui le seguenti configurazioni per AEM Forms:

1. Configurare l’accesso per AEM Forms:

   Apri il file dispatcher.any per la modifica. Passa alla sezione del filtro e aggiungi il seguente filtro alla sezione del filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salvare e chiudere il file. Per informazioni dettagliate sui filtri, consulta la [documentazione di Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configura il servizio filtro referenti:

   Accedi al gestore della configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore della configurazione è https://&#39;server&#39;:[port_number]/system/console/configMgr. Nel menu **Configurations**, seleziona l&#39;opzione **Apache Sling Referrer Filter**. Nel campo Consenti host, immetti il nome host del dispatcher per consentirlo come referrer e fai clic su **Salva**. Il formato della voce è `https://'[server]:[port]'`.

#### Configura cache {#configure-cache}

La memorizzazione nella cache è un meccanismo che consente di ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di input/output (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per il rendering di un modulo adattivo.

* Quando si utilizza la cache dei moduli adattivi, utilizzare [AEM Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html) per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, mantieni disabilitata la cache dei moduli adattivi sul server utilizzato per lo sviluppo.

Per configurare la cache dei moduli adattivi, effettua le seguenti operazioni:

1. Passare a Gestione configurazione console Web AEM all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr`.
1. Fai clic su **[!UICONTROL Configurazione modulo adattivo e canale web di comunicazione interattiva]** per modificarne i valori di configurazione. Nella finestra di dialogo per la modifica dei valori di configurazione, specifica il numero massimo di moduli o documenti che un&#39;istanza del server AEM Forms può memorizzare nella cache nel campo **Numero di Forms adattivi**. Il valore predefinito è 100. Fai clic su **Salva**.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disattiva o si modifica la configurazione della cache.

#### Configurare Adobe Sign {#configure-adobe-sign}

Adobe Sign abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In un tipico scenario di flusso di lavoro basato su Adobe Sign e Forms su OSGi, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di domanda, viene avviato un flusso di lavoro di approvazione/rifiuto. Il fornitore di servizi esamina l’applicazione nella casella in entrata di AEM e utilizza Adobe Sign per firmare elettronicamente l’applicazione. Per abilitare flussi di lavoro di firma elettronica simili, puoi integrare Adobe Sign con AEM Forms.

Per utilizzare Adobe Sign con AEM Forms, [Integra Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per l’utilizzo di un flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Ora, i passaggi per utilizzare la funzionalità sono i seguenti:

* [Utilizzo del flusso di lavoro incentrato su Forms su OSGi](../../forms/using/aem-forms-workflow.md)
* [Guida di riferimento per i passaggi dei flussi di lavoro](/help/sites-developing/workflows-step-ref.md)
* [Post-elaborazione di lettere e comunicazioni interattive](../../forms/using/submit-letter-topostprocess.md)
