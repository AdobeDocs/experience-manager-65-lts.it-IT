---
title: Installare e configurare le funzionalità di acquisizione dati
description: Installare e configurare moduli adattivi, PDF forms e HTML5 Forms. Configura Adobe Analytics e Adobe Target per moduli adattivi per analizzare l’utilizzo dei moduli e indirizzare l’attività agli utenti in base al loro profilo.
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
exl-id: ee917b4b-fd38-4e05-8632-8efb82d9cddc
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 2%

---

# Installare e configurare le funzionalità di acquisizione dati{#install-and-configure-data-capture-capabilities}

## Introduzione {#introduction}

AEM Forms fornisce un set di moduli per ottenere dati dall’utente finale: moduli adattivi, HTML5 Forms e PDF forms. Fornisce inoltre strumenti per elencare tutti i moduli disponibili in una pagina web, analizzare l’utilizzo dei moduli e indirizzare gli utenti in base al loro profilo. Queste funzionalità sono incluse nel pacchetto del componente aggiuntivo AEM Forms. Il pacchetto del componente aggiuntivo viene distribuito su un’istanza Author o Publish di AEM.

**Moduli adattivi:** Questi moduli cambiano aspetto in base alle dimensioni dello schermo del dispositivo, sono coinvolgenti e di natura interattiva. Forms adattivo può anche essere integrato con Adobe Analytics, Adobe Sign e Adobe Target. Consente di fornire agli utenti moduli personalizzati ed esperienze orientate ai processi in base alla demografia e ad altre funzioni. Puoi anche integrare i moduli adattivi con Adobe Sign.

**PDF forms** è adatto per la stampa perfetta dei pixel e l&#39;acquisizione di informazioni digitali all&#39;interno di un documento PDF. Nell’avatar digitale, puoi utilizzare Adobe Acrobat o Acrobat Reader per compilare questi moduli. Puoi ospitare questi moduli sul tuo sito web o utilizzare il portale dei moduli per elencarli su un sito AEM. È inoltre possibile inviare questi moduli ad altri utenti tramite posta elettronica come allegati. Questi moduli sono particolarmente adatti per gli ambienti desktop.

**HTML5 Forms** è la versione di PDF forms compatibile con i browser. HTML5 Forms è adatto per ambienti che non supportano plug-in PDF. HTML5 Forms consente il rendering di moduli basati su XFA su dispositivi mobili e browser desktop su cui non è supportato il PDF basato su XFA. Questi moduli sono particolarmente adatti per tablet e ambienti desktop.

AEM Forms è una potente piattaforma di classe enterprise e l’acquisizione dei dati (moduli adattivi, PDF forms e HTML5 Forms) è solo una delle funzionalità di AEM Forms. Per l&#39;elenco completo delle funzionalità, vedere [Introduzione ad AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata in AEM. Per eseguire le funzionalità di acquisizione dati di AEM, è necessario disporre almeno di un’istanza Author e AEM Publish di AEM Forms. Per eseguire le funzionalità di acquisizione dati di AEM Forms AEM Forms, si consiglia di utilizzare la topologia riportata di seguito. Per informazioni dettagliate sulla topologia, vedere [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare la funzionalità di acquisizione dati di AEM Forms, assicurati che:

* Infrastruttura hardware e software già esistente. Per un elenco dettagliato di hardware e software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza di AEM non contiene spazi vuoti.
* Un’istanza di AEM è attiva e in esecuzione. Per gli utenti di Windows, installa l’istanza di AEM in modalità avanzata. Nella terminologia di AEM, per &quot;istanza&quot; si intende una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. Sono necessarie almeno due [istanze di AEM (una istanza Author e una Publish)](/help/sites-deploying/deploy.md) per eseguire le funzionalità di acquisizione dati di AEM Forms:

   * **Autore**: istanza di AEM utilizzata per creare, caricare e modificare contenuti e amministrare il sito Web. Quando il contenuto è pronto per essere pubblicato, viene replicato nell’istanza di pubblicazione.
   * **Pubblicazione**: istanza di AEM che fornisce il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto del componente aggiuntivo AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni Microsoft basate su Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Sono impostate la replica e la replica inversa per le istanze di authoring e pubblicazione. Per ulteriori dettagli, vedere [Replica](/help/sites-deploying/replication.md).
* Per i sistemi basati su UNIX:

   * Installare i seguenti pacchetti a 32 bit dal supporto di installazione:

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuide</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Se OpenSSL è già installato sul server, aggiornalo alla versione più recente.
>* Crea i symlink libcurl.so, libcrypto.so e libssl.so che puntano rispettivamente alla versione più recente delle librerie libcurl, libcrypto e libssl.
>

* Installare il seguente pacchetto a 64 bit dal supporto di installazione:

   * libicu

* Installa [Microsoft Visual Studio 2019 a 32 bit Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).


## Installare il pacchetto del componente aggiuntivo AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata in AEM. Il pacchetto contiene l’acquisizione dei dati di AEM Forms e altre funzionalità. Per installare il pacchetto aggiuntivo, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](/help/sites-administering/package-manager.md) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

   Puoi scaricare il pacchetto anche tramite il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).
1. Dopo l’installazione del pacchetto, viene richiesto di riavviare l’istanza di AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel file `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` e che il registro sia stabile.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Ripeti i passaggi da 1 a 7 su tutte le istanze Author e Publish.

### (Solo Windows) Installazione automatica dei ridistribuibili di Visual Studio {#automatic-installation-visual-studio-redistributables}

Se si installa un&#39;istanza di AEM in modalità avanzata, i componenti ridistribuibili di Visual Studio a 32 bit vengono installati automaticamente durante l&#39;installazione del pacchetto del componente aggiuntivo AEM Forms.

Per valutare se i redistribuibili di Visual Studio sono installati automaticamente, aprire il file `error.log` disponibile nella directory `/crx-repository/logs/`. I registri includono il seguente messaggio:

`Redist <service name> already installed on system, will not attempt re-installation`

Se i file ridistribuibili non vengono installati, i registri includono il seguente messaggio:

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Per risolvere il problema, riavviare il server AEM, installare AEM in modalità avanzata e quindi installare il pacchetto del componente aggiuntivo AEM Forms.

Se il controllo dei privilegi non riesce, i registri includono il seguente messaggio:

`Privilege escalation check failed with error: <error message>`

## Configurazioni post-installazione {#post-installation-configurations}

AEM Forms dispone di alcune configurazioni obbligatorie e opzionali. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell’agente di serializzazione. Le configurazioni facoltative includono la configurazione di Dispatcher, Forms Portal, Adobe Sign, Adobe Analytics e Adobe Target.

### Configurazioni post-installazione obbligatorie {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Per avviare le librerie, esegui i seguenti passaggi su tutte le istanze Author e Publish:

1. Arresta l’istanza AEM sottostante.
1. Apri il file `[AEM installation directory]\crx-quickstart\conf\sling.properties` per la modifica.

   Se hai utilizzato `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare AEM, modifica il file sling.properties che si trova in `[AEM_root]\crx-quickstart\`.

1. Aggiungi le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salva e chiudi il file e avvia l’istanza di AEM.
1. Ripeti i passaggi 1-4 su tutte le istanze Author e Publish.

#### Configurare l’agente di serializzazione {#configure-the-serialization-agent}

Per aggiungere il pacchetto al inserisco nell&#39;elenco Consentiti di creazione, effettua le seguenti operazioni su tutte le istanze Author e Publish:

1. Apri AEM Configuration Manager in una finestra del browser. URL predefinito: `https://'[server]:[port]'/system/console/configMgr`.
1. Cerca **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** e apri la configurazione.
1. Aggiungere il pacchetto **sun.util.calendar** al campo **inserisce nell&#39;elenco Consentiti** di un&#39;unità di misura Fai clic su **Salva**.
1. Ripeti i passaggi 1-3 su tutte le istanze Author e Publish.

### Configurazioni opzionali post-installazione {#optional-post-installation-configurations}

#### Configurare Dispatcher {#configure-dispatcher}

Dispatcher è uno strumento di caching e/o bilanciamento del carico di Adobe Experience Manager che può essere utilizzato insieme a un server web di classe enterprise. Se utilizzi [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), esegui le seguenti configurazioni per AEM Forms:

1. Configurare l’accesso per AEM Forms:

   Apri il file dispatcher.any per la modifica. Passa alla sezione del filtro e aggiungi il seguente filtro alla sezione del filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salvare e chiudere il file. Per informazioni dettagliate sui filtri, consulta la [documentazione di Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configura il servizio filtro referenti:

   Accedi al gestore della configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore della configurazione è `https://[server]:[port_number]/system/console/configMgr`. Nel menu **Configurations**, seleziona l&#39;opzione **Apache Sling Referrer Filter**. Nel campo Consenti host, immetti il nome host del dispatcher per consentirlo come referrer e fai clic su **Salva**. Il formato della voce è `https://[server]:[port]`.

#### Configura cache {#configure-cache}

La memorizzazione nella cache è un meccanismo che consente di ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di input/output (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per il rendering di un modulo adattivo.

* Quando si utilizza la cache dei moduli adattivi, utilizzare [AEM Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html) per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, mantieni disabilitata la cache dei moduli adattivi sul server utilizzato per lo sviluppo.

Per configurare la cache dei moduli adattivi, effettua le seguenti operazioni:

1. Vai a Gestione configurazione console Web AEM all&#39;indirizzo https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Fai clic su **Configurazione modulo adattivo e canale web di comunicazione interattiva** per modificarne i valori di configurazione. Nella finestra di dialogo per la modifica dei valori di configurazione, specifica il numero massimo di moduli o documenti che un&#39;istanza del server AEM Forms può memorizzare nella cache nel campo **Numero di Forms adattivi**. Il valore predefinito è 100. Fai clic su **Salva**.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disattiva o si modifica la configurazione della cache.

#### Configurare la comunicazione SSL per il modello dati modulo {#configure-ssl-communcation-for-form-data-model}

Puoi abilitare la comunicazione SSL per il modello dati modulo. Per abilitare la comunicazione SSL per il modello dati del modulo, prima di avviare qualsiasi istanza di AEM Forms, aggiungi i certificati all’archivio fonti attendibili Java di tutte le istanze. Puoi eseguire il comando seguente per aggiungere i certificati: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurare Adobe Sign {#configure-adobe-sign}

Adobe Sign abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In uno scenario tipico di Adobe Sign e moduli adattivi, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di richiesta, questo viene inviato al fornitore di servizi per ulteriori azioni. Il provider di servizi esamina l’applicazione e utilizza Adobe Sign per contrassegnarla come approvata. Per abilitare flussi di lavoro di firma elettronica simili, puoi integrare Adobe Sign con AEM Forms.

Per utilizzare Adobe Sign con AEM Forms, [Integra Adobe Sign con AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurare Adobe Analytics {#configure-adobe-analytics}

AEM Forms si integra con Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli e i documenti pubblicati. L’obiettivo dell’analisi di queste metriche è quello di prendere decisioni informate in base ai dati sulle modifiche necessarie per rendere i moduli o i documenti più utilizzabili.

Per utilizzare Adobe Analytics con AEM Forms, vedi [Configurazione di analisi e report](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrare Adobe Target {#integrate-adobe-target}

È probabile che i clienti abbandonino un modulo se l’esperienza che fornisce non è coinvolgente. Se da un lato è frustrante per i clienti, dall’altro può anche aumentare il volume e i costi del supporto per la tua organizzazione. Identificare e fornire la giusta esperienza del cliente che aumenti il tasso di conversione è fondamentale e impegnativo. AEM Forms è la chiave di questo problema.

AEM forms si integra con Adobe Target, una soluzione Adobe Marketing Cloud, per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Per utilizzare Adobe Target per testare i moduli adattivi A/B, [Integra Adobe Target con AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per l’utilizzo delle funzionalità di acquisizione dati di AEM Forms. Ora, i passaggi successivi per utilizzare la funzionalità sono:

* [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md)
* [Crea il tuo primo PDF Form](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introduzione a HTML5 Forms](/help/forms/using/introduction.md)
