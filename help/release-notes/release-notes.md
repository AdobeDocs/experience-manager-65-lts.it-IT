---
title: Note sulla versione corrente per Adobe Experience Manager 6.5 LTS, SP2
description: Informazioni sulla versione corrente di Adobe Experience Manager 6.5 LTS, Service Pack 2.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: f75f02c1e10deb6eef788d6584229c045b88880d
workflow-type: tm+mt
source-wordcount: '6062'
ht-degree: 21%

---

# Note sulla versione corrente per Adobe Experience Manager 6.5 LTS, SP2 {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versione | Service Pack 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 19 febbraio 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione del software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

## Cosa è incluso in [!DNL Adobe Experience Manager] 6.5 LTS, SP2 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP2 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale di 6.5 LTS a marzo 2025. [Installare il Service Pack](#install-update) su 6.5 LTS.

## Caratteristica chiave e miglioramento

**AEM Sites**

AEM 6.5 LTS SP2 ora include OpenAPI per [Gestione di modelli e frammenti di contenuto](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/) e [Lanci](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/). Queste API consentono di accedere a Frammenti di contenuto e avvii per l’authoring e la pianificazione. Utilizzano le stesse OpenAPI moderne di AEM as a Cloud Service.


<!-- UPDATE THE EACH RELEASE -->

## Sono stati risolti i problemi in 6.5 LTS, Service Pack 2 {#fixed-issues}

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-65-LTS-SP2}

#### Accessibilità {#sites-accessibility-65-lts-sp2}

* Il componente Testo non è più attivo quando gli autori passano il cursore sugli elementi nel browser Componenti durante la modifica. Ciò ha interrotto la digitazione e ha provocato un errore di accessibilità in WCAG 3.2.1. La correzione impedisce che lo stile del passaggio del mouse sposti lo stato attivo e mantiene attivo il componente Testo durante l’interazione con il browser componenti. (SITES-35370)
* È stata corretta la gestione dello stato attivo nel campo Testo RTF Descrizione, che bloccava la navigazione in avanti con il tasto TAB. Gli utenti si bloccavano nell’editor Rich Text perché il componente si basava su un comando non standard della tastiera per spostare lo stato attivo, interrompendo la navigazione prevista nella finestra di dialogo. La modifica applica l&#39;interazione standard della tastiera e mantiene la sequenza logica delle schede in tutta la finestra di dialogo. (SITES-35228)
* È stato risolto un problema nell’editor Sites che interrompeva il comportamento previsto durante l’authoring delle pagine e causava un’interazione incoerente dei componenti. Gli autori hanno riscontrato risposte inaffidabili dell’interfaccia utente che hanno interferito con le attività di modifica standard e ridotto l’efficienza del flusso di lavoro. L’aggiornamento perfeziona la logica dell’editor sottostante e ripristina un’interazione stabile e prevedibile tra i componenti interessati. (SITES-35227)
* una regressione che ha interrotto il selettore delle risorse nell’editor pagina e ne ha impedito il caricamento in scenari di modifica specifici della pagina. Gli autori possono ora aprire e utilizzare il selettore delle risorse normalmente durante la scelta o l’esplorazione delle risorse durante la modifica di una pagina. Questa modifica ripristina un accesso coerente ai flussi di lavoro di selezione delle risorse che interrompono il caricamento degli errori. (SITES-35226)
* È stato eliminato un problema nell’editor Sites che causava un comportamento incoerente durante l’interazione delle pagine e interrompeva i flussi di lavoro di authoring standard. Il difetto ha portato a risposte impreviste dell’interfaccia utente che hanno interferito con la configurazione dei componenti e gli aggiornamenti dei contenuti. L’aggiornamento stabilizza la funzionalità interessata e ripristina l’esecuzione affidabile delle azioni di modifica su più pagine. (SITES-35225)
* È stato eliminato un difetto nell’interfaccia di authoring di Sites che causava un comportamento incoerente durante la modifica delle pagine e interrompeva i normali flussi di lavoro. Gli autori hanno riscontrato risposte impreviste dell’interfaccia utente che hanno interferito con l’interazione dei componenti e con gli aggiornamenti dei contenuti. L’aggiornamento stabilizza le funzionalità interessate e ripristina un comportamento affidabile e prevedibile in tutti gli scenari di modifica. (SITES-35224)
* AEM Sites ora include il supporto testuale `alt` per le immagini per soddisfare i requisiti ADA e WCAG. L&#39;output della pagina non omette più gli attributi `alt`, pertanto gli assistenti vocali ricevono il testo alternativo corretto. (SITES-27153)
* È stato corretto il layout della barra degli strumenti `Note Add` in modo che il pulsante Aggiungi non si sovrapponga più al titolo con una larghezza del riquadro di visualizzazione di 320 px. È stato migliorato il riversamento su piccolo schermo in modo che i controlli rimangano leggibili e utilizzabili con uno zoom del 400%. (SITES-25376)
* Sono stati corretti gli annunci mancanti degli assistenti vocali per gli errori della finestra di dialogo di selezione dei collegamenti. L’interfaccia utente ora pubblica il testo dell’errore tramite un contenitore per messaggi di stato, pertanto NVDA legge il messaggio non appena viene visualizzato. (SITES-25368)
* Sono stati rimossi i ruoli griglia ARIA e cella griglia dall’elenco delle risorse nella barra laterale. Sono state ripristinate la semantica standard degli elenchi e l’ordine di attivazione della tastiera, migliorando la navigazione degli assistenti vocali e riducendo le tabulazioni aggiuntive. (SITES-25361)
* È stata corretta la sequenza di attivazione nella barra laterale di Assets. Gli utenti che utilizzano la tastiera ora raggiungono ogni azione della risorsa, inclusa la modifica, tramite un percorso di tabulazione coerente. (SITES-25360)
* È stato corretto l’overflow del layout nel modale Search Assets (Ricerca) con una larghezza del riquadro di visualizzazione di 320 px. Il contenuto modale ora viene ridisposto e rimane leggibile, pertanto i controlli non si sovrappongono più o sovraccaricano la finestra di dialogo. (SITES-25330)
* Output NVDA corretto per il pulsante Modifica. NVDA ora annuncia l&#39;azione Modifica, non &quot;Pulsante Anteprima premuto&quot;. (SITES-25320)
* Sono stati corretti gli input di testo della barra degli strumenti Demografia senza nome che causavano un output di utilità di lettura dello schermo silenzioso o generico. Ogni input ora espone un chiaro nome accessibile basato su etichette, che migliora la navigazione tramite tastiera e tecnologia per l’accessibilità. (SITES-25316)
* È stato corretto l’ordine di attivazione della tastiera per la barra degli strumenti Demografia durante la navigazione nell’anteprima di layout. La navigazione tramite scheda ora si sposta direttamente dal pulsante Demografico ai controlli della barra degli strumenti, senza passare alla barra degli strumenti secondaria. (SITES-25305)
* È stato corretto l’ordine di annuncio errato per le etichette &quot;Screens più piccolo&quot; e &quot;Tablet&quot; sul righello Modifica layout. Gli assistenti vocali ora annunciano queste etichette ai marcatori righello corretti, che corrispondono al layout della pagina. (SITES-25291)
* È stato corretto l’overflow della barra degli strumenti Modifica layout con uno zoom del 200%. Il contenuto ora rimane all’interno del riquadro di visualizzazione e rimane raggiungibile tramite lo scorrimento. (SITES-25288)
* È stato risolto un ordine di attivazione errato nella sovrapposizione Annotazioni. La tabulazione da tastiera ora passa da controlli di sovrapposizione a elementi di annotazione. La pagina padre non si attiva più da dietro la sovrapposizione. (SITES-25282)
* Gestione a comparsa dei campioni corretti. La finestra di dialogo ora sposta lo stato attivo su un&#39;intestazione chiara e avvia l&#39;output dell&#39;utilità di lettura dello schermo in corrispondenza di tale punto di ingresso. NVDA non legge più il contenuto completo della finestra di dialogo fuori sequenza. (SITES-25275)
* È stata corretta la gestione dell’attivazione modale di Timewarp dopo la chiusura del Selettore data. `Escape` ora restituisce lo stato attivo al pulsante Selezione data. La selezione della data ora attiva il campo di input accanto al controllo Selezione data, impedendo la perdita dello stato attivo e l&#39;accesso alla pagina in background. (SITES-25264)
* È stata corretta la gestione dello stato attivo della tastiera per la finestra di dialogo Elimina annotazione. Annulla ora restituisce lo stato attivo al controllo `Delete` che ha aperto la finestra di dialogo, non al controllo Conferma valore esadecimale. Gli assistenti vocali non visualizzano più il contenuto di una finestra di dialogo non correlata dopo l&#39;annullamento. (SITES-25258)
* È stata corretta la gestione dello stato attivo per la finestra di dialogo modale Annotazione. L&#39;apertura della finestra di dialogo ora imposta lo stato attivo sull&#39;intestazione della finestra di dialogo e impedisce a NVDA di leggere il contenuto dell&#39;area di lavoro e il testo della finestra di dialogo non correlato. La navigazione tramite tastiera ora rimane all&#39;interno della finestra di dialogo fino a quando non viene chiusa. (SITES-25257)
* Sono stati risolti i problemi di layout modale di ricerca a 320 px di larghezza. Il contenuto modale ora scorre in modo pulito ed evita la sovrapposizione con la directory della struttura. Gli utenti possono visualizzare i risultati e navigare nella directory senza controlli oscurati. (SITES-25246)
* Il testo modale di ricerca non viene più ritagliato dopo l&#39;aumento della spaziatura. Il layout della directory ad albero mantiene ora una separazione netta, in modo che le etichette e le voci rimangano leggibili. Gli utenti possono ora completare la ricerca e la navigazione senza sovrapporsi o separare il testo. (SITES-25245)
* L’attivazione di Annota consente ora di spostare lo stato attivo della tastiera sul contenuto dell’annotazione, non sul pulsante Esci dall’annotazione. L&#39;ordine di tabulazione segue una sequenza logica e consente di mantenere i controlli correlati raggiungibili senza spostamenti all&#39;indietro. (SITES-25241)
* Nei collegamenti Date (Data) e Exit Timewarp (Esci) manca un indicatore visibile dello stato attivo durante la navigazione da tastiera. L’interfaccia utente ora esegue il rendering di uno stile di attivazione a contrasto elevato distinto in modo che gli utenti possano identificare immediatamente il collegamento attivo. (SITES-25232)
* L’intestazione modale Teaser non impedisce più agli utenti che utilizzano la tastiera di spostare la finestra di dialogo. I controlli da tastiera consentono ora le azioni di ritiro, spostamento e rilascio, che migliorano l&#39;usabilità dello screen reader e l&#39;operabilità complessiva. (SITES-25226)
* AEM ora utilizza un’etichetta accessibile significativa per il pulsante Informazioni modali del teaser. Gli assistenti vocali annunciano un nome chiaro per l’azione invece della stringa di testo alternativo predefinita per l’icona. (SITES-25223)
* Gli assistenti vocali ora annunciano l’azione corretta quando gli utenti attivano il pulsante Modifica. NVDA non segnala più &quot;Pulsante Anteprima premuto&quot;, che ha causato feedback fuorvianti e confusione durante la navigazione da tastiera. (SITES-25208)
* L&#39;espansione della barra a sinistra ora sposta la tastiera sul primo controllo della barra a sinistra. La sequenza Tab non passa più alla barra degli strumenti secondaria né arriva all’elenco intermedio, pertanto gli utenti con tastiera possono raggiungere il contenuto della barra a sinistra senza ricorrere alla navigazione inversa. (SITES-24998)
* Il contenuto della barra dell’emulatore del dispositivo ora rimane completamente visibile con una larghezza del riquadro di visualizzazione di 320 px. Il testo della barra degli strumenti e i controlli vengono disposti a capo anziché troncati, riducendo la sovrapposizione e migliorando la leggibilità. (SITES-24953)
* AEM ora visualizza l’etichetta completa del dispositivo iPhone nella barra degli strumenti dell’emulatore. Il testo non viene più troncato alla larghezza predefinita, migliorando la leggibilità e la chiarezza della selezione del dispositivo. (SITES-24952)
* Le intestazioni della tabella Vista a elenco ora espongono lo stato di ordinamento tramite ARIA. Gli assistenti vocali annunciano un ordine crescente o decrescente dopo un’azione di ordinamento delle colonne. (SITES-24943)
* AEM ora mantiene la visibilità dell’etichetta del menu Altre azioni nella Vista a schede durante le modifiche della spaziatura del testo. Le opzioni di menu mantengono il testo completo, inclusa la pubblicazione rapida, e il menu rimane leggibile durante tutte le impostazioni di spaziatura del testo WCAG. (SITES-24941)
* La barra dei menu Azioni scheda ora espone un nome accessibile in Vista scheda. Gli assistenti vocali annunciano chiaramente lo scopo della barra dei menu e il controllo vocale può impostare il controllo in base al nome. (SITES-24938)
* La vista a schede non si basa più sulla semantica della griglia ARIA, che ha causato confusione nel comportamento degli assistenti vocali. L’interfaccia utente fornisce ora ruoli ed etichette significativi per il contenuto della scheda e la barra delle azioni della scheda, che riduce i controlli mancanti durante l’utilizzo della tastiera. (SITES-24933)
* La descrizione comando `Delete Modal` viene ora visualizzata ogni volta che gli utenti passano il puntatore sull&#39;icona della descrizione. Le azioni di attivazione ora mostrano lo stesso testo della descrizione comando, migliorando l&#39;accesso ripetuto per gli utenti di mouse e tastiera. (SITES-24778)
* La navigazione nella barra a sinistra segue ora l’ordine previsto di attivazione della tastiera dopo la configurazione della barra da parte degli utenti. Lo stato attivo della scheda si trova sull’area della barra a sinistra selezionata invece di Switch Display (Schermo switch), il che migliora la chiarezza della navigazione dell’assistente vocale. (SITES-24754)
* È stato risolto un feedback NVDA errato durante la navigazione dei campioni di colore nella finestra modale Preferenze utente. NVDA ora legge l’etichetta del campione che riceve lo stato attivo, rimuovendo l’output di colore fuorviante. Il set di campioni ora supporta una navigazione coerente da tastiera e il riconoscimento della selezione. (SITES-24739)
* Output NVDA dettagliato ridotto per il controllo `Spin`. È stata rimossa l’etichettatura di gruppo ridondante che duplicava l’etichetta di input, pertanto NVDA annuncia una volta il nome del controllo. La navigazione tramite tastiera e utilità di lettura dello schermo ora offre un annuncio singolo e chiaro. (SITES-24725)
* La finestra di dialogo Carosello ora posiziona lo stato attivo sull&#39;intestazione della finestra di dialogo anziché sulla scheda Elementi. Annulla ed Esc ripristinano lo stato attivo sul controllo che ha avviato la finestra di dialogo, riducendo l’output NVDA dettagliato. (SITES-24716)
* La finestra di dialogo per la selezione dei collegamenti ora allinea l’etichetta programmatica con l’etichetta visualizzata sullo schermo per gli elementi dell’albero di ultimo livello. La navigazione con tasti di direzione attiva un annuncio affidabile sull’utilità di lettura dello schermo per ogni elemento e rimuove l’output di etichette fuorvianti. (SITES-24710)
* La finestra di dialogo Collega selezione aperta ora scorre correttamente sotto un riquadro di visualizzazione a 320 px. Il contenuto non supera più il modale o i tronchi e il modale non mostra più una barra di scorrimento orizzontale. (SITES-24709)
* La finestra di dialogo Collega selezione aperta ora ripristina lo stato attivo della tastiera sull&#39;attivatore della finestra di dialogo dopo Chiudi o Annulla. La messa a fuoco non passa più all&#39;input Link, che mantiene stabile il contesto dell&#39;utilità di lettura dello schermo e riduce la navigazione aggiuntiva. (SITES-24707)
* La finestra di dialogo modale dell’immagine ora segue una sequenza logica di attivazione. Lo stato attivo non ignora più i controlli precedenti o i rilasci sul punto di riferimento della pagina dopo l’annullamento e gli utenti riprendono a utilizzare il pulsante Configura dopo l’uscita. (SITES-24693)
* La finestra di dialogo modale Barra dei riferimenti ora registra lo stato attivo della tastiera. Tab e Maiusc+Tab rimangono all&#39;interno dei controlli della finestra di dialogo e lo stato attivo non passa più al contenuto della pagina. Gli assistenti vocali annunciano solo il contenuto della finestra di dialogo. (SITES-24683)
* La finestra modale Selezione percorso collegamento ipertestuale ora imposta lo stato attivo sull’intestazione della finestra di dialogo all’apertura. Annulla chiude la finestra di dialogo e ripristina lo stato attivo sul pulsante Apri finestra di dialogo di selezione, impedendo la perdita della messa a fuoco e l&#39;output ridondante dell&#39;utilità per la lettura dello schermo. (SITES-24672)
* Il campo Ricerca ora utilizza un’etichetta persistente sullo schermo invece del testo segnaposto. L&#39;etichetta rimane visibile durante l&#39;immissione, migliorando la chiarezza per gli utenti di tastiera, utilità di lettura dello schermo e riconoscimento vocale. (SITES-24529)
* La finestra di dialogo modale teaser ora imposta lo stato attivo sull’intestazione della finestra di dialogo all’apertura. La chiusura della finestra di dialogo riporta lo stato attivo sul controllo `Configure`, impedendo la perdita della messa a fuoco e l&#39;eccessivo output dell&#39;utilità di lettura dello schermo. (SITES-24522)
* Il pannello Assets della barra laterale ora include un controllo Chiudi. Chiudi riporta lo stato attivo della tastiera sull’interruttore della barra laterale e impedisce la tabulazione forzata attraverso il contenuto del pannello. (SITES-24489)
* La tabulazione da tastiera ora raggiunge i pulsanti e i collegamenti all’interno delle tabelle di amministrazione. Gli utenti non si affidano più alla navigazione tramite celle con tasti di direzione per trovare i controlli interattivi. (SITES-24285)
* La finestra di dialogo del componente Immagine non espone più icone decorative della Guida e a schermo intero come immagini. Gli assistenti vocali ora ignorano queste icone, mantenendo lo stato attivo sui controlli utilizzabili e sul contenuto dei campi. (SITES-2940)
* L’amministratore Sites ora rimuove il ruolo immagine dalle icone delle miniature delle cartelle. La tecnologia assistiva ignora questi elementi decorativi, mantenendo l’attenzione sui nomi delle cartelle e sulle azioni. (SITES-2852)
* Struttura contenuto ora indirizza lo stato attivo della tastiera all&#39;elemento della struttura attivo o al primo elemento della struttura. Il contenitore ad albero non funge più da punto di tabulazione vuoto, impedendo le trap di Maiusc+Tab focus. (SITES-1577)

#### Interfaccia utente amministratore{#sites-adminui-65-lts-sp2}

Le impostazioni della Vista a elenco della console Sites non riflettevano le colonne visualizzate nella Vista a elenco. La finestra di dialogo si apriva con le caselle di controllo deselezionate e un conteggio errato delle colonne selezionate. Lo stato della finestra di dialogo Correggi sincronizza con le colonne della griglia attive e aggiorna il contatore in modo che corrisponda alla visibilità effettiva delle colonne. (SITES-38576)

#### Interfaccia utente classica{#sites-classicui-65-lts-sp2}

Dopo un aggiornamento, nella modifica del componente testo dell’interfaccia classica venivano visualizzati dei tag HTML non formattati, ma non testo formattato. Service Pack 2 corregge il rendering dell’editor Rich Text dell’interfaccia classica in modo che l’editor visualizzi il contenuto formattato e conservi il markup memorizzato. La correzione interrompe anche l’espansione del markup durante le modifiche e i salvataggi ripetuti. (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

In 6.5 LTS, il supporto per gli eventi headless non disponeva degli eventi OSGi richiesti per frammenti di contenuto e modelli. L&#39;aggiornamento aggiunge il bundle di eventi più le dipendenze richieste e include una build LTS 6.5. Gli eventi Modello e Frammento di contenuto ora vengono attivati correttamente e supportano i flussi di lavoro API Launches. (SITES-35329)

#### [!DNL Content Fragments] - Amministratore{#sites-admin-65-lts-sp2}

* È stata modificata la gestione dei componenti nell’interfaccia di authoring di Sites per interrompere il comportamento irregolare durante gli aggiornamenti delle pagine. Il difetto ha portato a risposte imprevedibili dell’editor che hanno interferito con le modifiche di routine dei contenuti e ridotto l’efficienza del flusso di lavoro. L’aggiornamento allinea la logica dell’editor ai modelli di interazione previsti e offre prestazioni affidabili durante le attività di authoring. (SITES-35078) CRITICO

* Una regressione ha interrotto la Vista a elenco della console Assets per i frammenti di contenuto e ha attivato un errore durante il rendering dell’elenco. L’aggiornamento corregge la logica della vista a elenco dopo la rimozione delle informazioni di anteprima e ripristina l’output stabile dell’elenco. La console ora visualizza i Frammenti di contenuto senza errori e mantiene utilizzabili le interazioni elenco. (SITES-38683)
* L’Editor frammento di contenuto ora localizza l’etichetta Tag. L’editor localizza anche l’etichetta Raccolte, in modo che il testo dell’interfaccia utente corrisponda alle impostazioni internazionali selezionate. (SITES-977)


#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-65-lts-sp2}

* I tag di variante dei frammenti di contenuto scomparivano quando l’attivazione della funzione rimaneva disabilitata dopo il refactoring. La correzione ripristina il supporto dei tag di variante anche quando questo interruttore rimane disattivato. Gli autori possono nuovamente aggiungere e visualizzare tag di varianti nell’Editor frammento di contenuto. (SITES-38682) CRITICO
* I frammenti di contenuto modificati sono scomparsi dall’elenco della console Assets dopo che gli autori sono tornati dall’Editor frammenti di contenuto. La memorizzazione nella cache del browser ha restituito un elenco non aggiornato e ha nascosto il frammento aggiornato fino a un aggiornamento manuale. La correzione aggiunge la gestione del controllo cache per il percorso di ritorno dell’editor in modo che l’elenco venga ricaricato correttamente e che il frammento modificato rimanga visibile. (SITES-35374) CRITICO

* L’Editor Rich Text per frammenti di contenuto mostrava problemi di layout e di visualizzazione dopo recenti modifiche di stile dell’interfaccia utente. Service Pack 2 ottimizza lo stile dell’editor Rich Text in modo che la barra degli strumenti e l’area modificabile vengano riprodotte correttamente e rimangano leggibili. L’Editor frammento di contenuto ora è allineato con l’aspetto e il comportamento dell’Editor pagina. (SITES-38684)
* La rimozione degli ambiti IMS da Polaris Asset Selector ha interrotto l’integrazione del frammento di contenuto con l’endpoint di consegna. Gli autori riscontrano degli errori quando apri il selettore di risorse remoto e selezioni le risorse. L’aggiornamento aggiunge nuovamente gli ambiti IMS necessari e ripristina l’accesso stabile a livello di consegna. (SITES-35837)
* Il pannello Contenuto associato non esegue più il rendering di un segnaposto codificato &quot;non definito&quot;. L’Editor frammento di contenuto ora risolve il testo tramite le risorse di localizzazione, in modo che gli editor possano vedere il testo tradotto dell’interfaccia utente. (SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* L’Editor frammento di contenuto ora visualizza un’etichetta della scheda Generale tradotta per tutte le lingue. L’editor sostituisce il testo di scheda non localizzato e rimuove gli ID interni dai titoli delle schede. (SITES-30715)
* L’Editor frammento di contenuto ora visualizza i nomi tradotti per i tipi di risorse consentiti. L’elenco selettore non combina più stringhe interne ed etichette solo in inglese quando gli autori configurano le restrizioni relative ai riferimenti ai contenuti. (SITES-29699)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-65-lts-sp2}

* È stata perfezionata la gestione della convalida delle query GraphQL per arrestare gli errori di distribuzione causati da errori di esecuzione dei filtri. Il difetto ha generato eccezioni durante l’avvio dell’applicazione e ha bloccato il rollout riuscito negli ambienti interessati. La revisione garantisce un comportamento di convalida coerente e consente una distribuzione fluida senza interruzioni della convalida delle query di runtime. (SITES-34301) CRITICO

* La finestra di dialogo Modifica endpoint GraphQL ora visualizza stringhe localizzate dell’interfaccia utente. La finestra di dialogo non mostra più il testo solo in inglese, ad esempio &quot;GraphQL schema is take from configuration&quot; (Lo schema di proviene dalla configurazione), e le etichette correlate vengono riprodotte correttamente nelle diverse lingue. (SITES-34018)

#### [!DNL Content Fragments] - Editor query GraphQL{#sites-graphql-query-editor-65-lts-sp2}

* È stata perfezionata la gestione della convalida delle query GraphQL per arrestare gli errori di distribuzione causati da errori di esecuzione dei filtri. Il difetto ha generato eccezioni durante l’avvio dell’applicazione e ha bloccato il rollout riuscito negli ambienti interessati. La revisione garantisce un comportamento di convalida coerente e consente una distribuzione fluida senza interruzioni della convalida delle query di runtime. (SITES-35529)
* Esplora risorse di GraphQL non avrà più esito negativo se il nome di un browser di configurazione contiene caratteri CJK. La creazione degli endpoint e l’accesso alle query salvate funzionano normalmente e la pagina Editor query di GraphQL rimane priva di errori. (SITES-31616)

#### [!DNL Content Fragments] - Editor modelli{#sites-model-editor-65-lts-sp2}

* I modelli per frammenti di contenuto nidificato non funzionavano più quando il refactoring associava la funzione a un interruttore disabilitato. La correzione ripristina il supporto del modello nidificato senza richiedere l’attivazione/disattivazione delle modifiche. Gli autori possono di nuovo creare e utilizzare modelli nidificati nell&#39;Editor modelli. (SITES-38681) CRITICO

* Il pannello dei filtri Modelli per frammenti di contenuto non espone più stringhe non localizzate. AEM ora visualizza le etichette dei filtri localizzati e i valori dello stato localizzato in tutte le lingue. (SITES-30863)
* L’Editor modello per frammenti di contenuto ora esegue il rendering delle stringhe localizzate per la finestra di dialogo di avviso del blocco. L’interfaccia utente sostituisce i messaggi in inglese non localizzati con risorse locali nelle lingue supportate. (SITES-28592)

#### [!DNL Content Fragments] - API REST{#sites-restapi-65-lts-sp2}

AEM Headless richiedeva un ramo della versione dedicato per evitare conflitti di dipendenza e di versione del bundle con le build principali. L’aggiornamento aggiunge un ramo headless versione 6.5lts e allinea i set di dipendenze e le versioni del bundle. Jenkins ora crea la base di codice headless in modo pulito, senza conflitti tra versioni. (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### API contenuto{#sites-content-api-65-lts-sp2}

Un difetto di attivazione della funzione ha segnalato in modo errato lo stato dell’API di gestione pagina. L’aggiornamento aggiunge un flag di abilitazione dedicato e lo valuta insieme all’interruttore esistente. L’API di gestione pagina ora mostra uno stato stabile. L’API di gestione del sito rimane sperimentale. (SITES-39284)

#### Back-end core{#sites-core-backend-65-lts-sp2}

* Una modifica nell’esperienza di authoring di Sites per risolvere comportamenti incoerenti che hanno interrotto i flussi di lavoro di modifica delle pagine standard. Gli autori hanno riscontrato risultati imprevisti durante l’interazione con i componenti, che hanno interferito con gli aggiornamenti dei contenuti e ridotto l’affidabilità. La modifica ripristina un comportamento stabile dell’editor e garantisce l’esecuzione coerente delle azioni di authoring in tutti gli scenari interessati. (SITES-35162) CRITICO

* È stato perfezionato il comportamento di authoring di Sites per risolvere un problema che ha interrotto la modifica della pagina e causato risultati incoerenti durante l’interazione con i componenti. Gli autori hanno riscontrato risposte impreviste dell’interfaccia utente che hanno interferito con gli aggiornamenti dei contenuti e ridotto l’affidabilità del flusso di lavoro. La modifica ripristina una gestione stabile dello stato dell’editor e garantisce l’esecuzione prevedibile delle azioni di authoring negli scenari interessati. (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### Lanci{#sites-launches-65-lts-sp2}

* La timeline dei siti mostrava un testo in inglese hardcoded durante la promozione di Launch: &quot;Creata versione ... prima di promuovere il lancio.&quot; L’aggiornamento sostituisce la stringa hardcoded con la gestione localizzata dei messaggi. La timeline ora visualizza il testo localizzato e allinea la voce con il comportamento di localizzazione standard di AEM. (SITES-39157)
* L’ambito della promozione di Launch si è spostato quando gli autori hanno promosso una sottosezione utilizzando Promuovi pagina corrente e sottopagine. AEM ha inoltre promosso pagine non correlate e causato modifiche live impreviste. La correzione corregge il calcolo dell’ambito di Launch in modo che venga promosso solo il sottoalbero scelto. (SITES-38315)
* I frammenti di contenuto all&#39;interno di Launches non hanno partecipato all&#39;indice `damAssetLucene` e hanno limitato i risultati di ricerca e l&#39;efficienza delle query. Questa modifica aggiunge i percorsi dei frammenti di contenuto di Launch alla definizione dell’indice. Nelle query di ricerca e personalizzate sono ora disponibili frammenti di contenuto in `/content/launches`. (SITES-35634)
* Nell’interfaccia utente Lanci sono stati visualizzati i controlli di lancio per frammenti di contenuto, anche se il prodotto non espone i lanci per frammenti di contenuto nell’interfaccia utente touch. Questa modifica elimina i percorsi del codice di Launch per frammenti di contenuto da cq-launches-content e regola il filtro degli elenchi di Launch. Gli autori ora visualizzano opzioni di lancio pagina coerenti senza voci di lancio per frammenti di contenuto. (SITES-35633)
* In AEM 6.5 LTS Quickstart mancavano i bundle e i prerequisiti Launches richiesti, bloccando l’abilitazione di OpenAPI Launches. L’aggiornamento aggiunge i bundle Launches e le dipendenze richieste, ad esempio il supporto delle metriche, gli aggiornamenti DAM-cfm e la configurazione della coda. Le API Launches ora vengono eseguite su 6.5 LTS Quickstart con i componenti di runtime richiesti presenti. (SITES-35297)
* Il pacchetto CF Launches richiamava versioni di dipendenze più recenti e librerie GraphQL non necessarie, il che ha complicato l’integrazione con AEM 6.5 LTS. Questa modifica allinea le versioni delle dipendenze alla linea di base di AEM 6.5 LTS e elimina le dipendenze GraphQL non utilizzate. La risoluzione del bundle ora rimane coerente e l&#39;avvio di CF Launches rimane stabile. (SITES-35295)
* AEM Launches ora esegue una pipeline Jenkins dedicata per il ramo 6.5 LTS. La pipeline viene eseguita ogni notte per generare e inviare avvisi di errore tramite e-mail. Questa configurazione aumenta la copertura dei test e rileva tempestivamente le regressioni. (SITES-35293)
* AEM 6.5 LTS ora distribuisce un bundle API Launches aggiornato con versioni allineate degli artefatti. Il bundle tiene traccia della riga del codice principale mantenendo la versione corretta della versione 6.5 LTS. Questo aggiornamento stabilizza il consumo dell’API Launches nello stack 6.5 LTS. (SITES-35292)
* AEM 6.5 LTS ora include un bundle launch-core aggiornato con versioni di dipendenza allineate. L’aggiornamento aggiunge la gestione di base Launches per i tipi di dati UUID di frammenti e UUID di riferimento. L’elaborazione dei lanci ora mantiene un comportamento coerente tra i lanci e i flussi di lavoro per frammenti di contenuto. (SITES-35290)
* È stato perfezionato l’editor Sites per risolvere eventuali comportamenti incoerenti che hanno interrotto i normali flussi di lavoro di authoring delle pagine. Gli autori hanno riscontrato un’interazione imprevista tra i componenti che ha interferito con gli aggiornamenti dei contenuti e ha ridotto l’affidabilità delle modifiche. La modifica ripristina una gestione coerente dello stato dell’interfaccia utente e garantisce l’esecuzione prevedibile delle azioni di authoring negli scenari interessati. (SITES-35138)
* Launches Modifica ora mostra il testo dell&#39;errore localizzato invece della stringa hardcoded `Provided path is not a launch`. Ora l’interfaccia utente esegue il rendering dei messaggi tradotti tra le lingue quando Edit riceve un percorso di avvio non valido. (SITES-33360)
* AEM 6.5 LTS ora include il lavoro delle porte laterali OpenAPI Launches. L’aggiornamento porta in parità i bundle API Launches, i pacchetti di contenuti e gli artefatti Quickstart richiesti e abilita gli scenari OpenAPI di Launches di frammenti di contenuto con convalida CI stabile. (SITES-32050)
* L’interfaccia utente Launches ora localizza l’etichetta del modello Sostituito. I dettagli di sostituzione del modello ora visualizzano il testo tradotto invece di una stringa solo in inglese. (SITES-29525)
* AEM ha risolto una chiave di localizzazione mancante in **Sites** > **Launches** > **Edit**. Ora gli utenti visualizzano un messaggio di errore tradotto invece della stringa non elaborata &quot;Impossibile aggiornare l’elenco delle origini del lancio&quot;. (SITES-21499)
* L’interfaccia utente di promozione di Launch ora visualizza le etichette di stato localizzate e le azioni. Nell&#39;area di anteprima viene visualizzato il testo tradotto per **Eliminato**, **Nuovo** e **Visualizza**, anziché le stringhe inglesi non elaborate. (SITES-13540)
* La creazione del lancio ora mostra messaggi di errore localizzati. L&#39;interfaccia utente non visualizza più stringhe inglesi non elaborate, ad esempio `Unable to create launch page`, `Source root resource is not a page` o `Mandatory parameter is missing`. (SITES-13085)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp2}

* Gli amministratori avevano visibilità limitata sull’elaborazione push-on-modify di MSM durante le modifiche al contenuto. La correzione aggiunge una registrazione dettagliata della ricezione e dell’esecuzione del rollout degli eventi MSM. L’output di debug ora mostra quali eventi sono stati attivati, quali percorsi di contenuto sono stati modificati e chi ha attivato la modifica. (SITES-38029)
* AEM ha risolto un problema di layout di localizzazione nel campo data di rollout blueprint. Il prompt della data è ora adatto al controllo e rimane leggibile nelle lingue supportate, incluso `fr_FR`. (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### Replica{#sites-replication-65-lts-sp2}

La pubblicazione dell’Editor pagina ora gestisce gli URL contenenti selettori o suffissi. La richiesta pubblicata ora invia il percorso della pagina JCR, non una stringa URL di selettore o suffisso, quindi l’attivazione viene completata e il contenuto viene attivato. La replica ora restituisce uno stato di errore in caso di errore, che impedisce la visualizzazione di falsi messaggi di &quot;pubblicazione avviata&quot;. (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### Editor modello{#sites-template-editor-65-lts-sp2}

Il testo dello stato del modello viene visualizzato in verticale in **Strumenti** > **Generale** > **Modelli** per alcune impostazioni internazionali. L’etichetta &quot;obsoleto&quot; interrompeva il layout e veniva letta come una colonna di caratteri. La correzione corregge lo stile dello stato del modello in modo che l’etichetta venga riprodotta su una singola linea orizzontale. (SITES-36797)

#### Editor universale {#sites-universal-editor-65-lts-sp2}

* Configurazione predefinita OSGi impostata come `preview=true`. L&#39;editor universale è stato avviato in modalità Anteprima. Questo aggiornamento corregge il valore predefinito e ripristina il comportamento standard della voce Produzione. Universal Editor ora si apre in modalità Produzione a meno che un amministratore non attivi esplicitamente la modalità Anteprima. (SITES-37193)
* Per impostazione predefinita, il comando Apri di Universal Editor è ora disponibile in modalità Anteprima negli ambienti di sviluppo e stage. Il comando aggiunge preview=true, che mantiene i controlli dell’autore allineati con il contesto di anteprima ed evita l’apertura accidentale della produzione. (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

Assets Relate ora funziona per i nomi di file che includono spazi. La logica del client di relazione aggiornata ora gestisce correttamente i percorsi contenenti spazio ed evita `undefined` errori di origine durante la selezione della relazione. Viene visualizzata la finestra di dialogo Riferisci (Relate), che consente di salvare le relazioni senza interruzioni dell&#39;interfaccia utente o spiner. Gli utenti DAM possono correlare, derivare e annullare la correlazione delle risorse senza rinominare i file. (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* Nuova integrazione del lettore video Dynamic Media (rollout limitato) - Una nuova esperienza di lettore video Dynamic Media è ora disponibile in AEM 6.6 Quickstart. Questo miglioramento è attualmente abilitato solo per i clienti iniziali come parte di un rollout controllato. (Assets-60165)
* È stato risolto un problema che impediva all&#39;opzione Seleziona miniatura nella finestra di dialogo delle proprietà video di aprire il selettore risorse, consentendo agli utenti di scegliere miniature personalizzate per le risorse video. (Assets-58926)
* Nei video Dynamic Media, è stato aggiunto il supporto per la selezione dell’arabo nell’elenco a discesa Lingua sottotitoli e tracce audio, consentendo agli autori di gestire i sottotitoli arabi direttamente in AEM. (Assets-61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->


<!--
### [!DNL Forms]{#forms-65-lts-sp2}

#### Forms Designer

#### Forms

#### Forms JEE 

#### Forms Captcha {#forms-captcha-65-lts-sp2}

#### XMLFM {#forms-xmlfm-65-lts-sp2}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp2}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp2}

#### Forms Designer

#### AdaptIve Forms

#### Forms Captcha

#### Forms Management UI
-->


### Foundation {#foundation-65-lts-sp2}

#### Apache Felix {#foundation-apachefelix-65-lts-sp2}

* La sicurezza Sling Resource Access è ora in esecuzione sulla versione 1.1.2. ResourceAccessSecurityImpl non genera più un&#39;eccezione ClassCastException durante l&#39;inizializzazione quando vengono registrati più servizi ResourceAccessGateHandler. L&#39;inizializzazione viene ora completata in modo affidabile ed evita errori di avvio in ambienti con più gestori. (NPR-42750)
* Console JMX e Console Web ora inviano un `Content-Type: text/css header` per le risorse CSS della console. Il controllo MIME rigoroso non blocca più il caricamento del foglio di stile, pertanto nell&#39;interfaccia utente `/system/console/jmx` viene eseguito il rendering con uno stile normale. (GRANITE-63677)
* AEM ora evita di duplicare le voci ACL per il gruppo `contributor` in `WEB-INF/resources/provisioning/model.txt` generato. L’output WAR ora contiene un blocco ACL coerente, che impedisce la confusione delle autorizzazioni durante la revisione. (GRANITE-63269)
* AEM non cancella più le impostazioni di deserializzazione Firewall (Firewall deserializzazione) durante le operazioni di aggiornamento del bundle, inserire nell&#39;elenco Bloccati inserire nell&#39;elenco Consentiti e. La logica di registrazione del filtro aggiornata mantiene l’istanza del firewall attiva allineata con la configurazione salvata, pertanto la protezione rimane abilitata senza riavviare il sistema. (GRANITE-61382)
* La console Web Felix non genera più `NullPointerException` errori intermittenti durante l&#39;accesso `/system/console`. La gestione ServiceTracker aggiornata impedisce uno stato di tracciamento null. L’accesso e la navigazione dalla console rimangono stabili durante le richieste ripetute e la convalida automatizzata. (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

CRXDE Lite non mostra più una scheda vuota quando si apre un file JSP dopo un aggiornamento del Service Pack. AEM ora distribuisce il codice principale e aggiuntivo di CodeMirror corrispondente, evitando in tal modo l’errore irreversibile del browser e mantenendo l’editor utilizzabile. (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

Convalida sicurezza espressioni ora gestisce valori di configurazione OSGi vuoti o nulli. Applica i valori predefiniti sicuri, ignora le matrici vuote e registra i registri di cancellazione, impedendo NullPointerException e risultati di convalida imprevedibili. (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### Integrazioni{#foundation-integrations-65-lts-sp2}

AEM ora sincronizza le attività di Adobe Target anche quando esistono date di inizio e di fine. Il payload di Target ora formatta le date dell’attività come marche temporali ISO 8601 complete, inclusi secondi, millisecondi e fuso orario. Target non rifiuta più la richiesta con `InvalidJson.Json`. Le attività pianificate ora passano a uno stato sincronizzato invece di rimanere non sincronizzate. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 



#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS Service Pack 2 richiede S3 Connector 1.60.10 o versione successiva. La configurazione dell’archivio dati S3 ora include `crossRegionAccess` e `mode`, quindi gli amministratori possono abilitare l’accesso al bucket tra aree geografiche e passare l’archiviazione a GCP quando necessario. `s3EndPoint` prevede ora un&#39;area allineata a `s3Region` oppure rimane vuota in modo che il driver generi l&#39;endpoint. (GRANITE-64873)


#### Quickstart{#foundation-quickstart-65-lts-sp2}

* Sling aggiorna il elenco Consentiti amministrativo-di accesso per utilizzare la terminologia inclusiva e i nuovi PID di configurazione. Questa modifica è allineata con Sling JCR Base 3.2.0. (GRANITE-63756)

  **Impatto**

   * Sling depreca questi PID e devi rimuoverli dalle configurazioni:
      * PID factory: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * PID globale: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
Queste configurazioni meno recenti utilizzano proprietà quali `whitelist.name` e `whitelist.bundles`.

   * Sling fornisce ancora una parziale compatibilità con le versioni precedenti per i PID obsoleti, ma non li utilizza per le nuove configurazioni. Utilizza i PID `LoginAdminAllowList.*` più recenti.
   * Non eseguire contemporaneamente configurazioni di inserisco nell&#39;elenco Consentiti obsolete e nuove configurazioni di. Configurazioni miste possono creare ambiguità e produrre comportamenti non desiderati. Quando esegui la migrazione ad AEM 6.5 LTS SP2, rimuovi completamente i PID obsoleti.

  **Come comportarsi**

   1. Trovare configurazioni di inserisce nell&#39;elenco Consentiti di che utilizzano `LoginAdminWhitelist*` PID.
   1. Sostituirli con i nuovi PID appropriati:

      * PID factory: `org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * PID globale: `org.apache.sling.jcr.base.LoginAdminAllowList`

      Per ulteriori dettagli, consulta [Approccio obsoleto per inserire nell&#39;elenco Consentiti i bundle per l&#39;accesso amministrativo](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login).

* AEM 6.5 LTS SP2 aggiorna il bundle di Foundation Layer impostato per Sling, Oak e Felix. Questi aggiornamenti rafforzano la stabilità del runtime principale e allineano le versioni delle dipendenze in tutta la piattaforma. (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311) -->

#### Sling{#foundation-sling-65-lts-sp2}

AEM ora include Sling Engine 2.16.6. Questa modifica elimina le violazioni XSS segnalate dagli strumenti di sicurezza e migliora la sicurezza e la stabilità del rendering di base. (NPR-43105)

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

AEM Translations non genera più errori in Java 17 o Java 21 a causa di problemi di formato XLIFF. La pipeline di esportazione ora produce XLIFF conformi agli standard accettati dai provider di traduzione. Questa modifica rimuove le interruzioni del lavoro di traduzione e ripristina un trasferimento prevedibile tra AEM e i servizi di traduzione. I flussi di lavoro di traduzione ora rimangono stabili nei runtime Java supportati. (CQ-4360217)

#### Flusso di lavoro{#foundation-workflow-65-lts-sp2}

EmailNotificationService-Processor non attiva più errori ripetuti di tipo &quot;Segmento non trovato&quot; durante la gestione delle notifiche del flusso di lavoro. La gestione aggiornata delle eccezioni rileva SegmentNotFoundException e interrompe il ciclo di elaborazione invece di continuare con letture non valide. L’esecuzione del flusso di lavoro rimane stabile e il rumore del registro diminuisce durante l’accesso alla casella in entrata e all’elemento di lavoro. (GRANITE-62635)




## Informazioni su [!DNL Experience Manager Foundation] {#experience-manager-foundation}

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
* Per istruzioni di aggiornamento dettagliate, consulta la [Guida all&#39;aggiornamento per AEM Forms 6.5 LTS SP1 su JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### Best practice per gli aggiornamenti del Service Pack di AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**Ambiente**
Applicabile a: clienti AEM 6.5 LTS (On-Premise) che installano Service Pack 2 (SP2). SP2 viene fornito come file JAR Quickstart.

**Perché è importante**
SP2 per AEM 6.5 LTS viene fornito come file JAR Quickstart anziché come file ZIP da installare tramite Gestione pacchetti. I clienti on-premise possono eseguire l’aggiornamento sostituendo il file Quickstart JAR, decomprimendolo e riavviandolo. Questo metodo è coerente con la procedura di aggiornamento diretto di Adobe.

**Flusso di aggiornamento consigliato (authoring o pubblicazione)**

1. Verifica che l’istanza AEM 6.5 LTS sia integra e accessibile.
1. Scarica il file JAR Quickstart (ad esempio, `cq-quickstart-6.6.x.jar`) da Software Distribution.
1. Arresta l&#39;istanza in esecuzione.
1. Nella directory di installazione di AEM (all&#39;esterno di `crx-quickstart/`), sostituire il file JAR Quickstart precedente con il file JAR SP2.
1. Decomprimi il file JAR:

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (Regola i flag dell&#39;heap in base alle esigenze).

1. Rinomina il file JAR decompresso in modo che corrisponda al ruolo e alla porta, ad esempio `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Avvia AEM e conferma l’aggiornamento nell’interfaccia utente (Guida > Informazioni) e nei registri.

**Buone pratiche**

* Esegui l’aggiornamento in ambienti di test o inferiori prima di eseguirlo in ambienti di produzione.
* Prima di iniziare, è necessario eseguire un backup completo e ripristinabile (archivio più eventuali archivi dati esterni).
* Consulta la guida all’aggiornamento diretto di Adobe e i requisiti tecnici (consigliato Java 17/21 per LTS).

>[!NOTE]
>
>I nomi di file mostrati sopra (ad esempio, `cq-quickstart-6.6.x.jar`) riflettono la denominazione dell&#39;artefatto Quickstart osservata per questa versione LTS; utilizzare sempre il nome di file esatto scaricato da Software Distribution.

## Installazione e aggiornarnamento{#install-update}

Per i requisiti di configurazione, consulta [Istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

>[!NOTE]
>
> Se si esegue l&#39;aggiornamento diretto a LTS SP1 da 6.5 SP precedenti, seguire le istruzioni fornite per l&#39;aggiornamento da 6.5 a 6.5 LTS GA [upgrade](/help/sites-deploying/upgrade.md).


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
| Quickstart | API Mongo | Le API Mongo ora sono obsolete e la loro rimozione è prevista nelle versioni future. | 6.5 TS SP2 |
| Sites | Supporto dei frammenti di contenuto nell’API REST di AEM Assets | AEM 6.5 LTS SP2 fornisce API OpenAPI moderne per la gestione di modelli e frammenti di contenuto; pertanto, gli endpoint precedenti per il supporto dei frammenti di contenuto nell’API REST di AEM Assets sono ora obsoleti.<br>Adobe intende mantenere questi endpoint meno recenti disponibili fino a un annuncio di fine del ciclo di vita. Adobe non prevede ulteriori miglioramenti per gli endpoint obsoleti. | 6,5 LTS SP2 |
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

### Installare gli indici Oak richiesti per le API headless di Sites{#site-headless-api}

Alcune API che sono state spostate in Sites Headless richiedono indici Oak aggiuntivi per garantire la piena funzionalità.

Installare il pacchetto `cq-dam-cfm-indices` per utilizzare le funzionalità seguenti:

* Elencare modelli per frammenti di contenuto
* Elenco frammenti di contenuto
* API di ricerca
* Flussi di lavoro

Scarica il pacchetto di indice [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip) dal portale di distribuzione software di Adobe.

### Errore di connessione di Dispatcher con la funzione solo SSL (risolto in AEM 6.5 LTS SP1 e versioni successive){#ssl-only-feature}

>[!NOTE]
>
> Questo problema è presente solo nella versione AEM 6.5 LTS GA.

Quando si abilita la funzione solo SSL nelle implementazioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze Dispatcher e AEM. Dopo aver abilitato questa funzione, le verifiche stato potrebbero non riuscire e la comunicazione tra le istanze Dispatcher e AEM potrebbe essere interrotta. Questo problema si verifica in modo specifico quando i clienti tentano di connettersi tramite `https + IP` dalle istanze Dispatcher ad AEM. È correlato a problemi di convalida SNI (Server Name Indication).

**Impatto**

* Errori di verifica stato con codici di risposta HTTP 400
* Traffico interrotto tra istanze Dispatcher e AEM
* Il contenuto non può essere gestito correttamente tramite Dispatcher
* Errori di connessione durante l’utilizzo di HTTPS con indirizzi IP nella configurazione di Dispatcher
* HTTP 400: errori “SNI non valida” durante la connessione tramite HTTPS + IP

**Ambienti interessati**

* Implementazioni di AEM con configurazioni Dispatcher
* Sistemi in cui è stata abilitata la funzione solo SSL
* Configurazioni di Dispatcher che utilizzano il metodo di connessione `https + IP` alle istanze AEM

**Soluzione**

Se riscontri questo problema, contatta l’Assistenza clienti Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip). Non tentare di abilitare le funzioni solo SSL finché non viene applicato l’hotfix necessario.

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i Pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 LTS, Service Pack 1:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei Pacchetti di contenuti inclusi in Experience Manager 6.5 LTS, Service Pack 1](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web con restrizioni{#restricted-sites}

Questi siti web sono disponibili solo per la clientela. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience).

