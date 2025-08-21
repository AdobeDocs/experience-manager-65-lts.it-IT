---
title: Note sulla versione corrente per Adobe Experience Manager 6.5 LTS, SP1
description: Trova informazioni sulla versione corrente per Adobe Experience Manager 6.5 LTS, Service Pack 1.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: b6a5e6bacfee72e162ce3bc035f909c02fbbf6db
workflow-type: tm+mt
source-wordcount: '4935'
ht-degree: 14%

---

# Note sulla versione corrente per Adobe Experience Manager 6.5 LTS, SP1 {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versione | Service Pack 1 (SP1) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | 21 agosto 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione software](https://artifactory.corp.adobe.com/artifactory/maven-aem-release-local/com/adobe/aem/cq-quickstart/6.6.1/cq-quickstart-6.6.1.jar) |

<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## Cosa è incluso in [!DNL Adobe Experience Manager] 6.5 LTS, SP1 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP1 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale di 6,5 LTS a marzo 2025. [Installare il Service Pack](#install-update) su 6,5 LTS.

<!-- ## Key features and enhancements -->

<!-- 6.5 LTS REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE EACH RELEASE -->

## Sono stati risolti i problemi in 6.5 LTS, Service Pack 1 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP1}

#### Accessibilità {#sites-accessibility-65-lts-sp1}

* È stato risolto un problema a causa del quale l’elemento dell’editor di testo nei Frammenti di contenuto veniva troncato per impostazione predefinita. L’editor di testo ora visualizza il contenuto completo senza troncamento. (SITES-33005)
* È stato risolto un problema che causava l&#39;apertura della home page di Indigo al posto dell&#39;URL di destinazione corretto quando si faceva clic su URL paths. (SITES-33004)
* È stato risolto un problema di accessibilità in un componente AEM personalizzato che causava errori di conformità ADA durante il test automatizzato. (SITES-30660)
* Sono stati risolti i problemi di conformità ADA nella finestra di dialogo Avviso e Messaggi del flusso di lavoro garantendo la visualizzazione del testo in nero su sfondi chiari e la conformità ai requisiti di contrasto di WCAG 2.0. (SITES-30138)
* È stato risolto un problema di accessibilità a causa del quale il pulsante &quot;Category&quot; nell’editor di AEM Sites mancava di un’etichetta specifica, causando l’annuncio da parte di JAWS di come &quot;Images button menu&quot; (Menu pulsante Immagini) invece di fornire un’etichetta descrittiva. (SITES-27497)
* È stato risolto un problema di accessibilità a causa del quale le icone dei segni di spunta nella schermata Autorizzazioni effettive mancavano di testo alternativo, impedendo a JAWS di leggere e trasmettere il loro significato. (SITES-27272)
* È stato risolto un problema di accessibilità a causa del quale la pagina Autorizzazioni non conteneva un chiaro annuncio JAWS per la rimozione delle autorizzazioni di utenti o gruppi, generando confusione per gli utenti di utilità per la lettura dello schermo. (SITES-27238)
* È stato risolto un problema di accessibilità a causa del quale i messaggi di errore venivano visualizzati solo come icone senza testo descrittivo, impedendo a JAWS di annunciare gli errori quando si verificavano. (SITES-27155)
* È stato risolto un problema di accessibilità a causa del quale JAWS leggeva descrizioni dei pulsanti non corrette e non chiare nell’ambiente AEM On-Premise, incluso il testo del livello di intestazione 2 mancante per la sezione dei moduli. (SITES-27152)
* È stato risolto un problema di accessibilità a causa del quale JAWS non annunciava il numero di risultati dopo il filtraggio dei valori nella scheda AEM Assets. (SITES-27150)
* È stato risolto un problema di accessibilità a causa del quale la creazione di una cartella non mostrava una conferma e JAWS non la annunciava nell’interfaccia utente di Assets. (SITES-27141)
* È stato risolto un problema di accessibilità in AEM Sites. JAWS non ha annunciato errori modulo, lo stato attivo è stato spostato su elementi di errore non interattivi e gli errori dei campi obbligatori non sono stati visualizzati alla tabulazione. (SITES-27138)
* È stato risolto un problema di accessibilità a causa del quale il menu del pulsante Timeline non disponeva di un’etichetta specifica, causando la lettura di solo &quot;Menu del pulsante Attività&quot; da parte di JAWS senza fornire una descrizione chiara. (SITES-27134)
* È stato risolto un problema di accessibilità a causa del quale JAWS non annunciava l’azione o il ruolo per gli elementi contenitore, leggendo solo &quot;Breadcrumb v1&quot; e &quot;button v2&quot; invece delle etichette descrittive. (SITES-27131)
* È stato risolto un problema di accessibilità a causa del quale il pop-up Pubblicazione rapida non forniva un messaggio di successo corretto, impedendo agli assistenti vocali di annunciare il feedback di completamento. (SITES-26912)
* È stato risolto un problema di accessibilità nella vista a colonne di corallo a causa del quale gli elementi con ruoli ARIA che richiedevano ruoli figlio non li contenevano, causando la mancata conformità agli standard di accessibilità. (SITES-26898)
* È stato risolto un problema di accessibilità a causa del quale i testi &quot;modello&quot; e &quot;proprietà&quot; nella navigazione superiore della pagina di creazione non erano visibili in modalità Riflusso, impedendo l’accesso agli utenti che utilizzano tastiera e utilità per la lettura dello schermo. (SITES-26895)
* È stato risolto un problema di accessibilità a causa del quale le descrizioni comandi per le icone &quot;search&quot;, &quot;solution&quot;, &quot;help&quot;, &quot;inbox&quot; e &quot;user&quot; nella navigazione superiore non erano accessibili tramite la navigazione da tastiera. (SITES-26889)
* È stato risolto un problema di accessibilità a causa del quale i campi modulo scheda Base non fornivano suggerimenti di errore, impedendo agli utenti di ricevere indicazioni quando i campi di input obbligatori venivano lasciati vuoti. (SITES-26885)
* È stato risolto un problema di accessibilità a causa del quale gli assistenti vocali di NVDA e Assistente vocale non annunciavano i dettagli dei file modello nella pagina Crea, impedendo agli utenti di ricevere informazioni complete a livello di programmazione. (SITES-26884)
* È stato risolto un problema di accessibilità a causa del quale veniva utilizzato un nome errato per la casella di testo &quot;Titolo pagina&quot; nella scheda Base, impedendo agli assistenti vocali di fornire informazioni accurate agli utenti. (SITES-26879)
* Sono stati aggiornati i colori di primo piano e di sfondo dei pulsanti per soddisfare i requisiti del rapporto di contrasto minimo di WCAG 2.2 AA, migliorando la leggibilità e l’accessibilità per tutti gli utenti. (SITES-26877)
* È stato risolto un problema che causava la scomparsa dei testi &quot;modello&quot; e &quot;proprietà&quot; nella navigazione superiore della pagina di creazione dopo il ridimensionamento, garantendo visibilità e accessibilità agli utenti ipovedenti. (SITES-26872)
* È stato risolto un problema che causava la visualizzazione di più barre di scorrimento orizzontali sulla pagina principale dopo l’applicazione di un riversamento, garantendo una singola barra di scorrimento per la corretta accessibilità e visibilità del contenuto. (SITES-26800)
* È stato risolto un problema di accessibilità nell’Editor pagina di AEM a causa del quale lo stato attivo sulla tastiera si ripristina all’inizio della barra degli strumenti Demografica dopo l’attivazione di pulsanti come Persona, Carrello o Abbandonato. Ora è attivo il pulsante attivato per supportare flussi di lavoro coerenti per la navigazione da tastiera e l’utilità di lettura dello schermo. (SITES-25306)
* È stato risolto il problema di associazione delle etichette di accessibilità per i campi titolo pagina e tag. L’interfaccia di AEM ora associa correttamente le etichette di accessibilità ai campi &quot;Titolo&quot; e &quot;Titolo pagina&quot; quando si utilizzano utilità per la lettura dello schermo come JAWS. La correzione assicura la corretta lettura delle etichette e migliora la conformità ADA nei flussi di lavoro di creazione, proprietà e spostamento delle pagine. (SITES-27149)
* È stata corretta l’etichetta visiva mancante per i campi di input dei commenti nella timeline. Sono state corrette le etichette visive mancanti per i campi di input &quot;commento&quot; nella sezione timeline per migliorarne l’accessibilità. L’aggiornamento garantisce che gli assistenti vocali possano annunciare con precisione le etichette dei campi. Questa esperienza migliora la navigazione e l’invio dei moduli per tutti gli utenti, in particolare gli utenti che si basano su tecnologie per l’accessibilità. (SITES-26903)
* È stata corretta l’accessibilità da tastiera per il pulsante con puntini di sospensione nei commenti della timeline. Attivazione della navigazione tramite tastiera per il pulsante con puntini di sospensione (tre punti) accanto ai commenti nella sezione timeline. Gli utenti possono ora accedere al pulsante e interagire con esso utilizzando il tasto TAB, migliorando l’accessibilità per gli utenti che si affidano alla navigazione tramite sola tastiera. (SITES-26891)
* Sono stati migliorati gli annunci NVDA/Assistente vocale per i risultati di ricerca nelle finestre di dialogo di selezione. È stata aggiornata la finestra di dialogo Apri selezione per indicare se i risultati della ricerca vengono trovati o meno quando si utilizzano utilità per la lettura dello schermo, come NVDA o Assistente vocale. Questo miglioramento consente agli utenti che si affidano alle tecnologie per l’accessibilità di comprendere il risultato delle azioni di ricerca senza bisogno di conferma visiva. (SITES-26883)
* È stato corretto il ruolo ARIA per l’icona con i puntini di sospensione accanto al campo di input del commento. È stata aggiornata l’icona con i puntini di sospensione (tre punti) accanto al campo di immissione del commento per utilizzare il ruolo ARIA corretto, in modo che gli assistenti vocali possano identificare con precisione l’elemento. Questo miglioramento migliora la conformità in materia di accessibilità e l’esperienza degli utenti che si affidano alle tecnologie per l’accessibilità. (SITES-26881)
* Sono stati corretti gli attributi ARIA non validi nei componenti dell’interfaccia utente Coral. Sono stati aggiornati i componenti dell’interfaccia utente Coral per garantire che tutti gli attributi ARIA utilizzino valori validi, migliorando l’accessibilità e la conformità. In particolare, sono stati risolti casi in cui valori non validi come `aria-modal="dialog"` non venivano assegnati correttamente. Questo miglioramento consente agli assistenti vocali di interpretare correttamente gli elementi delle finestre di dialogo, migliorando l’accessibilità per gli utenti che si affidano a tecnologie per l’accessibilità. (SITES-26873)
* Sono state migliorate la visibilità e le descrizioni per le icone negli scenari di riversamento. È stato migliorato il comportamento Ridisponi per garantire la corretta visualizzazione delle descrizioni per le icone **Scarica**, **Rielabora risorse** e **Estrai**. Focalizzato su un problema di accessibilità in cui le icone e le relative etichette diventavano invisibili quando il riquadro di visualizzazione veniva ridimensionato o le impostazioni di zoom del browser cambiavano. Questa correzione consente di mantenere la visibilità degli utenti ipovedenti e fornisce descrizioni delle icone durante il riversamento. (SITES-26871)


#### Interfaccia utente amministratore{#sites-adminui-65-lts-sp1}

* È stato risolto un problema di accessibilità a causa del quale JAWS non annunciava i ruoli elenco né forniva istruzioni di navigazione e attivazione nella finestra di dialogo Crea sito. (SITES-30661)
* Il supporto per gli assistenti vocali per i messaggi di stato nella vista filtro Sites funziona come previsto, garantendo agli utenti un feedback chiaro e tempestivo quando passano da una visualizzazione all’altra. (SITES-24992)
* Il selettore data nella barra dei filtri viene visualizzato completamente all’interno del relativo contenitore, fornendo dimensioni di destinazione di contatto adeguate ed eliminando i problemi di clipping. (SITES-24988)
* I tag di filtro selezionati ora utilizzano etichette semantiche HTML e aria corrispondenti alla presentazione visiva, garantendo un supporto preciso dei ruoli e azioni chiare per le tecnologie per l’accessibilità. (SITES-24980)
* È stato aggiunto un attributo aria-label all’area della barra Riferimenti per fornire un’etichetta univoca e descrittiva per gli utenti degli assistenti vocali e garantire un’identificazione coerente dei punti di riferimento all’interno della pagina. (SITES-24973)
* La barra Riferimenti è stata aggiornata per utilizzare le unità relative per il dimensionamento e il posizionamento, consentendo la scalabilità e la piena funzionalità del contenuto quando viene ingrandito al 400% in un riquadro di visualizzazione 1280x1024. (SITES-24972)
* Gli elementi di tabella confermati nella visualizzazione elenco della home page di Sites contengono ruoli di intestazione di colonna corretti, che consentono agli assistenti vocali di annunciare le intestazioni per ogni cella di dati. (SITES-24942)
* NVDA ora annuncia la data di modifica nella directory ad albero, garantendo che gli utenti che usano utilità di lettura dello schermo ricevano informazioni complete sui dettagli delle risorse. (SITES-24782)
* È stato risolto un problema a causa del quale l’assistente vocale NVDA annunciava un testo incompleto per gli elementi nel componente Directory ad albero in AEM Sites. NVDA legge ora il testo completo per ogni elemento, migliorando l’accessibilità e la conformità. (SITES-24780)
* È stata aggiunta l&#39;accessibilità della tastiera alla barra di divisione della finestra nella directory ad albero, consentendo agli utenti di ridimensionare la barra laterale sinistra utilizzando solo una tastiera. (SITES-24779)
* Sono stati aggiornati i risultati della ricerca nel menu Aiuto per includere i ruoli ARIA corretti per le voci di elenco, garantendo che gli assistenti vocali annuncino correttamente i collegamenti per migliorare l’accessibilità. (SITES-24729)
* È stato risolto un problema a causa del quale gli assistenti vocali non annunciavano il messaggio di stato &quot;X di Y risultati&quot;. Oppure il messaggio &quot;nessun risultato trovato&quot; dopo l’applicazione di filtri nel pannello Filtro siti, per garantire che gli utenti ricevano la conferma corretta dei risultati. (SITES-24720)
* Sono state corrette le assegnazioni di ruolo mancanti per i collegamenti di navigazione nella navigazione dell’app. Sono stati aggiunti i ruoli ARIA appropriati per garantire che gli assistenti vocali identifichino e annunciino correttamente gli elementi di navigazione. (SITES-24719)
* Il markup del ruolo griglia non corretto per i tag filtro selezionati è stato sostituito con gli elementi dei pulsanti e i nomi accessibili aggiunti, in modo che gli assistenti vocali possano annunciare e identificare correttamente i tag. (SITES-24717)
* Sono stati aggiunti annunci di utilità di lettura dello schermo per il messaggio di stato della barra Riferimenti quando si eseguono selezioni multiple, in modo che gli utenti ricevano conferma delle modifiche. (SITES-24678)
* È stato corretto il comportamento del campo di ricerca in modo che il primo risultato non venga annunciato automaticamente. Gli assistenti vocali ora annunciano il numero di risultati trovati, consentendo agli utenti di navigare nell’elenco senza annunci di attivazione errati. (SITES-24658)
* Gli attributi `aria-label` non corretti sono stati rimossi dagli elementi statici non interattivi nella visualizzazione elenco per impedire agli assistenti vocali di annunciare informazioni fuorvianti o irrilevanti. (SITES-24515)
* La casella di controllo nella prima colonna della Vista a elenco è stata aggiornata per utilizzare il testo della colonna Titolo come nome accessibile, in modo che gli assistenti vocali possano comunicare con precisione lo scopo del campo modulo. (SITES-24514)
* Sono stati aggiunti gli attributi ARIA appropriati e il supporto per le aree attive per annunciare il caricamento dei messaggi di stato agli utenti di utilità di lettura dello schermo durante la navigazione all’interno del contenuto. (SITES-24481)
* È stato aggiornato il design reattivo per eliminare lo scorrimento orizzontale quando il contenuto viene ingrandito al 400% con una larghezza del riquadro di visualizzazione di 1280×1024, garantendo una visibilità completa senza scorrimento laterale. (SITES-24308)
* È stata corretta la navigazione dello stato attivo nell’interfaccia utente di amministrazione di Sites in modo da seguire un ordine logico, riportando lo stato attivo sul pulsante &quot;Seleziona tutto&quot; dopo aver premuto Esc e spostando lo stato attivo sull’elemento interattivo successivo dopo aver premuto Tab. (SITES-24307)
* È stato aggiornato l&#39;ordine di attivazione nell&#39;interfaccia utente di amministrazione di Sites in modo che il pulsante Breadcrumb nell&#39;elemento `<betty-titlebar-title>` riceva lo stato attivo nella sequenza corretta durante la navigazione da tastiera. (SITES-24305)
* È stata verificata la funzionalità di salto di collegamento per garantire che sposti lo stato attivo sulla tastiera nell’area del contenuto principale, consentendo agli utenti che utilizzano la tastiera di ignorare gli elementi dell’intestazione e di accedere ai contenuti in modo efficiente. (SITES-24061)


#### Interfaccia classica{#sites-classicui-65-lts-sp1}

È stato risolto un problema nell’interfaccia classica a causa del quale le etichette delle caselle di controllo non erano presenti e HTML veniva visualizzato come testo codificato in più elementi dell’interfaccia utente, inclusi Ricerca per data e interfacce non standard. (SITES-31822)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp1}

AEM ora evita il deterioramento delle prestazioni causato da metadati XMP non validi nelle risorse immagine. Assets che contiene nomi di proprietà XMP non validi o non conformi, ad esempio quelli con segmenti numerici o strutture non qualificate, non attiva più i registri di avviso ripetuti durante l’elaborazione. Il sistema filtra i metadati problematici per garantire che l’inserimento e la convalida delle risorse siano completati senza errori. (SITES-30683)

<!--
#### [!DNL Content Fragments] - Admin{#sites-admin-65-lts-sp1} -->

#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-65-lts-sp1}

Altri autori possono comunque pubblicare frammenti di contenuto anche quando un altro autore li estrae, il che è contrario al comportamento previsto della funzione di estrazione. Questa correzione impedisce ad altri utenti di visualizzare o utilizzare i pulsanti di pubblicazione nell’interfaccia di authoring quando viene estratto un frammento di contenuto. (SITES-30578)

<!--
#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp1}

#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp1}

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp1} -->

#### Console Componenti{#sites-component-console-65-lts-sp1}

È stato risolto un problema nel componente Elenco prodotti a causa del quale la casella di controllo &quot;Seleziona tutti&quot; aggiungeva solo i primi 20 SKU dalla pagina iniziale invece di tutti gli SKU nei risultati della ricerca. (SITES-29191)

#### Back-end core{#sites-core-backend-65-lts-sp1}

I metadati di XMP formattati in modo non corretto hanno generato un errore durante l&#39;elaborazione delle risorse immagine in `ValidationDataServlet`. La correzione assicura la gestione dei metadati conforme ed evita l’analisi ridondante di proprietà non valide. (SITE-30683)

<!--
#### Core Components{#sites-core-components-65-lts-sp1}

#### Campaign integration{#sites-campaign-integration-65-lts-sp1}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp1}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp1}

#### Launches{#sites-launches-65-lts-sp1}

#### Link Checker{#sites-link-checker-65-lts-sp1} -->

#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp1}

* È stato corretto un errore JavaScript `ns.ui.alert is not a function` che si verificava durante la riattivazione dell&#39;ereditarietà del componente fantasma in AEM 6.5 On-Prem. (SITES-31993)
* È stato risolto un problema a causa del quale l’opzione Rollout &quot;Più tardi&quot; consentiva di continuare senza selezionare una data in AEM 6.5. (SITES-31374)

#### Editor pagina{#sites-pageeditor-65-lts-sp1}

* È stato risolto un problema nel modale Teaser a causa del quale la scheda Collegamento e azioni continuava a visualizzare lo stile degli errori, le icone e l’attributo aria-invalid dopo l’immissione dei dati validi e la risoluzione degli errori. (SITES-25527)
* È stato risolto un problema nell’editor di testo modale Teaser a causa del quale i pulsanti Elenchi e Paragrafi non trasmettevano il loro stato espanso o compresso agli assistenti vocali, garantendo accurati aggiornamenti degli attributi aria-espansi. (SITES-25365)
* È stato risolto un problema nella barra degli strumenti Demografia a causa del quale la regolazione del cursore del carrello con l’input della tastiera spostava lo stato attivo sul pulsante Carrello invece di mantenere lo stato attivo sul cursore, migliorando l’efficienza della navigazione per gli utenti che utilizzano la tastiera. (SITES-25324)
* È stato aggiunto un nome accessibile al cursore del carrello nella barra degli strumenti Demografia assegnando un valore all&#39;elemento `<label>` associato. Questa correzione ha migliorato la compatibilità con le tecnologie per l’accessibilità e l’usabilità per gli utenti di utilità per la lettura dello schermo. (SITES-25322)
* Sono stati aggiunti i ruoli ARIA e i nomi accessibili ai pulsanti nel menu a discesa della barra degli strumenti Demografia. Questa correzione ha consentito una corretta identificazione tramite tecnologie per l’accessibilità e una migliore navigazione per gli utenti che utilizzano tastiera e utilità per la lettura dello schermo. (SITES-25315)
* È stato corretto il layout della barra degli strumenti demografica per impedire l’overflow del contenuto oltre il riquadro di visualizzazione con uno zoom del browser del 200%, garantendo che tutti i controlli rimangano accessibili senza scorrimento orizzontale. (SITES-25309)
* È stata corretta la gestione dello stato attivo nella barra degli strumenti Demografica per mantenere lo stato attivo sulla tastiera del pulsante attivato invece di reimpostare lo stato attivo sulla posizione iniziale della barra degli strumenti. (SITES-25306)
* L’etichetta del pulsante si sovrappone come previsto, utilizzando una descrizione per visualizzare l’etichetta quando sono attive modalità con larghezze di schermo simili. (SITES-25285)
* La finestra modale per l’annotazione include un pulsante di invio visibile che consente agli utenti di inviare le annotazioni senza utilizzare il tasto Esc o senza fare clic all’esterno del modale. (SITES-25281)
* La finestra modale per l’annotazione include un pulsante con icona a forma di penna che consente agli utenti di inviare annotazioni, fornendo un metodo di invio chiaro e accessibile. (SITES-25269)
* Sono stati corretti gli annunci degli assistenti vocali relativi ai pulsanti Annota e Chiudi annotazione per fornire un feedback accurato e pertinente e rimuovere informazioni non correlate o confuse. (SITES-25268)
* Le sezioni Canvas nelle pagine dell’Editor di AEM ora supportano l’accessibilità completa da tastiera. Gli utenti possono attivare i titoli delle sezioni e i pulsanti di modifica utilizzando solo la tastiera, senza dover passare con il mouse. Questo aggiornamento garantisce la conformità a WCAG 2.1.1 e migliora l’usabilità tra i componenti (come moduli Teaser, Immagine, Carosello, Layout, Timewarp e Annotation). (SITES-25256)
* È stato rimosso l’inutile scorrimento orizzontale nel modale Carosello a una larghezza di 320 px per garantire che tutto il contenuto venga visualizzato nella finestra della vista senza richiedere la navigazione laterale. (SITES-25254)
* È stato rimosso l’inutile scorrimento orizzontale nella finestra modale Immagine a una larghezza di 320 px per garantire che tutto il contenuto venga visualizzato nella finestra della vista senza richiedere la navigazione laterale. (SITES-25244)
* È stato rimosso l’inutile scorrimento orizzontale nel modale Teaser a una larghezza di 320 px per garantire che tutti i contenuti vengano visualizzati nella finestra della vista senza richiedere la navigazione laterale. (SITES-25242)
* Attivazione della navigazione tramite tastiera per il menu a comparsa `List` e `Paragraph Format`, entrambi nel modale Teaser. Questa correzione consente agli utenti di accedere e navigare in questi menu utilizzando i tasti freccia. (SITES-25235)
* Sono stati corretti gli annunci degli assistenti vocali relativi ai pulsanti Annota e Chiudi annotazione per fornire un feedback preciso e pertinente in linea con le azioni associate. (SITES-25234)
* È stata migliorata l’etichetta del pulsante Aiuto nel modale Teaser per descriverne chiaramente lo scopo e fornire un contesto significativo per tutti gli utenti, compresi gli utenti di tecnologie per l’accessibilità. (SITES-25224)
* È stato migliorato il righello dell’emulatore per gli utenti di utilità di lettura dello schermo associando le misurazioni dei righelli ai rispettivi dispositivi. Inoltre, sostituendo la descrizione con un elemento aria-descritto da. (SITES-24955)
* Non è stata implementata alcuna correzione perché il pulsante Modifica funziona come previsto e fornisce contesto informativo anziché eseguire un&#39;azione. (SITES-24950)
* L&#39;ordine di attivazione confermato nella pagina dell&#39;editor segue una sequenza logica che consente agli utenti di spostarsi tra tutti gli elementi interattivi senza saltare o tornare indietro in modo imprevisto. (SITES-24937)
* L&#39;area di lavoro in modalità Anteprima confermata aggiorna correttamente la spaziatura del testo quando gli utenti applicano impostazioni di spaziatura personalizzate, garantendo una formattazione coerente in tutte le aree di contenuto. (SITES-24936)
* Il pulsante Anteprima verificata non attiva più le modifiche di contesto o stato nello stato attivo, garantendo agli utenti di attivarlo intenzionalmente prima che la visualizzazione della pagina venga aggiornata. (SITES-24784)
* Ai collegamenti di navigazione dell’app sono state aggiunte le assegnazioni corrette del ruolo ARIA, che consentono agli assistenti vocali di identificare con precisione gli elementi desiderati e di annunciarne gli elementi per migliorarne l’accessibilità. (SITES-24718)
* Il pulsante Change Filters è stato aggiornato per annunciare gli stati espansi e compressi per gli assistenti vocali, rimuovere gli attributi ARIA ridondanti e regolare l’etichettatura per fornire descrizioni chiare e non duplicanti. (SITES-24713)
* Nella finestra di dialogo per la selezione dei collegamenti sono stati aggiunti annunci di utilità di lettura dello schermo per i messaggi di stato dei risultati di ricerca, in modo che gli utenti ricevano una conferma al caricamento dei risultati o quando non vengono trovate corrispondenze. (SITES-24700)
* Sono stati aggiunti annunci di utilità di lettura dello schermo per lo stato di caricamento del modale Immagine, in modo che gli utenti ricevano un feedback durante il caricamento del modale e siano pronti per l’interazione. (SITES-24697)
* È stato risolto un problema di accessibilità a causa del quale l’intestazione fissa oscurava il contenuto modale di Teaser con uno zoom del 200% e del 400%, garantendo piena visibilità e usabilità quando si utilizzava l’ingrandimento della pagina. (SITES-24523)
* È stato aggiunto al campo Ricerca/filtro un messaggio di stato con il numero di risultati di ricerca, per consentire agli assistenti vocali di annunciare i risultati agli utenti. (SITES-24506)
* Sono stati aggiunti annunci di utilità di lettura dello schermo per il numero di risultati di ricerca nel campo Ricerca/Filtro, in modo che gli utenti ricevano un feedback immediato al caricamento dei risultati. (SITES-24505)
* È stato aggiunto un nome accessibile all’elenco di schede nel pannello della barra laterale, consentendo agli assistenti vocali di annunciarne lo scopo in conformità alle linee guida WAI-ARIA. (SITES-24492)
* Sono state aggiunte etichette descrittive alle icone dell’editor ambigue, in modo che tutti gli utenti comprendano chiaramente la funzione di ciascun pulsante. (SITES-24480)
* È stata abilitata l’accessibilità completa da tastiera per i titoli delle sezioni e i pulsanti di azione nella vista Area di lavoro, garantendo un funzionamento coerente per gli utenti di mouse e tastiera. (SITES-24479)

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

Sono stati risolti i cicli di dipendenza OSGi che impedivano il funzionamento della factory del motore di script HTL, garantendo una risoluzione del servizio e l’esecuzione dello script corrette. (Granite-58275)

#### Integrazioni{#foundation-integrations-65-lts-sp1}

* È stato rimosso l&#39;utilizzo di commons-httpclient 3.x dal bundle `com.adobe.cq.cq-analytics-integration` e sostituito con `org.apache.httpcomponents.httpclient` 4.5.13.B0001 per allinearlo ai più recenti standard AEM 6.5 LTS. (CQ-4360586)
* È stato rimosso il bundle di integrazione Search&amp;Promote obsoleto da AEM per eliminare i componenti inutilizzati e ridurre il sovraccarico di manutenzione. (CQ-4358030)
* Sono stati aggiunti nuovi casi di test back-end per l’integrazione SiteCatalyst per migliorare la convalida delle analisi e garantire una copertura più completa. (CQ-4359991)
* È stato risolto un problema nella sezione Proprietà della configurazione di Launch a causa del quale i menu a discesa Società e Proprietà non venivano visualizzati. Inoltre, Salva e chiudi hanno attivato errori nonostante tutti i campi obbligatori fossero compilati e messaggi di errore non corretti venivano visualizzati per Azienda e Proprietà quando solo il campo Titolo era vuoto. (CQ-4359853)
* È stata rimossa la voce del percorso del servlet `searchpromote` dalla versione 6.6 per allinearla alla rimozione del bundle Search&amp;Promote. (CQ-4359523)
* Sono stati corretti alcuni casi di test HTTP per l’archivio Target, al fine di garantire una convalida accurata e una maggiore affidabilità dei test. (CQ-4359022)
* È stato rimosso l’utilizzo del caching Guava dal modulo integration-adobeims-console per eliminare le dipendenze della libreria Guava. (CQ-4358710)
* Flussi di lavoro di integrazione di DTM convalidati, attività casella in entrata e funzionalità di progetto in AEM 6.6 per garantire il corretto funzionamento in AEM 6.5. (CQ-4358151)
* Funzionalità Insight del contenuto convalidata in AEM 6.6 per garantire la compatibilità e il corretto funzionamento in AEM 6.5. (CQ-4357774)
* Funzionalità Cloud Services convalidata in AEM 6.6 per garantire la compatibilità e il corretto funzionamento in AEM 6.5. (CQ-4357773)
* Integrazione convalidata della console Adobe IMS in AEM 6.6 per garantire la compatibilità e il corretto funzionamento in AEM 6.5. (CQ-4357772)
* È stata aggiornata la pipeline Jenkins per l’integrazione Test&amp;Target da eseguire su Java 17, risolvere gli errori dei test Selenium, spostare alcuni test su Playwright e garantire il superamento di tutti gli unit test. (CQ-4357770)
* Sono state allineate le integrazioni DX, il flusso di lavoro, la casella in entrata e i progetti con il ramo 6.6.0 aggiornando le pipeline di build e test. Risoluzione dei problemi di compatibilità dell&#39;aggiornamento e convalida di tutti i servizi interessati per la stabilità e la funzionalità. (CQ-4357767)

<!--
#### Jetty{#foundation-jetty-65-lts-sp1} -->

#### Localizzazione{#foundation-localization-65-lts-sp1}

* Le stringhe nella finestra di dialogo Rimuovi controllo di accesso dall&#39;elenco Autorizzazioni sono state localizzate per visualizzare le traduzioni corrette. (GRANITE-59427)
* È stato risolto un problema nella finestra di dialogo Aggiungi regola dell’Editor modelli &quot;Proprietà suddivise o&quot; a causa del quale più stringhe di interfaccia utente, inclusi operatori ed etichette di campo, venivano visualizzate non localizzate. Tutte le stringhe vengono ora visualizzate con la localizzazione corretta. (CQ-4354014)
* È stata aggiunta la traduzione mancante per la descrizione &quot;Mostra descrizione per&quot; nella finestra di dialogo Modifica modelli flusso di lavoro. (CQ-4347996)

#### Oak {#foundation-oak-65-lts-sp1}

È stato risolto un problema a causa del quale AEM ricreava o rinominava i file di configurazione esistenti in `/apps/system/config` durante gli aggiornamenti, sostituendo `.cfg.json` file con `.config` file. (GRANITE-58899)

#### Omnisearch{#foundation-omnisearch-65-lts-sp1}

È stato risolto un problema di accessibilità a causa del quale i segnaposto venivano erroneamente visualizzati come etichette per i campi di input. Questo problema causa la mancanza di etichette dei campi in Ricerca, Frammenti esperienza AEM, Frammenti di contenuto e Modelli per frammenti di contenuto. (Granite-61791)

<!--
#### Platform{#foundation-platform-65-lts-sp1} -->

#### Progetti{#foundation-projects-65-lts-sp1}

* È stato risolto un problema che causava la visualizzazione di un pop-up di errore non corretto durante l’eliminazione di un progetto nella vista Calendario, nonostante l’eliminazione del progetto avesse esito positivo. (CQ-4358890)
* È stato risolto un problema in Firefox a causa del quale il piè di pagina della scheda &quot;Asset Collection&quot; nella vista Progetto si sovrapponeva al bordo della scheda. Il piè di pagina ora viene allineato correttamente senza sovrapposizioni. (CQ-4353317)

#### Quickstart{#foundation-quickstart-65-lts-sp1}

* È stato aggiornato lo script di disinstallazione per regolare l’intervallo di versioni per il bundle Guava, impedendo l’attivazione di tale script quando viene installato tramite Gestione pacchetti. Il bundle Guava non può essere installato in modo da poter essere inserito nell&#39;elenco Bloccati in modo da poter essere utilizzato in qualsiasi momento durante l’installazione del bundle stesso. (GRANITE-59559)
* È stato risolto un errore di configurazione in più parti che si verificava durante il caricamento di pacchetti AEMFD su Tomcat 11 con JDK 17 aggiornando la configurazione del server per supportare installazioni di pacchetti di grandi dimensioni senza attivare errori di analisi. (GRANITE-58327)
* È stato risolto un problema nell&#39;interfaccia utente di replica a causa del quale veniva visualizzato un errore (`#1660`) durante la modifica degli agenti di replica correggendo la gestione delle caselle di controllo classiche nell&#39;interfaccia. (GRANITE-58302)
* Sono stati risolti diversi errori di avvio per l’archivio dati S3 durante l’esecuzione di AEM 6.5 LTS con JDK 21, risolvendo il problema delle autorizzazioni di servizio mancanti, aggiornando la gestione della configurazione e garantendo la corretta inizializzazione dei servizi richiesti. (GRANITE-57082)
* Definita la strategia di manutenzione e mantenimento per AEM 6.5. Questa correzione includeva quanto segue:
   * Cadenza Service Pack.
   * Frequenza hotfix.
   * Supporto parallelo con AEM 6.6.
   * Matrice di supporto aggiornata.
   * Responsabilità di proprietà del componente aggiuntivo. (GRANITE-50459)

<!--
#### Security{#foundation-security-65-lts-sp1} -->

#### Sling{#foundation-sling-65-lts-sp1}

* Aggiornamento di Sling ResourceAccessSecurity alla versione 1.1.2 per risolvere un `ClassCastException` che si è verificato quando più riferimenti `ResourceAccessGate` hanno inizializzato `ResourceAccessSecurityImpl`. (NPR-42750)
* È stato risolto un problema nell’integrazione di Adobe Stock a causa del quale la finestra di dialogo Licenza appariva in grigio. Questo problema era dovuto alla rimozione dei campi di input richiesti dalla funzione `sunt:initList`. La funzione è stata trovata nelle librerie client di Coral Foundation. Sono state aggiornate le librerie client per mantenere i campi necessari, abilitando la funzionalità appropriata della finestra di dialogo delle licenze. (NPR-42748)
* È stato eseguito il backport della correzione per il problema di script Sling che ha causato `DataTimeParseException` e `String.length()` eccezioni Null Pointer durante l&#39;installazione del pacchetto. Aggiornamento dello script Sling alla versione 2.8.3-1.0.10.6 per ridurre gli errori di installazione e migliorare la stabilità. (NPR-42640)

<!--
#### Translation{#foundation-translation-65-lts-sp1} -->

#### Interfaccia utente{#foundation-ui-65-lts-sp1}

* È stato risolto un problema nell’interfaccia utente di AEM Author che limitava la visualizzazione dei gruppi di utenti a 41. Questo problema era dovuto a un limite batch predefinito nel componente di selezione del gruppo dell’interfaccia utente Granite. Il componente è stato aggiornato per visualizzare tutti i gruppi senza troncamento. (NPR-42749)
* È stato risolto un problema nella procedura guidata per la creazione di pagine locali, a causa del quale i campi obbligatori nei componenti con più campi non venivano riconvalidati durante la modifica delle proprietà della pagina. Questo problema, a sua volta, consentiva agli autori di ignorare la convalida e procedere con dati incompleti. (GRANITE-58826)
* Sono stati corretti gli attributi ARIA per il pulsante Aiuto in AEM per garantire che gli assistenti vocali JAWS visualizzino un’etichetta chiara e intuitiva invece di visualizzare l’icona non tradotta e i metadati di testo. (GRANITE-55360)

#### WCM{#foundation-wcm-65-lts-sp1}

* È stato aggiunto il supporto Java 17 per le traduzioni AEM aggiornando i bundle di traduzione, verificando la compatibilità dei pacchetti Java, rimuovendo le dipendenze obsolete e garantendo la piena funzionalità tramite test completi. (CQ-4357525)
* È stato rimosso il test Evergreen `com.adobe.cq.platform.it.http.workflow.inbox.InboxOnOffTimeIT.testActivateLater` per evitare falsi errori durante il test automatico. (CQ-4298376)

#### Flusso di lavoro{#foundation-workflow-65-lts-sp1}

* È stato aggiunto l’attributo `data-detailsurl` mancante negli elementi della casella in entrata per impedire la visualizzazione di valori non definiti negli URL quando si utilizza AEM 6.5 LTS con Java 21. (GRANITE-60158)
* È stata corretta un&#39;eccezione NullPointerException nel metodo `deactivate` del bundle `WorkflowToPublishEventService` durante l&#39;esecuzione di AEM 6.5 LTS con Java 21, garantendo l&#39;arresto corretto del servizio del flusso di lavoro senza errori. (GRANITE-58151)
* L’indice del flusso di lavoro è stato aggiornato per supportare la condivisione, la personalizzazione fuori sede e la risoluzione dei problemi di query della timeline. (GRANITE-52640)
* L’indice del flusso di lavoro è stato aggiornato per supportare la condivisione, le funzioni di personalizzazione out-of-office e la risoluzione dei problemi di query della timeline. (GRANITE-52294)
* Sono stati risolti un numero maggiore di errori di registro durante la convalida del confronto dei registri per un aggiornamento del programma ad AEM versione 10912, garantendo un’esecuzione stabile del flusso di lavoro. (GRANITE-44268)
* È stato aggiornato il metodo di bonifica URL nei repository dei flussi di lavoro per sostituire `url.searchParams` con `url.search`, migliorando la protezione XSS per gli URL vulnerabili. (CQ-4359585)
* Sono state convalidate le funzionalità di flusso di lavoro, casella in entrata e progetti in AEM 6.6 Forms per garantirne il corretto funzionamento e l’integrazione. (CQ-4358777)
* È stata implementata l’automazione per il rilascio di artefatti di contenuti dei flussi di lavoro tramite Jenkins, consentendo processi di distribuzione semplificati e coerenti in AEM 6.5. (CQ-4358472)
* È stato risolto un problema nel flusso di lavoro Crea attività della casella in entrata a causa del quale, dopo aver fatto clic su Invia, la finestra di dialogo &quot;Aggiungi attività&quot; non si chiudeva a causa di un errore di sintassi JavaScript. (CQ-4355336)
* È stato risolto un problema che impediva il salvataggio della configurazione della visualizzazione Posta in arrivo a causa di una definizione di proprietà mancante per `isEndUserConfigurationEnabled`. (CQ-4287757)




## [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 LTS si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e dell’archivio dei contenuti Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x è utilizzato come motore servlet per Quickstart.

### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituisci i valori predefiniti del GC (catalogo globale) con altri valori. Per ulteriori informazioni, consulta la sezione [Installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuisce gli aggiornamenti di manutenzione Java™ 17 e Java™ 21 per l’utilizzo da parte del cliente nei progetti correlati ad AEM, se non disponibili pubblicamente da Oracle.

### Confezione di Uberjar {#uber-jar-packaging}

* Il pacchetto Uberjar di AEM 6.5 LTS presenta una leggera differenza. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Aggiornamento {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).

## Installare e aggiornare {#install-update}

Per i requisiti di configurazione, consulta [Istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

Per istruzioni dettagliate, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Per le nuove installazioni di AEM 6.5 LTS, le definizioni degli indici devono essere installate separatamente. Per ulteriori informazioni, vedere [questo articolo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, sui [requisiti tecnici AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Si consiglia di utilizzare le versioni Java™ 17/Java™ 21 con AEM 6.5 LTS.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobe rivede continuamente le funzionalità del prodotto per migliorare il valore del cliente modernizzando o sostituendo le funzioni meno recenti. Queste modifiche vengono apportate prestando particolare attenzione alla compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità di Adobe Experience Manager (AEM), si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una specifica funzione diventerà obsoleta. Anche se obsolete, le funzionalità sono ancora disponibili ma non vengono migliorate ulteriormente.
1. La rimozione delle funzionalità obsolete avviene non prima della versione principale successiva. La data effettiva di destinazione per la rimozione è pianificata per essere annunciata in un secondo momento.

Questo processo offre alla clientela almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.


### Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità che Adobe ha dichiarato obsolete in AEM 6.5 LTS. In genere, Adobe depreca le funzioni prima di rimuoverle in una versione futura e fornisce un’alternativa.


Consigliamo alla clientela di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|---|---|---|---|


### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità e le funzioni che sono state rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |



## Problemi noti {#known-issues}

<!-- DO THESE KNOWN ISSUES CARRY OVER EACH RELEASE? THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

### Problema con il bundle dello script JSP in AEM 6.5.21-6.5.23 e AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23 e AEM 6.5 LTS GA vengono forniti con il bundle `org.apache.sling.scripting.jsp:2.6.0`, che contiene un problema noto. Il problema si verifica in genere con un carico elevato quando l’istanza AEM gestisce molte richieste simultanee.

Quando si verifica questo problema, è possibile che nei registri errori venga visualizzata una delle eccezioni seguenti insieme ai riferimenti a `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip).

### Errore di connessione Dispatcher con funzionalità solo SSL {#ssl-only-feature}

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

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 LTS, Service Pack 1:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti web sono disponibili solo per la clientela. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/it/docs/customer-one/using/home).

