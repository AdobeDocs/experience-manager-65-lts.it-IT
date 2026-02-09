---
title: Note sulla versione corrente di Adobe Experience Manager 6.5 LTS, SP1
description: Informazioni sulla versione corrente di Adobe Experience Manager 6.5 LTS, Service Pack 1.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 7c3f5d203be1ee2daa3274f76eade9af2ab9c821
workflow-type: tm+mt
source-wordcount: '7751'
ht-degree: 93%

---

# Note sulla versione corrente di Adobe Experience Manager 6.5 LTS, SP1 {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versione | Service Pack 1 (SP1), Hotfix per GRANITE-61551 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 9 settembre 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione del software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fcq-6.5.lts.1-hotfix-GRANITE-61551-1.2.zip) |

<!-- OLD URL TO JAR
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.1.jar) | -->


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## Funzionalità incluse in [!DNL Adobe Experience Manager] 6.5 LTS, SP1 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP1 include nuove funzionalità, miglioramenti importanti richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale di 6.5 LTS a marzo 2025. [Installare il Service Pack](#install-update) su 6.5 LTS.

## Nuove funzioni e miglioramenti

### Forms

È ora disponibile AEM 6.5 Forms LTS su JEE. Per informazioni dettagliate sugli ambienti supportati, vedere il documento Combinazioni [Piattaforma supportata](/help/forms/using/aem-forms-jee-supported-platforms.md). I collegamenti del programma di installazione sono disponibili nella pagina [Versioni di AEM Forms](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

#### Cosa è incluso in AEM Forms 6.5 LTS SP1

**Aggiornamenti del supporto Java**

È stato introdotto il supporto per le versioni Java più recenti:

* Java™ 17
* Java™ 21

**Aggiornamenti supporto server applicazioni**

* È stato aggiunto il supporto per JBoss EAP 8.
* Il framework di sicurezza PicketBox legacy è stato rimosso.
* Gli archivi di credenziali basati su Elytron sono ora supportati per la gestione sicura delle credenziali.

**Configurazione: archivio credenziali (basato su Elytron)**

AEM Forms su JBoss EAP 8 utilizza Elytron per la gestione delle credenziali sicure. I clienti devono configurare un archivio credenziali basato su Elytron per garantire l&#39;avvio corretto del server e l&#39;autenticazione sicura del database.

Per informazioni dettagliate sulla configurazione, consulta la guida all’installazione e alla configurazione.

**Modifiche alla piattaforma e alla compatibilità**

* Supporto per la specifica Servlet 5+
* Basato sulla conformità a Jakarta EE 9

**Requisito migrazione spazio dei nomi**

* Jakarta EE 9 introduce una modifica dello spazio dei nomi da `javax.*` a `jakarta.*`
* Tutti i **DSC personalizzati** devono essere migrati allo spazio dei nomi `jakarta.*`
* AEM Forms 6.5 LTS SP1 supporta **solo i server applicazioni basati su Jakarta EE 9+**

Per ulteriori informazioni, consulta **Migrazione da javax a jakarta Namespace**.

#### Migrazione da `javax` a `jakarta` spazio dei nomi

A partire da **AEM Forms 6.5 LTS SP1**, sono supportati solo i server applicazioni che implementano **Jakarta Servlet API 5/6**. Con **Jakarta EE 9 e versioni successive**, tutte le API sono passate dallo spazio dei nomi `javax.{}` a `jakarta.`.

Di conseguenza, **tutte le DSC personalizzate devono utilizzare lo spazio dei nomi `jakarta`**. I componenti personalizzati generati con le API `javax.{}` sono **non compatibili** con i server applicazioni supportati.

**Opzioni di migrazione per DSC personalizzati**

È possibile eseguire la migrazione di DSC personalizzate esistenti utilizzando uno dei seguenti approcci:

**Opzione 1: migrazione codice Source (consigliata)**

* Aggiorna tutte le istruzioni di importazione da `javax.{}` a `jakarta.`
* Ricompilare e ricompilare i progetti DSC personalizzati
* Ridistribuisci i componenti aggiornati nel server applicazioni

**Vantaggi:**

* Garantisce la compatibilità a lungo termine con Jakarta EE 9+
* Ideale per progetti con manutenzione attiva

**Opzione 2: Migrazione Binario Tramite Eclipse Transformer**

* Usa lo strumento **Trasformatore Eclipse** per convertire i file binari compilati (`.jar`, `.war`) da `javax` in `jakarta`
* Non è richiesta alcuna modifica o ricompilazione del codice sorgente
* Ridistribuisci i file binari trasformati nel server applicazioni

>[!NOTE]
>
> La trasformazione binaria viene eseguita al **livello di bytecode**.

Di seguito sono riportati alcuni esempi comuni di modifiche allo spazio dei nomi necessarie durante la migrazione:

* Prima (javax)    Dopo (jakarta)
* javax.servlet. **jakarta.servlet**
* javax.servlet.http. **jakarta.servlet.http.**

**Mappature di importazione di esempio**

La tabella seguente mostra le modifiche comuni allo spazio dei nomi richieste durante la migrazione da `javax` a `jakarta`:

| Prima di (`javax`) | Dopo (`jakarta`) |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

Utilizza queste mappature come riferimento per aggiornare il codice sorgente DSC personalizzato o convalidare i file binari trasformati.

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## Sono stati risolti i problemi in 6.5 LTS, Service Pack 1 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### Accessibilità {#sites-accessibility-65-lts-sp1}

* È stato risolto un problema a causa del quale l’elemento dell’editor di testo nei frammenti di contenuto veniva troncato per impostazione predefinita. Ora l’editor di testo visualizza il contenuto completo senza troncamento. (SITES-33005)
* È stato risolto un problema che causava l’apertura della home page di Indigo al posto dell’URL di destinazione corretto quando si faceva clic sui percorsi dell’URL. (SITES-33004)
* È stato risolto un problema di accessibilità in un componente AEM personalizzato che causava errori di conformità ADA durante il test automatizzato. (SITES-30660)
* Sono stati risolti i problemi di conformità ADA nella finestra di dialogo Avviso e Messaggi del flusso di lavoro garantendo la visualizzazione del testo in nero su sfondi chiari e la conformità ai requisiti di contrasto di WCAG 2.0. (SITES-30138)
* È stato risolto un problema di accessibilità a causa del quale il pulsante “Categoria” nell’editor di AEM Sites mancava di un’etichetta specifica; JAWS lo annunciava infatti come “Images button menu” (Menu del pulsante Immagini) invece di fornire un’etichetta descrittiva. (SITES-27497)
* È stato risolto un problema di accessibilità a causa del quale le icone dei segni di spunta nella schermata Autorizzazioni effettive non avevano un testo alternativo, pertanto JAWS non riusciva a leggere e trasmettere il loro significato. (SITES-27272)
* È stato risolto un problema di accessibilità a causa del quale la pagina Autorizzazioni non conteneva un chiaro annuncio di JAWS per la rimozione delle autorizzazioni di utenti o gruppi, generando confusione per gli utenti di assistenti vocali. (SITES-27238)
* È stato risolto un problema di accessibilità a causa del quale i messaggi di errore venivano visualizzati solo come icone senza testo descrittivo, impedendo a JAWS di annunciare gli errori quando si verificavano. (SITES-27155)
* È stato risolto un problema di accessibilità a causa del quale JAWS leggeva descrizioni dei pulsanti non corrette e non chiare nell’ambiente di AEM On-Premise, incluso il testo del livello di intestazione 2 mancante per la sezione dei moduli. (SITES-27152)
* È stato risolto un problema di accessibilità a causa del quale JAWS non annunciava il numero di risultati dopo l’applicazione dei filtri ai valori nella scheda AEM Assets. (SITES-27150)
* È stato risolto un problema di accessibilità a causa del quale la creazione di una cartella non mostrava una conferma e JAWS non la annunciava nell’interfaccia utente di Assets. (SITES-27141)
* È stato risolto un problema di accessibilità in AEM Sites. JAWS non ha annunciato errori del modulo, lo stato attivo è stato spostato su elementi di errore non interattivi e gli errori dei campi obbligatori non sono stati visualizzati con l’uso del tasto di tabulazione. (SITES-27138)
* È stato risolto un problema di accessibilità a causa del quale il menu del pulsante Timeline non disponeva di un’etichetta specifica; JAWS si limitava pertanto a leggere “Menu del pulsante Attività” senza fornire una descrizione chiara. (SITES-27134)
* È stato risolto un problema di accessibilità a causa del quale JAWS non annunciava l’azione o il ruolo per gli elementi container, limitandosi a leggere “Breadcrumb v1” e “button v2” invece delle etichette descrittive. (SITES-27131)
* È stato risolto un problema di accessibilità a causa del quale il pop-up di pubblicazione rapida non forniva un messaggio di operazione completata adeguato, impedendo agli assistenti vocali di annunciare il feedback sul completamento. (SITES-26912)
* È stato risolto un problema di accessibilità nella vista a colonne di corallo a causa del quale gli elementi con ruoli ARIA che richiedevano ruoli secondari non ne contenevano, causando la mancata conformità agli standard di accessibilità. (SITES-26898)
* È stato risolto un problema di accessibilità a causa del quale i testi “modello” e “proprietà” nella navigazione presente in alto sulla pagina di creazione non erano visibili in modalità Riflusso, impedendo l’accesso agli utenti che utilizzano tastiera e assistente vocale. (SITES-26895)
* È stato risolto un problema di accessibilità a causa del quale le descrizioni comandi per le icone “ricerca”, “soluzione”, “guida”, “casella in entrata” e “utente” nella navigazione presente in alto non erano accessibili tramite la navigazione con tastiera. (SITES-26889)
* È stato risolto un problema di accessibilità a causa del quale i campi modulo della scheda Base non fornivano suggerimenti di errore, impedendo agli utenti di ricevere indicazioni quando i campi di input obbligatori erano lasciati vuoti. (SITES-26885)
* È stato risolto un problema di accessibilità a causa del quale gli assistenti vocali NVDA e Assistente vocale non annunciavano i dettagli dei file modello nella pagina Crea, impedendo agli utenti di ricevere informazioni complete a livello di programmazione. (SITES-26884)
* È stato risolto un problema di accessibilità a causa del quale veniva utilizzato un nome errato per “Casella di testo Titolo pagina” nella scheda Base, impedendo agli assistenti vocali di fornire informazioni accurate agli utenti. (SITES-26879)
* Sono stati aggiornati i colori di primo piano e di sfondo dei pulsanti per soddisfare i requisiti del rapporto di contrasto minimo di WCAG 2.2 AA, migliorando la leggibilità e l’accessibilità per tutti gli utenti. (SITES-26877)
* È stato risolto un problema che causava la scomparsa dei testi “modello” e “proprietà” nella navigazione presente in alto sulla pagina di creazione dopo il ridimensionamento, garantendo visibilità e accessibilità agli utenti ipovedenti. (SITES-26872)
* È stato risolto un problema che causava la visualizzazione di più barre di scorrimento orizzontali sulla pagina principale dopo l’applicazione di un Riflusso, affinché una singola barra di scorrimento venga visualizzata per la corretta accessibilità e visibilità del contenuto. (SITES-26800)
* È stato risolto un problema di accessibilità nell’editor di pagine di AEM a causa del quale lo stato attivo sulla tastiera veniva ripristinato all’inizio della barra degli strumenti Demografica dopo l’attivazione dei pulsanti come Persona, Carrello o Abbandonato. Ora lo stato attivo resta sul pulsante attivato per supportare flussi di lavoro coerenti per la navigazione da tastiera e l’assistente vocale. (SITES-25306)
* È stato risolto il problema relativo all’associazione delle etichette di accessibilità per i campi titolo pagina e tag. L’interfaccia di AEM ora associa correttamente le etichette di accessibilità ai campi “Titolo” e “Titolo pagina” durante l’utilizzo di assistenti vocali come JAWS. La correzione assicura la corretta lettura delle etichette e migliora la conformità ADA nei flussi di lavoro di creazione, proprietà e spostamento delle pagine. (SITES-27149)
* È stata corretta l&#39;etichetta visiva mancante per i campi di input dei commenti nella timeline. Sono state corrette le etichette visive mancanti per i campi di input &quot;commento&quot; nella sezione della timeline per migliorarne l’accessibilità. L’aggiornamento garantisce che gli assistenti vocali possano annunciare con precisione le etichette dei campi. Questa esperienza migliora la navigazione e l&#39;invio dei moduli per tutti gli utenti, in particolare gli utenti che contano sulle tecnologie per l&#39;accessibilità. (SITES-26903)
* È stata corretta l&#39;accessibilità da tastiera per il pulsante con puntini di sospensione nei commenti della timeline. È stata abilitata la navigazione tramite tastiera per il pulsante con puntini di sospensione (tre punti) accanto ai commenti nella sezione della timeline. Gli utenti possono ora accedere al pulsante e interagire con esso utilizzando il tasto tab, migliorando l&#39;accessibilità per gli utenti che si affidano alla navigazione tramite sola tastiera. (SITES-26891)
* Sono stati migliorati gli annunci NVDA/Assistente vocale per i risultati di ricerca nelle finestre di dialogo di selezione. È stata aggiornata la finestra di dialogo Apri selezione per indicare se i risultati della ricerca vengono trovati o meno quando si utilizzano gli assistenti vocali, come NVDA o Assistente vocale. Questo miglioramento consente agli utenti che si affidano alle tecnologie per l&#39;accessibilità di comprendere il risultato delle azioni di ricerca senza bisogno di conferma visiva. (SITES-26883)
* È stato corretto il ruolo ARIA per l&#39;icona con i puntini di sospensione accanto al campo di input del commento. È stata aggiornata l&#39;icona con i puntini di sospensione (tre punti) accanto al campo di input del commento per utilizzare il ruolo ARIA corretto, in modo che gli assistenti vocali possano identificare con precisione l&#39;elemento. Questo miglioramento migliora la conformità in materia di accessibilità e l&#39;esperienza degli utenti che si affidano alle tecnologie per l&#39;accessibilità. (SITES-26881)
* Sono stati corretti gli attributi ARIA non validi nei componenti dell’interfaccia utente Coral. Sono stati aggiornati i componenti dell’interfaccia utente Coral per garantire che tutti gli attributi ARIA utilizzino valori validi, migliorando l’accessibilità e la conformità. In particolare, sono stati risolti casi in cui valori non validi come `aria-modal="dialog"` non venivano assegnati correttamente. Questo miglioramento consente agli assistenti vocali di interpretare correttamente gli elementi delle finestre di dialogo, migliorando l’accessibilità per gli utenti che si affidano a queste tecnologie. (SITES-26873)
* Sono state migliorate la visibilità e le descrizioni delle icone negli scenari di ridisposizione. È stato migliorato il comportamento Ridisponi per garantire la corretta visualizzazione delle descrizioni per le icone **Scarica**, **Rielabora risorse** e **Estrai**. È stato individuato un problema di accessibilità in cui le icone e le relative etichette diventavano invisibili quando il riquadro di visualizzazione veniva ridimensionato o le impostazioni di zoom del browser cambiavano. Questa correzione consente di mantenere la visibilità degli utenti ipovedenti e fornisce descrizioni delle icone durante la ridisposizione. (SITES-26871)


#### Interfaccia utente amministratore{#sites-adminui-65-lts-sp1}

* È stato risolto un problema di accessibilità a causa del quale JAWS non annunciava i ruoli elenco né forniva istruzioni di navigazione e attivazione nella finestra di dialogo Crea sito. (SITES-30661)
* Il supporto degli assistenti vocali sui messaggi di stato nella vista filtro Sites funziona come previsto, garantendo agli utenti un feedback chiaro e tempestivo quando passano da una visualizzazione all’altra. (SITES-24992)
* Il selettore data nella barra dei filtri viene visualizzato completamente all’interno del relativo contenitore, fornendo dimensioni delle destinazioni touch adeguate ed eliminando i problemi di ritaglio. (SITES-24988)
* I tag di filtro selezionati ora utilizzano etichette semantiche HTML e ARIA corrispondenti alla presentazione visiva, garantendo un supporto preciso dei ruoli e azioni chiare per le tecnologie per l’accessibilità. (SITES-24980)
* È stato aggiunto un attributo aria-label all’area della barra Riferimenti per fornire un’etichetta univoca e descrittiva per gli utenti degli assistenti vocali e garantire un’identificazione coerente dei punti di riferimento all’interno della pagina. (SITES-24973)
* La barra Riferimenti è stata aggiornata per utilizzare le unità relative a dimensionamento e posizionamento, consentendo la scalabilità e la piena funzionalità del contenuto quando viene ingrandito al 400% in un riquadro di visualizzazione 1280x1024. (SITES-24972)
* Gli elementi di tabella confermati nella visualizzazione elenco della pagina Home di Sites contengono ruoli di intestazione di colonna corretti, che consentono agli assistenti vocali di annunciare le intestazioni per ogni cella di dati. (SITES-24942)
* NVDA ha appena annunciato di aver inserito la Data di modifica nella directory ad albero, garantendo che gli utenti che usano utilità di lettura dello schermo ricevano informazioni complete sui dettagli delle risorse. (SITES-24782)
* È stato risolto un problema a causa del quale l’assistente vocale NVDA annunciava un testo incompleto per gli elementi del componente Directory ad albero in AEM Sites. NVDA legge ora il testo completo per ogni elemento, migliorando l’accessibilità e la conformità. (SITES-24780)
* È stata aggiunta l’accessibilità della tastiera alla finestra divisa nella directory ad albero, consentendo agli utenti di ridimensionare la barra laterale a sinistra utilizzando solo una tastiera. (SITES-24779)
* Sono stati aggiornati i risultati della ricerca nel menu Aiuto per includere i ruoli ARIA corretti per le voci di elenco, in modo che gli assistenti vocali annuncino correttamente i collegamenti per migliorare l’accessibilità. (SITES-24729)
* È stato risolto un problema a causa del quale gli assistenti vocali non annunciavano il messaggio di stato “Risultati X di Y”. Oppure il messaggio “nessun risultato trovato” dopo l’applicazione di filtri nel pannello Filtro siti, per garantire che gli utenti ricevano la conferma corretta dei risultati. (SITES-24720)
* Sono state corrette le assegnazioni di ruolo mancanti per i collegamenti di navigazione nell’app. Sono stati aggiunti i ruoli ARIA appropriati per garantire che gli assistenti vocali identifichino e annuncino correttamente gli elementi di navigazione. (SITES-24719)
* Il markup del ruolo griglia non corretto per i tag filtro selezionati è stato sostituito con gli elementi dei pulsanti e sono stati aggiunti nomi accessibili, in modo che gli assistenti vocali possano annunciare e identificare correttamente i tag. (SITES-24717)
* Sono stati aggiunti annunci di utilità di lettura dello schermo per il messaggio di stato della barra Riferimenti quando si eseguono selezioni multiple, in modo che gli utenti ricevano conferma delle modifiche. (SITES-24678)
* È stato corretto il comportamento del campo di ricerca in modo che non venga annunciato automaticamente il primo risultato. Gli assistenti vocali ora annunciano il numero di risultati trovati, consentendo agli utenti di navigare nell’elenco senza focalizzarsi su annunci errati. (SITES-24658)
* Gli attributi `aria-label` non corretti sono stati rimossi dagli elementi statici non interattivi nella visualizzazione elenco per impedire agli assistenti vocali di annunciare informazioni fuorvianti o irrilevanti. (SITES-24515)
* La casella di controllo nella prima colonna della Vista a elenco è stata aggiornata per utilizzare il testo della colonna Titolo come nome accessibile, in modo che gli assistenti vocali possano comunicare con precisione lo scopo del campo modulo. (SITES-24514)
* Sono stati aggiunti gli attributi ARIA appropriati e il supporto per le aree geografiche attive per annunciare il caricamento dei messaggi di stato agli assistenti vocali durante la navigazione all’interno del contenuto. (SITES-24481)
* È stata aggiornata la progettazione dinamica per eliminare lo scorrimento orizzontale quando il contenuto viene ingrandito al 400% con una larghezza di visualizzazione di 1280x1024, garantendo una visibilità completa senza scorrimento laterale. (SITES-24308)
* È stata corretta la navigazione dello stato attivo nell’interfaccia utente amministratore di Sites in modo da seguire un ordine logico, riportando lo stato attivo sul pulsante “Seleziona tutto” dopo aver premuto il tasto ESC e spostato lo stato attivo sull’elemento interattivo successivo dopo aver premuto il tasto Tab. (SITES-24307)
* È stato aggiornato l’ordine dello stato attivo nell’interfaccia utente amministratore di Sites in modo che il pulsante delle breadcrumb nell’elemento `<betty-titlebar-title>` riceva lo stato attivo nella sequenza corretta durante la navigazione da tastiera. (SITES-24305)
* È stata verificata la funzionalità che consente di ignorare il collegamento per garantire che sposti il focus della tastiera nell’area del contenuto principale, consentendo agli utenti che utilizzano la tastiera di ignorare gli elementi dell’intestazione e di accedere ai contenuti in modo efficiente. (SITES-24061)


#### Interfaccia utente classica{#sites-classicui-65-lts-sp1}

È stato risolto un problema dell’interfaccia classica a causa del quale le etichette delle caselle di controllo non erano presenti e HTML veniva visualizzato come testo codificato in più elementi dell’interfaccia utente, inclusi Ricerca per data e interfacce non standard. (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM ora evita il deterioramento delle prestazioni causato da metadati XMP non validi nelle risorse immagine. Le risorse che contengono nomi di proprietà XMP non validi o non conformi, ad esempio quelli con segmenti numerici o strutture non qualificate, non attivano più i registri di avviso ripetuti durante l’elaborazione. Il sistema filtra i metadati problematici per garantire che l’acquisizione e la convalida delle risorse siano completate senza errori. (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-65-lts-sp1}

Altri autori possono comunque pubblicare frammenti di contenuto anche quando un altro autore li estrae, il che è contrario al comportamento previsto della funzione di estrazione. Questa correzione impedisce ad altri utenti di visualizzare o utilizzare i pulsanti di pubblicazione nell’interfaccia di authoring quando viene estratto un frammento di contenuto. (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### Console dei componenti{#sites-component-console-65-lts-sp1}

È stato risolto un problema nel componente Elenco prodotti a causa del quale la casella di controllo &quot;Seleziona tutti&quot; aggiungeva solo le prime 20 SKU dalla pagina iniziale invece di tutte le SKU nei risultati della ricerca. (SITES-29191)

#### Back-end core{#sites-core-backend-65-lts-sp1}

I metadati XMP formattati in modo non corretto hanno generato un errore durante l&#39;elaborazione delle risorse immagine in `ValidationDataServlet`. La correzione assicura la gestione conforme dei metadati ed evita l’analisi ridondante di proprietà non valide. (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp1}

* È stato corretto un errore JavaScript `ns.ui.alert is not a function` che si verificava durante la riattivazione dell&#39;ereditarietà del componente fantasma in AEM 6.5 On-Prem. (SITES-31993)
* È stato risolto un problema a causa del quale l’opzione di rollout &quot;Più tardi&quot; consentiva di continuare senza selezionare una data in AEM 6.5. (SITES-31374)

#### Editor pagina{#sites-pageeditor-65-lts-sp1}

* È stato risolto un problema nel modale Teaser a causa del quale la scheda Collegamento e azioni continuava a visualizzare lo stile degli errori, le icone e l’attributo ARIA non valido dopo l’immissione di dati validi e la risoluzione degli errori. (SITES-25527)
* È stato risolto un problema nell’editor di testo del modale Teaser a causa del quale i pulsanti Elenchi e Paragrafi non trasmettevano il loro stato espanso o compresso agli assistenti vocali che garantiva aggiornamenti accurati degli attributi ARIA espansi. (SITES-25365)
* È stato risolto un problema nella barra degli strumenti dei dati demografici a causa del quale la regolazione del cursore del carrello con l’input della tastiera spostava il focus sul pulsante Carrello invece di mantenere il focus sul cursore, migliorando l’efficienza della navigazione per gli utenti che utilizzano la tastiera. (SITES-25324)
* È stato aggiunto un nome accessibile al cursore del carrello nella barra degli strumenti dei dati demografici assegnando un valore all&#39;elemento `<label>` associato. Questa correzione ha migliorato la compatibilità con le tecnologie per l’accessibilità e l’usabilità per gli assistenti vocali. (SITES-25322)
* Sono stati aggiunti i ruoli ARIA e i nomi accessibili ai pulsanti nel menu a discesa della barra degli strumenti dei dati demografici. Questa correzione ha consentito una corretta identificazione tramite tecnologie per l’accessibilità e una migliore navigazione per gli utenti che utilizzano la tastiera e gli assistenti vocali. (SITES-25315)
* È stato corretto il layout della barra degli strumenti dei dati demografici per impedire l’overflow del contenuto oltre la visualizzazione con uno zoom del browser del 200%, garantendo che tutti i controlli rimangano accessibili senza scorrimento orizzontale. (SITES-25309)
* È stata corretta la gestione del focus nella barra degli strumenti dei dati demografici per mantenere il focus della tastiera sul pulsante attivato invece di reimpostarlo sulla posizione iniziale della barra degli strumenti. (SITES-25306)
* L’etichetta del pulsante si sovrappone come previsto, utilizzando una descrizione per visualizzarla quando sono attive modalità con larghezze di schermo simili. (SITES-25285)
* L’annotazione modale include un pulsante di invio visibile che consente agli utenti di inviare le annotazioni senza utilizzare il tasto ESC o senza fare clic all’esterno del modale. (SITES-25281)
* L’annotazione modale include un pulsante con icona a forma di penna che consente agli utenti di inviare annotazioni, fornendo un metodo di invio chiaro e accessibile. (SITES-25269)
* Sono stati corretti gli annunci degli assistenti vocali relativi ai pulsanti Annota e Chiudi annotazione per fornire un feedback accurato e pertinente e rimuovere informazioni non correlate o che generano confusione. (SITES-25268)
* Le sezioni dell’area di lavoro nelle pagine dell&#39;Editor AEM ora supportano l’accessibilità completa da tastiera. Gli utenti possono attivare i titoli delle sezioni e i pulsanti di modifica utilizzando solo la tastiera, senza dover passare con il mouse. Questo aggiornamento garantisce la conformità a WCAG 2.1.1 e migliora l’usabilità tra i componenti (come modali Teaser, Immagine, Carosello, Layout, Timewarp e Annotazione). (SITES-25256)
* È stato rimosso l’inutile scorrimento orizzontale nel modale Carosello a una larghezza di 320 px per garantire che tutto il contenuto venga visualizzato nel riquadro di visualizzazione senza richiedere la navigazione laterale. (SITES-25254)
* È stato rimosso l’inutile scorrimento orizzontale nel modale Immagine a una larghezza di 320 px per garantire che tutto il contenuto venga visualizzato nel riquadro di visualizzazione senza richiedere la navigazione laterale. (SITES-25244)
* È stato rimosso l’inutile scorrimento orizzontale nel modale Teaser a una larghezza di 320 px per garantire che tutto il contenuto venga visualizzato nel riquadro di visualizzazione senza richiedere la navigazione laterale. (SITES-25242)
* Attivazione della navigazione tramite tastiera per il `List` e `Paragraph Format` il menu pop-up, entrambi nel modale Teaser. Questa correzione consente agli utenti di accedere e navigare in questi menu utilizzando i tasti freccia. (SITES-25235)
* Sono stati corretti gli annunci degli assistenti vocali relativi ai pulsanti Annota e Chiudi annotazione per fornire un feedback preciso e pertinente in linea con le azioni associate. (SITES-25234)
* È stata migliorata l’etichetta del pulsante Aiuto nel modale Teaser per descriverne chiaramente lo scopo e fornire un contesto significativo per tutti gli utenti, compresi gli utenti di tecnologie per l&#39;accessibilità. (SITES-25224)
* È stato migliorato il righello dell’emulatore per gli utenti di utilità di lettura dello schermo associando le misurazioni del righello ai rispettivi dispositivi. Inoltre, sostituendo la descrizione con un elemento descritto da aria. (SITES-24955)
* Non è stata implementata alcuna correzione perché il pulsante Modifica funziona come previsto e fornisce contesto informativo anziché eseguire un&#39;azione. (SITES-24950)
* L’ordine del focus confermato nella pagina dell’editor segue una sequenza logica che consente agli utenti di navigare tra tutti gli elementi interattivi senza saltare o tornare indietro in modo imprevisto. (SITES-24937)
* L’area di lavoro in modalità Anteprima confermata aggiorna correttamente la spaziatura del testo quando gli utenti applicano impostazioni di spaziatura di testo personalizzato, garantendo una formattazione coerente in tutte le aree di contenuto. (SITES-24936)
* Il pulsante Anteprima verificato non attiva più le modifiche di contesto o stato nel focus, garantendo agli utenti l’attivazione intenzionale prima che la vista della pagina venga aggiornata. (SITES-24784)
* Ai collegamenti di navigazione dell’app sono state aggiunte le assegnazioni corrette del ruolo ARIA, che consentono agli assistenti vocali di identificare con precisione gli elementi desiderati e di annunciarne gli elementi per migliorarne l&#39;accessibilità. (SITES-24718)
* Il pulsante Modifica filtri è stato aggiornato per annunciare gli stati espansi e compressi agli assistenti vocali, rimuovere gli attributi ARIA ridondanti e regolare l’etichettatura per fornire descrizioni chiare e non duplicate. (SITES-24713)
* Nella finestra di dialogo per la selezione dei collegamenti sono stati aggiunti annunci di assistenti vocali per i messaggi di stato dei risultati di ricerca, in modo che gli utenti ricevano una conferma al caricamento dei risultati o quando non vengono trovate corrispondenze. (SITES-24700)
* Sono stati aggiunti annunci di assistenti vocali per lo stato di caricamento del modale Immagine, in modo che gli utenti ricevano un feedback durante il caricamento del modale e siano pronti per l’interazione. (SITES-24697)
* È stato risolto un problema di accessibilità a causa del quale l’intestazione permanente oscurava il contenuto modale di Teaser con uno zoom del 200% e del 400%, garantendo piena visibilità e usabilità quando si utilizzava l’ingrandimento della pagina. (SITES-24523)
* È stato aggiunto al campo Ricerca/filtro un messaggio di stato con il numero di risultati di ricerca, per consentire agli assistenti vocali di annunciare i risultati agli utenti. (SITES-24506)
* Sono stati aggiunti annunci di assistenti vocali per il numero di risultati di ricerca nel campo Ricerca/Filtro, in modo che gli utenti ricevano un feedback immediato al caricamento dei risultati. (SITES-24505)
* È stato aggiunto un nome accessibile all&#39;elenco di schede nel pannello della barra laterale, consentendo agli assistenti vocali di annunciarne lo scopo in conformità alle linee guida WAI-ARIA. (SITES-24492)
* Sono state aggiunte etichette descrittive alle icone dell&#39;editor ambigue, in modo che tutti gli utenti comprendano chiaramente la funzione di ciascun pulsante. (SITES-24480)
* È stata abilitata l&#39;accessibilità completa da tastiera per i titoli delle sezioni e i pulsanti di azione nella vista Area di lavoro, garantendo un funzionamento coerente per gli utenti di mouse e tastiera. (SITES-24479)

<!--
#### Replication{#sites-replication-65-lts-sp1}

#### Rich Text Editor{#sites-rte-65-lts-sp1} -->

#### Editor universale {#sites-universal-editor-65-lts-sp1}

* È stata risolta una situazione di tipo &quot;race condition&quot; in QueryTokenService che causava accessi non validi quando più richieste con parametri di query venivano attivate prima che il servizio token di accesso restituisse un risultato. (SITES-30659)
* È stato risolto un problema in UniversalEditorURLService a causa del quale il salvataggio di un array di percorsi mappati in Felix ConfigMgr manteneva solo il primo elemento. (SITES-30292)

### [!DNL Assets]{#assets-65-lts-sp1}

È stato risolto un problema a causa del quale la sincronizzazione delle risorse da DAM remoto a AEM locale di Sites rimuoveva dalle risorse lo stato pubblicato e le proprietà relative alla replica. (Assets-48958)

<!--
#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp1}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp1}

### [!DNL Forms]{#forms-65-lts-sp1}

#### Forms Designer 

#### Forms

#### Forms JEE 
 
#### Forms Captcha {#forms-captcha-65-lts-sp1} 

#### XMLFM {#forms-xmlfm-65-lts-sp1}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp1}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp1} -->

### Foundation {#foundation-65-lts-sp1}

<!--
#### Apache Felix {#foundation-apachefelix-65-lts-sp1}

#### Campaign{#foundation-campaign-65-lts-sp1}

#### Cloud Services{#foundation-cloudservices-65-lts-sp1}



#### Communities {#foundation-communities-65-lts-sp1}

#### Content distribution{#foundation-content-distribution-65-lts-sp1}

#### CRX {#foundation-crx-65-lts-sp1}

#### Granite{#foundation-granite-65-lts-sp1} -->

#### HTL{#foundatoin-htl-5-lts-sp1}

Sono stati risolti i cicli di dipendenza OSGi che impedivano il funzionamento della factory del motore di script HTL, garantendo una risoluzione del servizio e l&#39;esecuzione dello script corrette. (Granite-58275)

#### Integrazioni{#foundation-integrations-65-lts-sp1}

* È stato rimosso l&#39;utilizzo di commons-httpclient 3.x dal bundle `com.adobe.cq.cq-analytics-integration` e sostituito con `org.apache.httpcomponents.httpclient` 4.5.13.B0001 per allinearlo ai più recenti standard AEM 6.5 LTS. (CQ-4360586)
* È stato rimosso il bundle di integrazione Search&amp;Promote obsoleto da AEM per eliminare i componenti inutilizzati e ridurre il sovraccarico di manutenzione. (CQ-4358030)
* Sono stati aggiunti nuovi casi di test back-end per l&#39;integrazione SiteCatalyst per migliorare la convalida delle analisi e garantire una copertura più completa. (CQ-4359991)
* È stato risolto un problema nella sezione Proprietà della configurazione di lancio a causa del quale i menu a discesa Azienda e Proprietà non venivano visualizzati. Inoltre, Salva e chiudi hanno attivato errori nonostante tutti i campi obbligatori fossero compilati e messaggi di errore non corretti venivano visualizzati per Azienda e Proprietà quando solo il campo Titolo era vuoto. (CQ-4359853)
* È stata rimossa la voce del percorso del servlet `searchpromote` dalla versione 6.6 per allinearla alla rimozione del bundle Search&amp;Promote. (CQ-4359523)
* Sono stati corretti alcuni casi di test HTTP per l&#39;archivio di destinazione, al fine di garantire una convalida accurata e una maggiore affidabilità dei test. (CQ-4359022)
* È stato rimosso l&#39;utilizzo del caching Guava dal modulo integration-adobeims-console per eliminare le dipendenze della libreria Guava. (CQ-4358710)
* Convalidati i flussi di lavoro di integrazione di DTM, attività casella in entrata e funzionalità di progetto in AEM 6.6 per garantire il corretto funzionamento in AEM 6.5. (CQ-4358151)
* Funzionalità Approfondimenti contenuto convalidata in AEM 6.6 per garantire la compatibilità e il corretto funzionamento in AEM 6.5. (CQ-4357774)
* Funzionalità Cloud Service convalidata in AEM 6.6 per garantire la compatibilità e il corretto funzionamento in AEM 6.5. (CQ-4357773)
* Integrazione convalidata della console Adobe IMS in AEM 6.6 per garantire la compatibilità e il corretto funzionamento in AEM 6.5. (CQ-4357772)
* È stata aggiornata la pipeline Jenkins per l&#39;integrazione Test&amp;Target da eseguire su Java 17, risolvere gli errori dei test Selenium, spostare alcuni test su Playwright e garantire il superamento di tutti test unitari. (CQ-4357770)
* Sono state allineate le integrazioni DX, il flusso di lavoro, la casella in entrata e i progetti con il ramo 6.6.0 aggiornando le pipeline di generazione e test. Risoluzione dei problemi di compatibilità dell&#39;aggiornamento e convalida di tutti i servizi interessati per la stabilità e la funzionalità. (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### Localizzazione{#foundation-localization-65-lts-sp1}

* Le stringhe nella finestra di dialogo &quot;Rimuovi controllo di accesso&quot; dall&#39;elenco &quot;Autorizzazioni&quot; sono state localizzate per visualizzare le traduzioni corrette. (GRANITE-59427)
* È stato risolto un problema nella finestra di dialogo Aggiungi regola di &quot;Proprietà suddivisione O&quot; dell&#39;editor dei modelli a causa del quale più stringhe di interfaccia utente, inclusi operatori ed etichette di campo, venivano visualizzate non localizzate. Tutte le stringhe vengono ora visualizzate con la localizzazione corretta. (CQ-4354014)
* È stata aggiunta la traduzione mancante per la descrizione comando &quot;Breve descrizione per&quot; nella finestra di dialogo Modifica modelli flusso di lavoro. (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

È stato risolto un problema a causa del quale AEM ricreava o rinominava i file di configurazione esistenti in `/apps/system/config` durante gli aggiornamenti, sostituendo `.cfg.json` file con `.config` file. (GRANITE-58899)

#### Omnisearch{#foundation-omnisearch-65-lts-sp1}

È stato risolto un problema di accessibilità a causa del quale i segnaposto venivano erroneamente visualizzati come etichette per i campi di input. Questo problema causa la mancanza di etichette dei campi in Ricerca, Frammenti di esperienza AEM, Frammenti di contenuto e Modelli di frammenti di contenuto. (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### Progetti{#foundation-projects-65-lts-sp1}

* È stato risolto un problema che causava la visualizzazione di un pop-up di errore non corretto durante l’eliminazione di un progetto nella vista Calendario, nonostante l’eliminazione del progetto fosse riuscita correttamente. (CQ-4358890)
* È stato risolto un problema in Firefox a causa del quale il piè di pagina della scheda &quot;Raccolta di risorse&quot; nella vista Progetto si sovrapponeva al bordo della scheda. Il piè di pagina ora viene allineato correttamente senza sovrapposizioni. (CQ-4353317)

#### Quickstart{#foundation-quickstart-65-lts-sp1}

* È stato aggiornato lo script di disinstallazione per regolare l’intervallo di versioni per il bundle Guava per evitare che venga inserito nell&#39;elenco Bloccati quando viene installato tramite il gestore di pacchetti. (GRANITE-59559)
* È stato risolto un problema nell&#39;interfaccia utente di replica a causa del quale veniva visualizzato un errore (`#1660`) durante la modifica degli agenti di replica; a tale scopo è stata corretta la gestione delle caselle di controllo classiche nell&#39;interfaccia. (GRANITE-58302)
* Sono stati risolti diversi errori di avvio per l’archivio dati S3 durante l’esecuzione di AEM 6.5 LTS con JDK 21, risolvendo il problema delle autorizzazioni di servizio mancanti, aggiornando la gestione della configurazione e garantendo la corretta inizializzazione dei servizi richiesti. (GRANITE-57082)
* È stata definita la strategia di manutenzione per AEM 6.5. Questa correzione includeva quanto segue:
   * Cadenza del Service Pack.
   * Cadenza dell&#39;hotfix.
   * Supporto parallelo con AEM 6.6.
   * Matrice di supporto aggiornata.
   * Responsabilità di proprietà del componente aggiuntivo. (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* Sling ResourceAccessSecurity è stato aggiornato alla versione 1.1.2 per risolvere un&#39;`ClassCastException` che si verificava quando più riferimenti a `ResourceAccessGate` inizializzavano `ResourceAccessSecurityImpl`. (NPR-42750)
* È stato risolto un problema nell’integrazione di Adobe Stock a causa del quale la finestra di dialogo Licenza veniva visualizzata in grigio. Questo problema era dovuto alla rimozione dei campi di input richiesti dalla funzione `sunt:initList`. La funzione è stata trovata nelle librerie client di Coral Foundation. Sono state aggiornate le librerie client per mantenere i campi necessari, abilitando la funzionalità appropriata della finestra di dialogo delle licenze. (NPR-42748)
* È stato corretto un errore di compilazione JSP imprevisto in `org.apache.sling.scripting.jsp 2.6.0`. (NPR-42640)

<!--
* Backported the fix for Sling Scripting issue that caused `DataTimeParseException` and `String.length()` null pointer exceptions during package installation. Updated Sling Scripting to version 2.8.3-1.0.10.6 to reduce installation errors and improve stability. (NPR-42640) -->

<!--

#### Translation{#foundation-translation-65-lts-sp1} -->

#### Interfaccia utente{#foundation-ui-65-lts-sp1}

* È stato risolto un problema nell’interfaccia utente di authoring di AEM che limitava la visualizzazione dei gruppi di utenti a 41. Questo problema era dovuto a un limite di batch predefinito nel componente di selezione dei gruppi dell’interfaccia utente Granite. Il componente è stato aggiornato per visualizzare tutti i gruppi senza troncamento. (NPR-42749)
* È stato risolto un problema nella procedura guidata per la creazione di pagine On-Prem, a causa del quale i campi obbligatori nei componenti con più campi non venivano riconvalidati durante la modifica delle proprietà della pagina. Questo problema, a sua volta, consentiva agli autori di ignorare la convalida e procedere con dati incompleti. (GRANITE-58826)
* Sono stati corretti gli attributi ARIA per il pulsante Guida in AEM per garantire che gli assistenti vocali JAWS visualizzino un&#39;etichetta chiara e intuitiva invece di visualizzare l&#39;icona non tradotta e i metadati di testo. (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* È stato aggiunto il supporto Java 17 per le traduzioni AEM aggiornando i bundle di traduzione, verificando la compatibilità dei pacchetti Java, rimuovendo le dipendenze obsolete e garantendo la piena funzionalità tramite test completi. (CQ-4357525)
* È stato rimosso il test Evergreen `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater` per evitare falsi errori durante il test automatico. (CQ-4298376)

#### Flusso di lavoro{#foundation-workflow-65-lts-sp1}

* È stato aggiunto l&#39;attributo `data-detailsurl` mancante negli elementi della casella in entrata per impedire la visualizzazione di valori non definiti negli URL quando si utilizza AEM 6.5 LTS con Java 21. (GRANITE-60158)
* È stata corretta un&#39;eccezione NullPointerException nel metodo `deactivate` del bundle `WorkflowToPublishEventService` durante l&#39;esecuzione di AEM 6.5 LTS con Java 21, garantendo l&#39;arresto corretto del servizio del flusso di lavoro senza errori. (GRANITE-58151)
* L&#39;indice del flusso di lavoro è stato aggiornato per supportare la condivisione, la personalizzazione fuori sede e la risoluzione dei problemi di query della timeline. (GRANITE-52640)
* L&#39;indice del flusso di lavoro è stato aggiornato per supportare la condivisione, le funzioni di personalizzazione fuori sede e la risoluzione dei problemi di query della timeline. (GRANITE-52294)
* Sono stati risolti un numero maggiore di errori di registro durante la convalida del confronto dei registri per un aggiornamento del programma ad AEM versione 10912, garantendo un&#39;esecuzione stabile del flusso di lavoro. (GRANITE-44268)
* È stato aggiornato il metodo di bonifica URL negli Archivi dei flussi di lavoro per sostituire `url.searchParams` con `url.search`, migliorando la protezione XSS per gli URL vulnerabili. (CQ-4359585)
* Sono state convalidate le funzionalità di flusso di lavoro, casella in entrata e Progetti in AEM 6.6 Forms per garantirne il corretto funzionamento e l&#39;integrazione. (CQ-4358777)
* È stata implementata l&#39;automazione per il rilascio di artefatti di contenuti dei flussi di lavoro tramite Jenkins, consentendo processi di distribuzione semplificati e coerenti in AEM 6.5. (CQ-4358472)
* È stato risolto un problema nel flusso di lavoro Crea attività nella casella in entrata a causa del quale, dopo aver fatto clic su Invia, la finestra di dialogo &quot;Aggiungi attività&quot; non si chiudeva a causa di un errore di sintassi JavaScript, nonostante l&#39;attività fosse stata creata. (CQ-4355336)
* È stato risolto un problema che impediva il salvataggio della configurazione della visualizzazione Casella in entrata a causa di una definizione di proprietà mancante per `isEndUserConfigurationEnabled`. (CQ-4287757)

## Moduli

### Forms Designer

* Quando un utente esporta i dati per un PDF basato su XFA utilizzando exportDataAPI, l’XML risultante mostra discrepanze rispetto ai dati XML esportati manualmente utilizzando Acrobat Reader. Nell’output mancavano valori di alcuni campi rispetto all’output generato da Acrobat Reader. (LC-3922791)
* La generazione di un PDF con tag con il servizio di output in Workbench aggiunge un tag di etichetta imprevisto sotto il tag di riferimento in un elemento del sommario. (LC-3922756)
* Quando si appiattiscono PDF dinamici compilabili in formato PDF/A utilizzando il servizio di output, lo stato dinamico non viene mantenuto. Questo comporta una perdita di dati e potenziali problemi di conformità, soprattutto quando è abilitata l’assegnazione di tag. (LC-3922708)
* Quando un utente inserisce le didascalie dei campi con allineamento in basso o a destra in AEM Forms Designer, la struttura ad albero dei tag include solo la didascalia senza il valore corrispondente, generando tag di accessibilità incompleti. (LC-3922619)
* I codici QR nei PDF generati diventano illeggibili. Anche il testo alternativo per i codici QR non supera il test di accessibilità, influendo sulla compatibilità dell’assistente vocale. (LC-3922551)
* Quando un utente esegue il rendering di una lettera nell’interfaccia utente dell’agente, la visualizzazione del contenuto non riesce a causa dell’API di render() di FormService. (LC-3922461)
* Quando un utente tenta di creare file PDF/A da XDP con stile Sunken Square in AEM Forms, si verificano problemi di rendering dei bordi. (LC-3922180)
* L’appiattimento dei moduli dinamici associati a uno schema XSD causa una perdita parziale di dati, in quanto alcuni dati dei moduli associati non vengono conservati nel PDF finale. (LC-3922008)
* Quando un utente tenta di esportare dati da PDF interattivi utilizzando l’API extractData in AEM Forms 6.5.13 e versioni successive, risultano dei dati mancanti rispetto all’esportazione manuale. (LC-3921983)
* La conversione di moduli XDP in PDF statici con AEM Forms Designer o il servizio di output crea più tag `Link-OBJR`. Questo causa un problema di conformità dell’accessibilità perché è previsto un singolo tag di collegamento unificato. (LC-3921977)

### Moduli adattivi

* In AEM Forms, se si abilita “Consenti testo formattato per il titolo” nel pannello principale, l’opzione “Escludi titolo dal documento di record” in un pannello nidificato nasconderà il titolo del pannello principale in modo errato. Questo errore si manifesta nel documento di record generato. (FORMS-19696)
* Il sistema ignora il `sling:resourceType` personalizzato assegnato tramite `aem:afProperties` in uno schema JSON. Il tipo di risorsa personalizzato viene ignorato durante il rendering. (FORMS-19691)
* Quando un utente invia un modulo adattivo con allegati precompilati utilizzando gli URI, tale invio non riesce e viene generata un’eccezione NullPointerException a causa della mancanza di dati binari. (FORMS-19371) (FORMS-19486)
* Quando un utente carica un PDF nella sezione “Moduli e documenti”, la funzione timeline smette di funzionare. (FORMS-19407)(FORMS-19234)
* Quando un utente carica i file utilizzando il componente predefinito (OOTB) del file allegato in AEM Forms, vengono identificate vulnerabilità di sicurezza. Questo problema può portare a una potenziale intercettazione del processo di invio da parte di entità non autorizzate. (FORMS-19271)
* Quando un utente configura un modulo adattivo predefinito in AEM Forms per generare automaticamente un documento di record (DoR), il campo “Titolo” in Proprietà documento di Acrobat Reader non visualizza il titolo DoR acquisito. Per impostazione predefinita, il titolo del modulo non viene visualizzato al posto del nome del file. (FORMS-19263)
* Quando un utente apre una comunicazione interattiva nell’interfaccia utente dell’agente, i dati precompilati non possono essere completamente cancellati; una volta rimossi, vengono ricompilati automaticamente con gli stessi dati. (FORMS-19151)
* Quando un utente visualizza l’anteprima di un campo data nell’interfaccia utente dell’agente, la data cambia in modo imprevisto. Questo problema si verifica a causa di discrepanze di fuso orario tra l’impostazione UTC della VM e l’interpretazione della data da parte del sistema. (FORMS-19115)
* Quando un utente invia un modulo, gli allegati potrebbero duplicarsi, generando più caricamenti dello stesso file. (FORMS-19045)(FORMS-19051)
* L’aggiunta di coordinatori ai set di criteri in Protezione documenti non riesce negli ambienti di produzione e in quelli inferiori. (FORMS-18603, FORMS-18212, FORMS-19697)
* Quando un utente fa clic sull’icona “datepicker-calendar-icon” in modalità desktop con un campo vuoto, si verifica un errore a causa della variabile _$focusDate non definita, che interrompe gli script personalizzati associati. (FORMS-18483)(FORMS-18268)
* Quando un cliente visualizza l’anteprima di una lettera, il campo “Quantità in parole” non viene visualizzato oppure aggiorna i valori numerici in modo errato, causando un disallineamento e una mancanza di spazi nel contenuto. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004)
* Quando un cliente visualizza in anteprima una lettera salvata su RHEL, il contenuto non risulta allineato, mancano spazi e vengono visualizzati caratteri imprevisti come la “x”. (FORMS-18422)(FORMS-17641)
* Quando un utente passa da una scheda all’altra in AEM Forms, la selezione dei componenti nella prima scheda risulta non reattiva. (FORMS-18345)
* Quando un utente converte un file HTML in PDF utilizzando l’opzione WebToPDF, nel PDF di output manca la sezione dell’intestazione, inclusi i tag di metadati e titolo. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224)
* In AEM JEE Process Manager SDK, quando un utente richiama il metodo retryAction(long actionOid), il sistema ritenta erroneamente la prima azione trovata nella tabella tb_action_instance. Questo flusso di lavoro si verifica anche quando viene fornito un ID azione specifico o quando l’ID è nullo, causando un comportamento non desiderato. (FORMS-18187)
* Un utente riscontra problemi quando le funzionalità di bozza e invio salvate non riescono senza visualizzare alcun messaggio di errore. (FORMS-18069)
* La transizione dai componenti di base basati su XSD ai componenti core impedisce l’implementazione di riferimenti tra file diversi negli schemi JSON, influendo sulla migrazione dei moduli adattivi. (FORMS-18065)
* Quando un utente visualizza l’anteprima di una lettera nell’interfaccia utente dell’agente, il campo data mostra un valore errato a causa di problemi di conversione dell’ora in IC. Queste discrepanze derivano dalle differenze di fuso orario tra l’ambiente VM e l’interpretazione dell’orario da parte del sistema (UTC rispetto all’ora locale). (FORMS-17988) (FORMS-17248)
* Quando un utente visualizza l’anteprima delle lettere utilizzando i modelli IC di avviso in AEM Forms, i tempi di generazione dei PDF variano in modo significativo, da 1,5 secondi a più di 10, anche sullo stesso server. Questa incoerenza influisce sui flussi di lavoro critici per l’azienda. (FORMS-17951)
* Quando un utente associa un oggetto Firma scarabocchio in un modulo adattivo a un XDP utilizzando l’opzione “Origini dati” le modifiche non possono essere salvate. Il motivo è dovuto a errori di convalida delle proporzioni persistenti, anche quando si utilizzano valori validi. (FORMS-17587)
* Quando un utente utilizza un XDP specifico con molti campi nascosti per i frammenti di documento, AEM crea nodi CRX con la proprietà `cm:optional` impostata su falso, causando un errore nell’invio della comunicazione interattiva (IC). (FORMS-17538)
* Quando un cliente visualizza l’anteprima di una lettera, il campo della casella numerica non è in grado di gestire correttamente i valori negativi quando sono definiti limiti per le cifre lead e frac (interi e decimali). Questo problema si verifica a causa dell’utilizzo di parseFloat, che tratta il segno meno come parte del numero. (FORMS-17451)
* Quando una lettera viene visualizzata in anteprima, si nota l’utilizzo del carattere jolly “*” nel file Adobe.json, sollevando dubbi sul suo scopo e sulla potenziale modifica. (FORMS-17317)
* Quando un utente utilizza l’assistente vocale nella sezione Richiedi un conto cointestato di risparmio a tasso fisso, le intestazioni vengono erroneamente annunciate come cliccabili, causando problemi di accessibilità. (FORMS-17038)
* Quando un modulo è incorporato, nell’iframe generato manca l’attributo titolo, il che provoca un problema di conformità per l’accessibilità. (FORMS-17010)
* Il download di un modulo tramite l’interfaccia utente Gestione moduli include sempre le dipendenze associate, ad esempio temi e frammenti. (FORMS-15811)
* Quando un utente accede al modulo su dispositivi mobili (iOS e Android™), i pulsanti “Avanti” e “Precedente” nella prima pagina sono disabilitati. Tuttavia, l’assistente vocale non li identifica come disabilitati. (FORMS-15773)
* Quando un utente salva un modulo di grandi dimensioni con frammenti e caricamento lento abilitati, non riesce a recuperare le bozze, interrompendo il flusso di lavoro. (FORMS-19890, FORMS-19808)
* Gli utenti hanno riscontrato dei problemi durante il salvataggio delle proprietà del modulo adattivo basato sui componenti core. Ciò si verificava perché venivano inclusi script ridondanti provenienti dal modulo adattivo basato sull’editor di componenti di base, causando conflitti nel modulo adattivo basato sui componenti core. editor. (FORMS-17474)
* Gli utenti hanno riscontrato dei problemi con la pagina Firma di Adobe Sign GovCloud che non eseguiva il rendering in un iframe. (FORMS-16803)
* Gli utenti rilevano degli errori durante la selezione dei riferimenti per i frammenti dei moduli adattivi (AF) dei componenti core. Viene visualizzato il messaggio di errore “Impossibile eseguire il rendering del riferimento: percorso non assoluto”, che impedisce il rendering del riferimento corretto. (FORMS-19678)
* È stato aggiunto il supporto per la conversione di file con più thread con Acrobat DC, consentendo agli utenti di eseguire conversioni simultanee di documenti Word, Excel e PowerPoint in documenti PDF in modo più efficiente. (FORMS-21310)
* È stata aggiunta l’inclusione del bundle `com.adobe.granite.toggle.impl.dev` in AEM Service Pack 24 per consentire processi di sviluppo più semplificati rimuovendolo dal componente aggiuntivo dei moduli. (FORMS-20139)
* FeatureToggleRenderConditionServlet è stato rimosso dal bundle forms-foundation e com.adobe.granite.toggle.impl.dev dal componente aggiuntivo dei moduli. Questo aggiornamento garantisce che, dopo l’installazione del componente aggiuntivo dei moduli, la condizione di rendering venga risolta correttamente, migliorando le funzionalità dei componenti per la clientela. (FORMS-20138)
* Gli utenti hanno riscontrato un rallentamento delle prestazioni a causa di query con tempi di esecuzione lunghi nei moduli adattivi. Questo aggiornamento esegue il backport delle modifiche alle query per migliorare l’efficienza. La clientela ora può creare l’indice con il nome tag aemformsAFReferences. (FORMS-21411)
* Gli utenti hanno riscontrato degli errori di allineamento delle posizioni di intestazione durante la conversione di HTML in PDF (Portable Document Format) con WebtoPDF. Questo problema influiva sulla coerenza del layout del documento e sulla leggibilità dell’output. (FORMS-21502, FORMS-21540)
* Gli utenti hanno riscontrato errori di convalida PDF/A-1b nonostante la verifica preliminare sia stata eseguita correttamente. Questo problema ha interessato i controlli di conformità dei documenti per la clientela enterprise che utilizza strumenti di convalida PDF. (FORMS-20196)
* Gli utenti hanno riscontrato stringhe non tradotte nell’interfaccia utente, che causano confusione e difficoltà nella comprensione dell’interfaccia. (FORMS-6542)
* Gli utenti hanno riscontrato problemi con le notifiche e-mail. Il passaggio del flusso di lavoro Invia e-mail non è riuscito a inviare le e-mail, con un impatto sui processi di comunicazione automatizzati. (FORMS-17961)
* Gli utenti hanno riscontrato test non riusciti per i flussi di lavoro di Forms, che hanno influito sulla loro capacità di completare i processi di flusso di lavoro in modo efficiente. (FORMS-16231)
* Gli utenti sono stati impossibilitati a utilizzare la funzione timeline dei PDF in AM Forms. Questo problema ha influito sulla capacità degli utenti di tenere traccia delle modifiche e delle revisioni dei documenti in modo efficace. Durante il caricamento di un PDF nella sezione “Moduli e documenti” dell’area di AEM Forms, la vista timeline non funziona più. (FORMS-19408)
* Gli utenti rilevano un’eccezione Null Pointer durante l’interazione con OData. Questo causa interruzioni nei processi di recupero dei dati. (FORMS-20348)
* È stata rimossa la libreria google.common.collect in seguito alla rimozione di Guava, una libreria Java open-source. Questo aggiornamento garantisce compatibilità e prestazioni migliori per la clientela enterprise che utilizza Moduli adattivi. (FORMS-17031)

### Captcha Forms

* È stato aggiunto il supporto `Hcaptcha` e `Turnstile` per i Moduli adattivi basato su componenti di base. (FORMS-16562)
* Gli utenti hanno riscontrato problemi di sovrapposizione delle icone nella finestra di dialogo `Create hCaptcha Configuration`. Durante la compilazione dei campi obbligatori, l’icona delle informazioni si sovrapponeva all’icona di errore, generando confusione durante l’impostazione della configurazione. (FORMS-16916)
* Gli utenti hanno riscontrato un’errata configurazione rilevata per reCAPTCHA in Moduli adattivi basata sui componenti di base. Quando il contenitore di configurazione non era selezionato per un modulo, il problema era causato da più configurazioni nella cartella `conf/global`. (FORMS-19237)
* Gli utenti hanno riscontrato dei problemi che impedivano il rendering di reCAPTCHA. Questo problema interessava l’invio dei moduli e la convalida di sicurezza per la clientela enterprise. (FORMS-17136, FORMS-19596)
* Gli utenti riscontrano un problema a causa del quale le dimensioni di reCAPTCHA enterprise non vengono riportate nell’interfaccia utente. (FORMS-16574)
* Gli utenti hanno riscontrato problemi con la funzionalità ReCaptcha a causa di un ResourceResolver non chiuso in `ReCaptchaConfigurationServiceImpl`, che hanno causato errori di convalida intermittenti durante l’invio dei moduli. (FORMS-19241)
* Gli utenti hanno riscontrato problemi con la convalida reCAPTCHA quando i moduli vengono creati in Sites. AEM Forms non riconosceva correttamente il nome del modulo, causando errori di convalida. (FORMS-20486)
* Gli utenti hanno riscontrato invii di moduli anche quando il punteggio enterprise di reCAPTCHA era 1.0, con potenziali rischi per la sicurezza. FORMS-16766){{$include }}
* È stato migliorato l’avviso reCAPTCHA in Moduli adattivi aggiornando i codici di errore di invio a 400. Inoltre, gli avvisi di registro sono stati perfezionati per distinguere tra timeout, scadenze e errori di rilevamento dei bot, migliorando l’accuratezza della risoluzione dei problemi e l’osservabilità del sistema. (FORMS-19240)
* È stata chiusa un’istanza ResourceResolver non chiusa in ReCaptchaConfigurationServiceImpl per evitare potenziali perdite di risorse e migliorare la stabilità del sistema quando si utilizzano integrazioni reCAPTCHA in AEM Forms. (FORMS-19242)
* È stata migliorata la gestione della configurazione CAPTCHA per AEM Forms, garantendo che la configurazione corretta venga associata a ciascun modulo quando esistono più voci nella cartella /conf/global. Impedisce l’utilizzo involontario di impostazioni CAPTCHA errate quando il contenitore di configurazione non è selezionato in modo esplicito. (FORMS-19239)

### Interfaccia utente per la gestione dei moduli

* Gli utenti hanno riscontrato stringhe non localizzate nel processo di creazione `Forms` > `Create Watchfolder` >` Watchfolder`. Durante la creazione di una cartella controllata, non sono state trovate stringhe quali `Watchfolder creation` e `Watchfolder created successfully`, con effetti sull’esperienza di interfaccia utente. (FORMS-15234)

## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 LTS si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e dell’archivio dei contenuti Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x è utilizzato come motore servlet per Quickstart.

### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituisci i valori predefiniti del GC (catalogo globale) con altri valori. Per ulteriori informazioni, consulta la sezione [Installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuisce gli aggiornamenti di manutenzione Java™ 17 e Java™ 21 per l’utilizzo da parte del cliente nei progetti correlati ad AEM, se non disponibili pubblicamente da Oracle.

### Pacchetto Uberjar {#uber-jar-packaging}

* Il pacchetto Uberjar di AEM 6.5 LTS presenta una leggera differenza. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Aggiornamento {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).
* Per istruzioni di aggiornamento dettagliate, consulta la [Guida all&#39;aggiornamento per AEM Forms 6.5 LTS SP1 su JEE](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### Best practice per gli aggiornamenti del Service Pack di AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**Ambiente**
Si applica a: clienti AEM 6.5 LTS (On-Premise) che installano il Service Pack 1 (SP1). SP1 viene fornito come file Quickstart JAR.

**Perché è importante**
SP1 per AEM 6.5 LTS viene fornito come file Quickstart JAR anziché come file ZIP da installare tramite Gestione pacchetti. I clienti on-premise possono eseguire l’aggiornamento sostituendo il file Quickstart JAR, decomprimendolo e riavviandolo. Questo metodo è coerente con la procedura di aggiornamento diretto di Adobe.

**Flusso di aggiornamento consigliato (authoring o pubblicazione)**

1. Verifica che l’istanza AEM 6.5 LTS sia integra e accessibile.
1. Scarica il file Quickstart JAR di SP1 (ad esempio, `cq-quickstart-6.6.x.jar`) da Distribuzione del software Adobe.
1. Arresta l&#39;istanza in esecuzione.
1. Nella directory di installazione di AEM (esterna a `crx-quickstart/`), sostituisci il file Quickstart JAR precedente con il file JAR SP1.
1. Decomprimi il file JAR:

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (Regola i flag dell&#39;heap in base alle esigenze).

1. Rinomina il file JAR decompresso in modo che corrisponda al ruolo e alla porta, ad esempio `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Avvia AEM e conferma l’aggiornamento nell’interfaccia utente (Guida > Informazioni) e nei registri.

**Buone pratiche**

* Esegui l’aggiornamento in ambienti di test o inferiori prima di eseguirlo in ambienti di produzione.
* Prima di iniziare, esegui backup completi e ripristinabili (repository più eventuali datastore esterni).
* Consulta la guida all’aggiornamento diretto di Adobe e i requisiti tecnici (consigliato Java 17/21 per LTS).

>[!NOTE]
>
>I nomi file mostrati sopra (ad esempio, `cq-quickstart-6.6.x.jar`) riflettono la denominazione dell&#39;artefatto Quickstart SP1 di questa versione LTS; utilizza sempre lo stesso nome del file scaricato da Distribuzione del software Adobe.

## Installazione e aggiornarnamento {#install-update}

Per i requisiti di configurazione, consulta [Istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

>[!NOTE]
>
> Se esegui l’aggiornamento diretto a LTS SP1 da 6.5 SP precedenti, segui le istruzioni fornite per l’[aggiornamento](/help/sites-deploying/upgrade.md) da 6.5 a 6.5 LTS GA.


Per istruzioni dettagliate, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Per le nuove installazioni di AEM 6.5 LTS, le definizioni degli indici devono essere installate separatamente. Per informazioni più dettagliate, consulta questo [articolo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Installare e aggiornare il componente aggiuntivo AEM Forms {#install-update-aem-forms-add-on}

Per istruzioni dettagliate, consulta [Esecuzione di un aggiornamento diretto](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions).



## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, sui [requisiti tecnici AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Si consiglia di utilizzare le versioni Java™ 17/Java™ 21 con AEM 6.5 LTS.


## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe rivede ed evolve continuamente le funzionalità dei prodotti per offrire maggiore valore ai clienti, modernizzando o sostituendo le funzionalità legacy. Queste modifiche vengono implementate prestando particolare attenzione alla compatibilità con le versioni precedenti.

Per garantire trasparenza e consentire una pianificazione adeguata, Adobe segue questo processo di deprecazione per Adobe Experience Manager (AEM):

* La deprecazione viene annunciata per prima. Le funzionalità obsolete rimangono disponibili ma non vengono più migliorate.

* La rimozione avviene non prima della versione principale successiva. La sequenza temporale della rimozione pianificata viene comunicata separatamente.

* Ai clienti è fornito almeno un ciclo di rilascio per la transizione alle alternative supportate prima della rimozione di una funzionalità.

### Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità che Adobe ha dichiarato obsolete in AEM 6.5 LTS. In genere, Adobe depreca le funzioni prima di rimuoverle in una versione futura e fornisce un’alternativa.

Consigliamo alla clientela di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione | Sostituzione | Versione (SP) |
| --- | --- | --- | --- |
| Sites | [Editor SPA](/help/sites-developing/spa-overview.md) | Gli editor preferiti per la gestione dei contenuti headless in AEM sono:<br>- [l’editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.<br>- [Editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo. | 6.5 LTS GA |
| [!DNL Foundation] | Supporto per com.adobe.granite.oauth.server | Integrazione di Adobe IMS |  |

### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità e le funzioni che sono state rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

* Il supporto per RDBMK per la persistenza dell’archivio CRX è stato rimosso.

* Negli ambienti cluster, MongoMK è ora l’unica opzione supportata per la persistenza dell’archivio.

| Area | Funzione | Sostituzione | Versione (SP) |
| --- | --- | --- | --- |
| Commerce | AEM CIF Classic non è supportato. | Esegui la migrazione a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluzioni | Social/Communities non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Screens | Gli Screens non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Risorse | `dam-pim` e `dam-rating` non sono supportati perché i bundle dipendono dal social. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Risorse | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` è stato rimosso. | Utilizza l’API alternativa `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` che è stata aggiunta. | 6.5 LTS GA |
| Portale | AEM Portal Director non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | Il bundle `com.adobe.granite.socketio` è stato rimosso. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | `crx2oak` non è supportato. | Scegliere la versione rilevante di [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Guava | Tutte le dipendenze guava ora vengono rimosse in AEM e pertanto il bundle `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` non fa parte di AEM. | Se possibile, la clientela può aggiungere guava autonomamente se dipende da guava o sostituire il codice guava con raccolte java o altre alternative. | 6.5 LTS GA |
| `We.Retail` | Il sito di esempio `We-retail` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | Il bundle `oak-solr-osgi` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` e `org.apache.sling.atom.taglib` non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | I pacchetti `org.apache.commons.io` ora vengono esportati da `org.apache.commons.commons-io`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | Esportazione dei pacchetti `javax.mail` dal bundle `com.sun.javax.mail`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | I pacchetti `org.apache.jackrabbit.api` ora vengono esportati dal bundle `org.apache.jackrabbit.oak-jackrabbit-api`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | `com.github.jknack.handlebars` non è supportato | Scegli la [versione](https://mvnrepository.com/artifact/com.github.jknack/handlebars) pertinente | 6.5 LTS GA |


## Problemi noti {#known-issues}

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

<!-- REMOVED THIS SECTION AS PER CQDOC-23046
### Issue with JSP scripting bundle in AEM 6.5.21-6.5.23 and AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23, and AEM 6.5 LTS GA ship with the `org.apache.sling.scripting.jsp:2.6.0` bundle, which contains a known issue. The issue typically occurs under high load when the AEM instance handles many concurrent requests.

When this issue occurs, one of the following exceptions may appear in the error logs alongside references to `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

A hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) is available to resolve this problem. -->

### Errore di connessione di Dispatcher con la funzione solo SSL (risolto in AEM 6.5 LTS SP1 e versioni successive){#ssl-only-feature}

>[!NOTE]
>
> Questo problema è presente solo nella versione AEM 6.5 LTS GA.

Quando si abilita la funzione solo SSL nelle implementazioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze Dispatcher e AEM. Dopo aver abilitato questa funzione, le verifiche stato potrebbero non riuscire e la comunicazione tra le istanze Dispatcher e AEM potrebbe essere interrotta. Questo problema si verifica in modo specifico quando i clienti tentano di connettersi tramite `https + IP` dalle istanze Dispatcher ad AEM. È correlato a problemi di convalida SNI (Server Name Indication).

**Impatto:**

* Errori di verifica stato con codici di risposta HTTP 400
* Traffico interrotto tra istanze Dispatcher e AEM
* Il contenuto non può essere gestito correttamente tramite Dispatcher
* Errori di connessione durante l’utilizzo di HTTPS con indirizzi IP nella configurazione di Dispatcher
* HTTP 400: errori “SNI non valida” durante la connessione tramite HTTPS + IP

**Ambienti interessati:**

* Implementazioni di AEM con configurazioni Dispatcher
* Sistemi in cui è stata abilitata la funzione solo SSL
* Configurazioni di Dispatcher che utilizzano il metodo di connessione `https + IP` alle istanze AEM

**Soluzione:**
se riscontri questo problema, contatta l’Assistenza Clienti di Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip). Non tentare di abilitare le funzioni solo SSL finché non viene applicato l’hotfix necessario.

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i Pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 LTS, Service Pack 1:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei Pacchetti di contenuti inclusi in Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web con restrizioni{#restricted-sites}

Questi siti web sono disponibili solo per la clientela. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/it/docs/customer-one/using/home).

