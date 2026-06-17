---
title: Note sulla versione corrente di Adobe Experience Manager 6.5 LTS, SP2
description: Informazioni sulla versione corrente di Adobe Experience Manager 6.5 LTS, Service Pack 2.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 6795f085b5a4d1ac2836b6c6f2f4d09a5739e639
workflow-type: tm+mt
source-wordcount: '7697'
ht-degree: 96%

---


# Note sulla versione corrente di Adobe Experience Manager 6.5 LTS, SP2 {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versione | Service Pack 2 (SP2) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 19 febbraio 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione del software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> **Hotfix obbligatorio**: per evitare problemi di SNFE (SegmentNotFoundException) con la compattazione offline durante l’installazione del SP2, installare l’hotfix descritto in [Problemi noti: corruzione dell’archivio durante la compattazione online](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146).

## Funzionalità incluse in [!DNL Adobe Experience Manager] 6.5 LTS, SP2 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP2 include nuove funzionalità, miglioramenti importanti richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la disponibilità iniziale di 6.5 LTS a marzo 2025. [Installare il Service Pack](#install-update) su 6.5 LTS.

## Funzionalità chiave e miglioramento

**AEM Sites**

AEM 6.5 LTS SP2 ora include OpenAPI per la [gestione di modelli e frammenti di contenuto](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/) e i [lanci](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/). Queste API forniscono l’accesso ai frammenti di contenuto e ai lanci per l’authoring e la pianificazione. Utilizzano le stesse OpenAPI moderne di AEM as a Cloud Service.

**AEM Forms**

**Funzionalità incluse in AEM Forms 6.5 LTS, SP2**

* È stato aggiunto il supporto per RDBMK con JBoss® EAP 8.0.

* È stato aggiunto il supporto per WebSphere® Liberty Profile (WLP). WLP è supportato solo con Oracle Database e IBM® Sumeru JDK 21.

* Esperienza utente migliorata nell’editor di regole visivo. Questo aggiornamento include:

   * Ricaricamento automatico della vista riepilogo dopo un salvataggio per mostrare lo stato aggiornato della regola

   * Visualizzazione dei pulsanti “Aggiungi”/“Elimina” e possibilità di attivazione/disattivazione della selezione anziché nasconderli

   * Fornitura di un feedback chiaro quando un’operazione di salvataggio di una regola non riesce (FORMS-21261)

* È stata aggiunta un’API (Application Programming Interface) di runtime aggiunte per attivare/disattivare la modalità di esportazione XML (Extensible Markup Language) legacy in AEM Forms, in sostituzione del parametro `Dcom.adobe.fd.forms.export.legacy`. Questo miglioramento consente agli utenti di passare da una modalità di esportazione all’altra in modo più efficiente, migliorando la flessibilità del flusso di lavoro. (FORMS-23115)

* È stato aggiunto il supporto per JSON (JavaScript Object Notation) con tag dello spazio dei nomi nei moduli adattivi. Questo miglioramento consente agli utenti di gestire le strutture di dati JSON in modo più efficace, migliorando le capacità di integrazione e di elaborazione dei dati. (FORMS-22519)

* È stato stato aggiunto il download del documento record (DoR)/invio del modulo come pulsante predefinito (OOTB) nell’editor di regole. Questo miglioramento consente ai clienti di utilizzare la funzione downloadDoR senza scrivere codice personalizzato, migliorando l’usabilità e l’efficienza. (FORMS-21263)

* È stato aggiunto il supporto per JSON (JavaScript Object Notation) con tag dello spazio dei nomi nei moduli adattivi. Questo miglioramento consente agli utenti di precompilare i moduli in modo più accurato ed efficiente, migliorando l’integrazione dei dati e riducendo gli errori di input manuali. (FORMS-10883)

<!-- UPDATE THE EACH RELEASE -->

## Sono stati risolti i problemi in 6.5 LTS, Service Pack 2 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP2}

#### Accessibilità {#sites-accessibility-65-lts-sp2}

* Il componente Testo non era più attivo sulla tastiera quando gli autori passavano con il mouse sugli elementi nel Browser dei componenti durante la modifica. Questo interrompeva la digitazione e causava una violazione dei criteri di accessibilità previsti dallo standard WCAG 3.2.1. La correzione impedisce allo stile applicato al passaggio del mouse di spostare lo stato attivo, mantenendo il componente Testo attivo durante l’interazione con il Browser dei componenti. (SITES-35370)
* È stata corretta la gestione dello stato attivo nel campo rich text della Descrizione, che bloccava la navigazione successiva con il tasto TAB. Gli utenti rimanevano bloccati nell’editor Rich Text perché il componente si affidava a un comando da tastiera non standard per spostare lo stato attivo, interrompendo la normale navigazione della finestra di dialogo. La modifica applica l’interazione standard da tastiera e mantiene la sequenza logica del tasto TAB all’interno dell’intera finestra di dialogo. (SITES-35228)
* È stato risolto un problema nell’editor Sites che interrompeva il comportamento previsto durante l’authoring della pagina e causava interazioni incoerenti con i componenti. Gli autori riscontravano risposte instabili dell’interfaccia utente, che interferivano con le attività di modifica standard e riducevano l’efficienza del flusso di lavoro. L’aggiornamento perfeziona la logica di base dell’editor e ripristina un’interazione stabile e prevedibile su tutti i componenti interessati. (SITES-35227)
* Una regressione che ha bloccato selettore delle risorse nell’editor di pagine, impedendone il caricamento in scenari specifici di modifica. Gli autori possono ora aprire e utilizzare normalmente il selettore delle risorse quando scelgono o esplorano le risorse durante la modifica di una pagina. Questa modifica ripristina un accesso coerente ai flussi di lavoro di selezione delle risorse che interrompono il caricamento degli errori. (SITES-35226)
* È stato eliminato un problema nell’editor Sites che causava un comportamento incoerente durante l’interazione delle pagine e interrompeva i flussi di lavoro di authoring standard. Il difetto ha portato a risposte dell’interfaccia utente impreviste, che hanno interferito con la configurazione dei componenti e gli aggiornamenti dei contenuti. L’aggiornamento stabilizza la funzionalità interessata e ripristina l’esecuzione affidabile delle azioni di modifica su più pagine. (SITES-35225)
* È stato eliminato un difetto nell’interfaccia di authoring di Sites che causava un comportamento incoerente durante la modifica delle pagine e interrompeva i normali flussi di lavoro. Gli autori hanno riscontrato risposte dell’interfaccia utente impreviste, che hanno interferito con l’interazione dei componenti e gli aggiornamenti dei contenuti. L’aggiornamento stabilizza le funzionalità interessate e ripristina un comportamento affidabile e prevedibile in tutti gli scenari di modifica. (SITES-35224)
* AEM Sites ora include il supporto testo `alt` sulle immagini per soddisfare i requisiti ADA e WCAG. L’output della pagina non omette più gli attributi `alt`, pertanto gli assistenti vocali ricevono il testo alternativo corretto. (SITES-27153)
* È stato corretto il layout della barra degli strumenti `Note Add` in modo che il pulsante Aggiungi non si sovrapponga più al titolo con una larghezza del riquadro di visualizzazione di 320 px. È stata migliorata la ridisposizione per schermi piccoli modo che i controlli rimangano leggibili e utilizzabili con uno zoom al 400%. (SITES-25376)
* Sono stati corretti gli annunci mancanti degli assistenti vocali per gli errori della finestra di dialogo di selezione dei collegamenti. L’interfaccia utente ora pubblica il testo dell’errore tramite un contenitore per messaggi di stato, pertanto NVDA legge il messaggio non appena viene visualizzato. (SITES-25368)
* Sono stati rimossi i ruoli griglia ARIA e cella griglia dall’elenco delle risorse nella barra laterale. Sono stati ripristinati la semantica degli elenchi standard e l’ordine dello stato attivo sulla tastiera, migliorando la navigazione degli assistenti vocali e riducendo le interruzioni delle tabulazioni aggiuntive. (SITES-25361)
* È stata corretta la sequenza dello stato attivo nella barra laterale di Assets. Gli utenti che utilizzano la tastiera ora raggiungono ogni azione della risorsa, inclusa la modifica, tramite un percorso di tabulazione coerente. (SITES-25360)
* È stato corretto l’overflow del layout nel modale Cerca risorse con una larghezza del riquadro di visualizzazione di 320 px. Il contenuto modale ora viene ridisposto e rimane leggibile, pertanto i controlli non si sovrappongono più né sovraccaricano la finestra di dialogo. (SITES-25330)
* Output NVDA corretto per il pulsante Modifica. NVDA ora annuncia l’azione Modifica, non “Pulsante Anteprima premuto”. (SITES-25320)
* Sono stati corretti gli input di testo della barra degli strumenti Demografia senza nome che causavano un output dell’assistente vocale silenzioso o generico. Ogni input ora espone un chiaro nome accessibile basato su etichette, che migliora la navigazione tramite tastiera e tecnologia per l’accessibilità. (SITES-25316)
* È stato corretto l’ordine dello stato attivo sulla tastiera per la barra degli strumenti dei dati demografici durante la navigazione nell’anteprima di layout. La navigazione tramite TAB ora si sposta direttamente dal pulsante Dati demografici ai controlli della barra degli strumenti, senza saltare alla barra degli strumenti secondaria. (SITES-25305)
* È stato corretto l’ordine di annuncio errato per le etichette “Schermi più piccoli” e “Tablet” sul righello Modifica layout. Gli assistenti vocali ora annunciano queste etichette ai marcatori righello corretti, che corrispondono al layout della pagina. (SITES-25291)
* È stato corretto l’overflow della barra degli strumenti Modifica layout con uno zoom del 200%. Il contenuto ora rimane all’interno del riquadro di visualizzazione ed è raggiungibile tramite lo scorrimento. (SITES-25288)
* È stato risolto un ordine di stato attivo errato nella sovrapposizione delle annotazioni. La tabulazione da tastiera ora passa da controlli di sovrapposizione a elementi di annotazione. La pagina principale non si attiva più da dietro la sovrapposizione. (SITES-25282)
* È stata risolta la gestione dello stato attivo del popover Campioni. La finestra di dialogo ora sposta lo stato attivo su un’intestazione chiara e avvia l’output dell’assistente vocale in corrispondenza di tale punto di ingresso. NVDA non legge più il contenuto completo della finestra di dialogo fuori sequenza. (SITES-25275)
* È stata risolta la gestione dello stato attivo modale di Timewarp dopo la chiusura del selettore data. `Escape` ora restituisce lo stato attivo al pulsante Selettore data. La selezione della data ora posiziona lo stato attivo sul campo di input accanto al controllo Selettore data, impedendo la perdita dello stato attivo e l’accesso alla pagina in background. (SITES-25264)
* È stata risolta la gestione dello stato attivo sulla tastiera per la finestra di dialogo Elimina annotazione. Annulla ora restituisce lo stato attivo al controllo `Delete` che ha aperto la finestra di dialogo, non al controllo Conferma valore esadecimale. Gli assistenti vocali non annunciano più il contenuto di una finestra di dialogo non correlato dopo l’annullamento. (SITES-25258)
* È stata risolta la gestione dello stato attivo per la finestra di dialogo modale Annotazione. L’apertura della finestra di dialogo ora imposta lo stato attivo sull’intestazione della finestra di dialogo e impedisce a NVDA di leggere il contenuto dell’area di lavoro e il testo della finestra di dialogo non correlato. La navigazione tramite tastiera ora rimane all’interno della finestra di dialogo fino a quando non viene chiusa. (SITES-25257)
* Sono stati risolti i problemi di layout modale della ricerca a 320 px di larghezza. Il contenuto modale ora viene ridisposto in modo pulito ed evita la sovrapposizione con la directory della struttura. Gli utenti possono visualizzare i risultati e navigare nella directory senza controlli oscurati. (SITES-25246)
* Il testo modale della ricerca non viene più ritagliato dopo l’aumento della spaziatura. Il layout della directory della struttura mantiene ora una separazione chiara, in modo che le etichette e le voci rimangano leggibili. Gli utenti possono ora completare la ricerca e la navigazione senza sovrapposizioni o ritagli di testo. (SITES-25245)
* L’attivazione di Annota consente ora di spostare lo stato attivo sulla tastiera sul contenuto dell’annotazione, non sul pulsante Esci dall’annotazione. L’ordine di tabulazione segue una sequenza logica e consente di mantenere i controlli correlati raggiungibili senza navigazione inversa. (SITES-25241)
* I collegamenti Imposta data e Esci dal Timewarp non disponevano di un indicatore dello stato attivo visibile durante la navigazione da tastiera. L’interfaccia utente ora esegue il rendering di uno stile di stato attivo a contrasto elevato distinto in modo che gli utenti possano identificare il collegamento attivo in sintesi. (SITES-25232)
* L’intestazione modale teaser non impedisce più agli utenti che utilizzano la tastiera di spostare la finestra di dialogo. I controlli da tastiera consentono ora le azioni di acquisizione, spostamento e rilascio, che migliorano l’usabilità dell’assistente vocale e l’operabilità complessiva. (SITES-25226)
* AEM ora utilizza un’etichetta accessibile significativa per il pulsante Informazioni modali teaser. Gli assistenti vocali annunciano un nome di azione chiaro invece della stringa di testo alternativo predefinita per l’icona. (SITES-25223)
* Gli assistenti vocali ora annunciano l’azione corretta quando gli utenti attivano il pulsante Modifica. NVDA non segnala più “Pulsante anteprima premuto”, che ha causato feedback fuorvianti e confusione durante la navigazione da tastiera. (SITES-25208)
* L’espansione della barra a sinistra ora sposta lo stato attivo sulla tastiera sul primo controllo della barra a sinistra. La sequenza TAB non salta più alla barra degli strumenti secondaria né arriva all’elenco intermedio, pertanto gli utenti con tastiera possono raggiungere il contenuto della barra a sinistra senza ricorrere alla navigazione inversa. (SITES-24998)
* Il contenuto della barra dell’emulatore del dispositivo ora rimane completamente visibile con una larghezza del riquadro di visualizzazione di 320 px. Il testo della barra degli strumenti e i controlli vengono disposti a capo anziché troncati, riducendo la sovrapposizione e migliorando la leggibilità. (SITES-24953)
* AEM ora visualizza l’etichetta del dispositivo iPhone completa nella barra degli strumenti dell’emulatore. Il testo non viene più troncato alla larghezza predefinita, migliorando la leggibilità e la chiarezza della selezione del dispositivo. (SITES-24952)
* Le intestazioni della tabella Vista a elenco ora espongono lo stato di ordinamento tramite ARIA. Gli assistenti vocali annunciano un ordine crescente o decrescente dopo un’azione di ordinamento delle colonne. (SITES-24943)
* AEM ora mantiene la visibilità dell’etichetta del menu Altre azioni nella Vista a scheda durante le modifiche della spaziatura del testo. Le opzioni di menu mantengono il testo completo, inclusa la pubblicazione rapida, e il menu rimane leggibile durante tutte le impostazioni di spaziatura del testo WCAG. (SITES-24941)
* La barra del menu Azioni scheda ora espone un nome accessibile in Vista a scheda. Gli assistenti vocali annunciano chiaramente lo scopo della barra dei menu e il controllo vocale può rivolgere il controllo in base al nome. (SITES-24938)
* La vista a scheda non si basa più sulla semantica della griglia ARIA, che ha causato confusione nel comportamento degli assistenti vocali. L’interfaccia utente fornisce ora ruoli ed etichette significativi per il contenuto della scheda e la barra delle azioni della scheda, che riduce i controlli mancanti durante l’utilizzo della tastiera. (SITES-24933)
* La descrizione comando `Delete Modal` viene ora visualizzata ogni volta che gli utenti passano il mouse sull’icona della descrizione comando. Le azioni dello stato attivo ora mostrano lo stesso testo della descrizione comando, migliorando l’accesso ripetuto per gli utenti che utilizzano il mouse e la tastiera. (SITES-24778)
* La navigazione nella barra a sinistra segue ora l’ordine previsto dello stato attivo sulla tastiera previsto dopo la configurazione della barra da parte degli utenti. Lo stato attivo del TAB si trova sull’area della barra a sinistra selezionata anziché su Passa a visualizzazione, migliorando la chiarezza della navigazione dell’assistente vocale. (SITES-24754)
* È stato risolto un feedback NVDA errato durante la navigazione dei campioni di colore nella finestra modale Preferenze utente. NVDA ora legge l’etichetta del campione che riceve lo stato attivo, rimuovendo l’output di colore fuorviante. Il set di campioni ora supporta una navigazione coerente da tastiera e il riconoscimento della selezione in modo chiaro. (SITES-24739)
* È stato ridotto l’output NVDA dettagliato per il controllo `Spin`. È stata rimossa l’etichettatura di gruppo ridondante che duplicava l’etichetta di input, pertanto NVDA annuncia il nome del controllo una volta. La navigazione tramite tastiera e assistente vocale ora offre un annuncio singolo e chiaro. (SITES-24725)
* La finestra di dialogo Carosello ora posiziona lo stato attivo sull’intestazione della finestra di dialogo anziché sulla scheda Elementi. Annulla ed Esc ripristinano lo stato attivo sul controllo che ha avviato la finestra di dialogo, riducendo l’output NVDA dettagliato. (SITES-24716)
* La finestra di dialogo Collega selezione ora allinea l’etichetta programmatica con l’etichetta visualizzata sullo schermo per gli elementi della struttura di ultimo livello. La navigazione con tasti di direzione attiva un annuncio dell’assistente vocale affidabile per ogni elemento e rimuove l’output di etichette fuorvianti. (SITES-24710)
* La finestra di dialogo Collega selezione aperta ora viene ridisposta correttamente sotto un riquadro di visualizzazione a 320 px. Il contenuto non supera più il modale o viene troncato e il modale non mostra più una barra di scorrimento orizzontale. (SITES-24709)
* La finestra di dialogo Collega selezione aperta ora ripristina lo stato attivo sulla tastiera sull’attivatore della finestra di dialogo dopo Chiudi o Annulla. Lo stato attivo non salta più all’input Collega, che mantiene stabile il contesto dell’assistente vocale e riduce la navigazione aggiuntiva. (SITES-24707)
* La finestra di dialogo modale dell’immagine ora segue una sequenza logica dello stato attivo. Lo stato attivo non ignora più i controlli precedenti o i rilasci sul punto di riferimento della pagina dopo l’annullamento e gli utenti riprendono lo stato attivo sul pulsante Configura dopo l’uscita. (SITES-24693)
* La finestra di dialogo modale Barra dei riferimenti ora registra lo stato attivo sulla tastiera. TAB e Maiusc+TAB rimangono all’interno dei controlli della finestra di dialogo e lo stato attivo non passa più al contenuto della pagina. Gli assistenti vocali annunciano solo il contenuto della finestra di dialogo. (SITES-24683)
* La finestra modale Selezione percorso collegamento ipertestuale ora imposta lo stato attivo sull’intestazione della finestra di dialogo all’apertura. Annulla chiude la finestra di dialogo e ripristina lo stato attivo sul pulsante Apri finestra di dialogo di selezione, impedendo la perdita dello stato attivo e l’output dell’assistente vocale ridondante. (SITES-24672)
* Il campo Ricerca ora utilizza un’etichetta persistente sullo schermo invece del testo segnaposto. L’etichetta rimane visibile durante l’immissione, migliorando la chiarezza per gli utenti che utilizzano tastiera, assistente vocale e riconoscimento vocale. (SITES-24529)
* La finestra di dialogo modale teaser ora imposta lo stato attivo sull’intestazione della finestra di dialogo all’apertura. La chiusura della finestra di dialogo restituisce lo stato attivo sul controllo `Configure`, impedendo la perdita dello stato attivo e l’eccessivo output dell’assistente vocale. (SITES-24522)
* Il pannello Assets della barra laterale ora include un controllo Chiudi. Chiudi restituisce lo stato attivo sulla tastiera sul pulsante di attivazione/disattivazione della barra laterale e impedisce la tabulazione forzata attraverso il contenuto del pannello. (SITES-24489)
* La tabulazione da tastiera ora raggiunge i pulsanti e i collegamenti all’interno delle tabelle di amministrazione. Gli utenti non si affidano più alla navigazione per celle con tasti di direzione per trovare i controlli interattivi. (SITES-24285)
* La finestra di dialogo del componente Immagine non espone più le icone decorative di guida e a schermo intero come immagini. Gli assistenti vocali ora ignorano queste icone, mantenendo lo stato attivo sui controlli actionable e sul contenuto dei campi. (SITES-2940)
* L’amministrazione sito ora rimuove il ruolo immagine dalle icone delle miniature delle cartelle. La tecnologia assistiva ignora questi elementi decorativi, mantenendo lo stato attivo sui nomi delle cartelle e sulle azioni. (SITES-2852)
* Struttura contenuto ora indirizza lo stato attivo sulla tastiera all’elemento della struttura attivo o al primo elemento della struttura. Il contenitore della struttura non funge più da punto di tabulazione vuoto, impedendo le trappole dello stato attivo di Maiusc+Tab. (SITES-1577)

#### Interfaccia utente amministratore{#sites-adminui-65-lts-sp2}

Le impostazioni della Vista a elenco della console Sites non riflettevano le colonne visualizzate nella Vista a elenco. La finestra di dialogo si apriva con le caselle di controllo deselezionate e un conteggio errato delle colonne selezionate. La correzione sincronizza lo stato della finestra di dialogo con le colonne della griglia attive e aggiorna il contatore in modo che corrisponda alla visibilità effettiva delle colonne. (SITES-38576)

#### Interfaccia utente classica{#sites-classicui-65-lts-sp2}

Dopo un aggiornamento, nella modifica del componente testo dell’interfaccia utente classica venivano visualizzati dei tag HTML non formattati, ma non Rich Text. Service Pack 2 corregge il rendering dell’editor Rich Text (RTE) dell’interfaccia utente classica in modo che l’editor visualizzi il contenuto formattato e conservi il markup memorizzato. La correzione interrompe anche l’espansione del markup durante le modifiche e i salvataggi ripetuti. (SITES-38709)

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

In 6.5 LTS, il supporto per gli eventi headless non disponeva degli eventi OSGi richiesti per frammenti di contenuto e modelli. L’aggiornamento aggiunge il bundle di eventi più le dipendenze richieste e include una build 6.5 LTS. Gli eventi Modello e Frammento di contenuto ora vengono attivati correttamente e supportano i flussi di lavoro API Launches. (SITES-35329)

#### [!DNL Content Fragments] - Amministratore{#sites-admin-65-lts-sp2}

* È stata regolata la gestione dei componenti nell’interfaccia di authoring di Sites per interrompere il comportamento irregolare durante gli aggiornamenti delle pagine. Il difetto ha portato a risposte dell’editor imprevedibili che hanno interferito con le modifiche di routine del contenuto e ridotto l’efficienza del flusso di lavoro. L’aggiornamento allinea la logica dell’editor ai pattern di interazione previsti e offre prestazioni affidabili durante le attività di authoring. (SITES-35078) CRITICO

* Una regressione ha interrotto la Vista a elenco della console Assets per i frammenti di contenuto e ha attivato un errore durante il rendering dell’elenco. L’aggiornamento corregge la logica della vista a elenco dopo la rimozione delle informazioni di anteprima e ripristina l’output dell’elenco stabile. La console ora visualizza i frammenti di contenuto senza errori e mantiene utilizzabili le interazioni dell’elenco. (SITES-38683)
* L’editor frammenti di contenuto ora localizza l’etichetta Tag. L’editor localizza anche l’etichetta Raccolte, in modo che il testo dell’interfaccia utente corrisponda alle impostazioni internazionali selezionate. (SITES-977)


#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-65-lts-sp2}

* I tag della variante dei frammenti di contenuto scomparivano quando l’attivazione della funzione rimaneva disabilitata dopo il refactoring. La correzione ripristina il supporto dei tag della variante anche quando il pulsante di attivazione/disattivazione rimane disattivato. Gli autori possono nuovamente aggiungere e visualizzare i tag delle varianti nell’editor frammenti di contenuto. (SITES-38682) CRITICO
* I frammenti di contenuto modificati sono scomparsi dall’elenco della console Assets dopo che gli autori sono tornati dall’editor frammenti di contenuto. La memorizzazione in cache del browser ha restituito un elenco non aggiornato e ha nascosto il frammento aggiornato fino a un aggiornamento manuale. La correzione aggiunge la gestione di controllo della cache per il percorso di ritorno dell’editor in modo che l’elenco venga ricaricato correttamente e che il frammento modificato rimanga visibile. (SITES-35374) CRITICO

* L’editor Rich Text per frammenti di contenuto mostrava problemi di layout e di visualizzazione dopo recenti modifiche di stile dell’interfaccia utente. Service Pack 2 ottimizza lo stile dell’editor Rich Text in modo che la barra degli strumenti e l’area modificabile eseguano il rendering correttamente e rimangano leggibili. L’editor frammenti di contenuto ora è allineato con l’aspetto e il comportamento dell’editor pagina. (SITES-38684)
* La rimozione degli ambiti IMS dal selettore risorse Polaris ha interrotto l’integrazione del frammento di contenuto con l’endpoint di consegna. Gli autori riscontrano errori all’apertura del selettore risorse remoto e durante la selezione delle risorse. L’aggiornamento aggiunge nuovamente gli ambiti IMS necessari e ripristina l’accesso stabile a livello di consegna. (SITES-35837)
* Il pannello Contenuto associato non esegue più il rendering di un segnaposto codificato &quot;non definito&quot;. L’Editor frammento di contenuto ora risolve il testo tramite le risorse di localizzazione, in modo che gli editor possano vedere il testo tradotto dell’interfaccia utente. (SITES-33675)
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* L’editor frammenti di contenuto ora visualizza un’etichetta della scheda Generale tradotta per tutte le lingue. L’editor sostituisce il testo della scheda non localizzato e rimuove gli ID interni dai titoli della scheda. (SITES-30715)
* L’editor frammenti di contenuto ora visualizza i nomi tradotti per i tipi di risorse consentiti. L’elenco selettore non combina più stringhe interne ed etichette solo in inglese quando gli autori configurano le restrizioni relative ai riferimenti ai contenuti. (SITES-29699)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-65-lts-sp2}

* È stata perfezionata la gestione della convalida delle query GraphQL per interrompere gli errori di distribuzione causati da errori di esecuzione del filtro. Il difetto ha generato eccezioni durante l’avvio dell’applicazione e ha bloccato il rollout riuscito negli ambienti interessati. La revisione garantisce un comportamento di convalida coerente e consente una distribuzione fluida senza interruzioni della convalida delle query di runtime. (SITES-34301) CRITICO

* La finestra di dialogo Modifica endpoint GraphQL ora visualizza stringhe dell’interfaccia utente localizzate. La finestra di dialogo non mostra più il testo solo in inglese, ad esempio “Lo schema GraphQL proviene dalla configurazione” e le etichette correlate vengono create correttamente nelle diverse lingue. (SITES-34018)

#### [!DNL Content Fragments] - Editor di query GraphQL{#sites-graphql-query-editor-65-lts-sp2}

* È stata perfezionata la gestione della convalida delle query GraphQL per interrompere gli errori di distribuzione causati da errori di esecuzione del filtro. Il difetto ha generato eccezioni durante l’avvio dell’applicazione e ha bloccato il rollout riuscito negli ambienti interessati. La revisione garantisce un comportamento di convalida coerente e consente una distribuzione fluida senza interruzioni della convalida delle query di runtime. (SITES-35529)
* GraphQL Explorer non avrà più esito negativo se il nome di un browser configurazione contiene caratteri CJK. La creazione degli endpoint e l’accesso alle query salvate funzionano normalmente e la pagina GraphQL Query Editor rimane priva di errori. (SITES-31616)

#### [!DNL Content Fragments] - Editor modello{#sites-model-editor-65-lts-sp2}

* I modelli di frammenti di contenuto nidificati non funzionavano più quando il refactoring associava la funzione a un pulsante di attivazione/disattivazione disabilitato. La correzione ripristina il supporto del modello nidificato senza richiedere l’attivazione/disattivazione delle modifiche. Gli autori possono di nuovo creare e utilizzare modelli nidificati nell’editor di modelli. (SITES-38681) CRITICO

* Il pannello dei filtri Modelli di frammenti di contenuto non espone più stringhe non localizzate. AEM ora visualizza le etichette dei filtri localizzate e i valori dello stato localizzati in tutte le lingue. (SITES-30863)
* L’editor modello per frammenti di contenuto ora esegue il rendering delle stringhe localizzate per la finestra di dialogo di avviso del blocco. L’interfaccia utente sostituisce i messaggi in inglese non localizzati con risorse locali nelle lingue supportate. (SITES-28592)

#### [!DNL Content Fragments] - API REST{#sites-restapi-65-lts-sp2}

AEM Headless richiedeva un ramo della versione dedicato per evitare conflitti di versione del bundle e di dipendenza con le build principali. L’aggiornamento aggiunge un ramo headless `release/6.5lts` e allinea i set di dipendenze e le versioni del bundle. Jenkins ora crea la base di codice headless in modo pulito, senza conflitti tra versioni. (SITES-36585)

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### API contenuto{#sites-content-api-65-lts-sp2}

Un difetto di attivazione della funzione ha segnalato in modo errato lo stato dell’API di gestione pagina. L’aggiornamento aggiunge un flag di abilitazione dedicato e lo valuta insieme al pulsante di attivazione/disattivazione esistente. L’API di gestione pagina ora mostra uno stato stabile. L’API di gestione sito rimane sperimentale. (SITES-39284)

#### Back-end core{#sites-core-backend-65-lts-sp2}

* Una modifica nell’esperienza di authoring di Sites per risolvere comportamenti incoerenti che hanno interrotto i flussi di lavoro di modifica delle pagine standard. Gli autori hanno riscontrato risultati imprevisti durante l’interazione con i componenti, che hanno interferito con gli aggiornamenti dei contenuti e ridotto l’affidabilità. La modifica ripristina un comportamento dell’editor stabile e garantisce l’esecuzione coerente delle azioni di authoring in tutti gli scenari interessati. (SITES-35162) CRITICO

* È stato perfezionato il comportamento di authoring di Sites per risolvere un problema che ha interrotto la modifica della pagina e causato risultati incoerenti durante l’interazione con i componenti. Gli autori hanno riscontrato risposte dell’interfaccia utente impreviste che hanno interferito con gli aggiornamenti dei contenuti e ridotto l’affidabilità del flusso di lavoro. La modifica ripristina una gestione stabile dello stato dell’editor e garantisce l’esecuzione prevedibile delle azioni di authoring negli scenari interessati. (SITES-34499)

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### Lanci{#sites-launches-65-lts-sp2}

* La timeline di Sites mostrava un testo in inglese hardcoded durante la promozione dei lanci: “Creata versione ... prima di promuovere il lancio”. L’aggiornamento sostituisce la stringa hardcoded con la gestione localizzata d messaggio. La timeline ora visualizza il testo localizzato e allinea la voce con il comportamento di localizzazione di AEM standard. (SITES-39157)
* L’ambito della promozione del lancio si è spostato quando gli autori hanno promosso una sottosezione utilizzando Promuovi pagina corrente e sottopagine. AEM ha inoltre promosso pagine non correlate e causato modifiche al sito attivo impreviste. La correzione corregge il calcolo dell’ambito del lancio in modo che venga promosso solo la truttura secondaria scelta. (SITES-38315)
* I frammenti di contenuto all’interno dei lanci non hanno partecipato all’indice `damAssetLucene` e hanno limitato i risultati della ricerca e l’efficienza delle query. Questa modifica aggiunge i percorsi dei frammenti di contenuto dei lanci alla definizione dell’indice. Nelle query di ricerca e personalizzate sono ora disponibili frammenti di contenuto in `/content/launches`. (SITES-35634)
* Nell’interfaccia utente Lanci sono stati visualizzati i controlli di lancio per frammenti di contenuto, anche se il prodotto non espone i lanci per frammenti di contenuto nell’interfaccia utente touch. Questa modifica elimina i percorsi di codice relativi ai lanci dei frammenti di contenuto da cq-launches-content e regola il filtro dell’elenco dei lanci. Gli autori ora visualizzano opzioni coerenti per i lanci di pagina, senza le voci relative ai lanci dei frammenti di contenuto. (SITES-35633)
* In AEM 6.5 LTS Quickstart mancavano i prerequisiti e i bundle dei lanci richiesti, bloccando l’abilitazione OpenAPI dei lanci. L’aggiornamento aggiunge i bundle dei lanci e le dipendenze richieste, ad esempio il supporto alle metriche, gli aggiornamenti DAM-cfm e la configurazione della coda. Le API lanci ora vengono eseguite su 6.5 LTS Quickstart con i componenti di runtime richiesti presenti. (SITES-35297)
* Il pacchetto CF lanci richiamava versioni di dipendenze più recenti e librerie GraphQL non necessarie, rendendo complicata l’integrazione con AEM 6.5 LTS. Questa modifica allinea le versioni delle dipendenze alla linea di base di AEM 6.5 LTS ed elimina le dipendenze GraphQL non utilizzate. La risoluzione del bundle ora rimane coerente e l’avvio di CF lanci rimane stabile. (SITES-35295)
* AEM Launch ora esegue una pipeline Jenkins dedicata per il ramo 6.5 LTS. La pipeline viene eseguita ogni notte per generare e inviare avvisi di errore tramite e-mail. Questa configurazione aumenta la copertura dei test e rileva tempestivamente le regressioni. (SITES-35293)
* AEM 6.5 LTS ora distribuisce un bundle API lanci aggiornato con versioni allineate degli artefatti. Il bundle tiene traccia della riga del codice principale mantenendo la versione corretta della versione 6.5 LTS. Questo aggiornamento stabilizza il consumo dell’API lanci nello stack 6.5 LTS. (SITES-35292)
* AEM 6.5 LTS ora include un bundle di base per lanci aggiornato con versioni delle dipendenze allineate. L’aggiornamento aggiunge la gestione di base per lanci per i tipi di dati UUID di frammenti e UUID di riferimento. L’elaborazione del lancio ora mantiene un comportamento coerente tra i lanci e i flussi di lavoro per frammenti di contenuto. (SITES-35290)
* È stato perfezionato l’editor Sites per risolvere comportamenti incoerenti che hanno interrotto i normali flussi di lavoro di authoring delle pagine. Gli autori hanno riscontrato un’interazione imprevista tra i componenti che ha interferito con gli aggiornamenti dei contenuti e ha ridotto l’affidabilità delle modifiche. La modifica ripristina la gestione coerente dello stato dell’interfaccia utente e garantisce l’esecuzione prevedibile delle azioni di authoring negli scenari interessati. (SITES-35138)
* Modifica lanci ora mostra il testo dell’errore localizzato invece della stringa `Provided path is not a launch` hardcoded. Ora l’interfaccia utente esegue il rendering dei messaggi tradotti tra le lingue quando la funzione Modifica riceve un percorso di lancio non valido. (SITES-33360)
* AEM 6.5 LTS ora include il funzionamento delle porte laterali OpenAPI dei lanci. L’aggiornamento porta in parità i bundle API lanci, i pacchetti di contenuti e gli artefatti Quickstart richiesti e abilita gli scenari OpenAPI dei lanci per frammenti di contenuto con convalida CI stabile. (SITES-32050)
* L’interfaccia utente Lanci ora localizza l’etichetta del modello Sostituito. I dettagli di sostituzione del modello ora visualizzano il testo tradotto invece di una stringa solo in inglese. (SITES-29525)
* AEM ha risolto una chiave di localizzazione mancante in **Siti** > **Lanci** > **Modifica**. Ora gli utenti visualizzano un messaggio di errore tradotto invece della stringa non elaborata “Impossibile aggiornare l’elenco delle origini del lancio”. (SITES-21499)
* L’interfaccia utente di promozione del lancio ora visualizza le etichette di stato localizzate e le azioni. Nell’area di anteprima viene visualizzato il testo tradotto per **Eliminato**, **Nuovo** e **Visualizza**, anziché le stringhe non elaborate in inglese. (SITES-13540)
* La creazione del lancio ora mostra messaggi di errore localizzati. L’interfaccia utente non visualizza più stringhe non elaborate in inglese, ad esempio `Unable to create launch page`, `Source root resource is not a page` o `Mandatory parameter is missing`. (SITES-13085)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp2}

* Gli amministratori avevano visibilità limitata sull’elaborazione push-on-modify di MSM durante le modifiche al contenuto. La correzione aggiunge una registrazione dettagliata della ricezione e dell’esecuzione del rollout degli eventi MSM. L’output di debug ora mostra quali eventi sono stati attivati, quali percorsi di contenuto sono stati modificati e l’utente che ha attivato la modifica. (SITES-38029)
* AEM ha risolto un problema di layout di localizzazione nel campo data del rollout blueprint. Il prompt della data è ora adattato al controllo e rimane leggibile nelle lingue supportate, inclusa `fr_FR`. (SITES-14961)

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### Replica{#sites-replication-65-lts-sp2}

La pubblicazione dell’editor pagina ora gestisce gli URL contenenti selettori o suffissi. La richiesta pubblicata ora invia il percorso della pagina JCR, non una stringa URL di selettore o suffisso, pertanto l’attivazione viene completata e il contenuto viene attivato. La replica ora restituisce uno stato di errore in caso di errore, che impedisce la visualizzazione di falsi messaggi di “pubblicazione avviata”. (NPR-43288)

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### Editor modello{#sites-template-editor-65-lts-sp2}

Per alcune lingue, il testo dello stato del modello viene visualizzato in verticale in **Strumenti** > **Generale** > **Modelli**. L’etichetta “obsoleto” interrompeva il layout e veniva letta come una colonna di caratteri. La correzione corregge lo stile dello stato del modello in modo che l’etichetta esegua il rendering su una singola linea orizzontale. (SITES-36797)

#### Editor universale {#sites-universal-editor-65-lts-sp2}

* È stata impostata una configurazione predefinita OSGi come `preview=true` che ha forzato l’avvio dell’editor universale in modalità Anteprima. Questo aggiornamento corregge il valore predefinito e ripristina il comportamento standard della voce Produzione. L’editor universale ora si apre in modalità Produzione a meno che un amministratore non abiliti esplicitamente la modalità Anteprima. (SITES-37193)
* Per impostazione predefinita, il comando Apri editor universale è ora disponibile in modalità Anteprima negli ambienti di sviluppo e staging. Il comando aggiunge `preview=true`, che mantiene i controlli dell’autore allineati con il contesto di anteprima ed evita l’apertura accidentale della produzione. (SITES-33839)

### [!DNL Assets]{#assets-65-lts-sp2}

Correla risorse ora funziona per i nomi di file che includono spazi. La logica del client di correlazione aggiornata ora gestisce correttamente i percorsi contenenti spazi ed evita errori di origine `undefined` durante la selezione della relazione. La finestra di dialogo Correla ora consente di aprire e salvare le relazioni senza pulsanti o interruzioni dell’interfaccia utente. Gli utenti DAM possono correlare, derivare e annullare la correlazione delle risorse senza rinominare i file. (Assets-56418)

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* Nuova integrazione del lettore video Dynamic Media (rollout limitato) - Una nuova esperienza di lettore video Dynamic Media è ora disponibile in AEM 6.6 Quickstart. Questo miglioramento è attualmente abilitato solo per la clientela iniziale come parte di un rollout controllato. (Assets-60165)
* È stato risolto un problema nella finestra di dialogo delle proprietà video che impediva all’opzione Seleziona miniatura di aprire il selettore risorse, consentendo ora agli utenti di scegliere miniature personalizzate per le risorse video. (Assets-58926)
* Nei video Dynamic Media, è stato aggiunto il supporto per la selezione dell’arabo nell’elenco a discesa Lingua sottotitoli e tracce audio, consentendo agli autori di gestire i sottotitoli in arabo direttamente in AEM. (Assets-61771)

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->

<!--
#### Forms Designer
-->

### [!DNL Forms]{#forms-65-lts-sp2}

* Gli utenti hanno riscontrato problemi con la funzionalità `Data Source / Enter Keyword` dell’editor modello dati modulo (FDM). Questo problema influiva sulla capacità di ricerca e selezione delle origini dati. (FORMS-23971)
* Sui dispositivi mobili, il componente tabella nei moduli adattivi eseguiva il rendering di un’intestazione nascosta nella parte superiore, causando l’annuncio errato del contenuto da parte degli assistenti vocali. Il problema ha influito sugli utenti che affidano la navigazione agli assistenti vocali. (FORMS-23754)
* Gli utenti hanno riscontrato problemi con i moduli adattivi basati sui componenti core che fanno riferimento a tipi di risorse contrassegnati come granite:InternalArea, che hanno influito sulla funzionalità di diversi componenti granite nel componente aggiuntivo Moduli locale. (FORMS-23632)
* L’invio del modulo non riesce dopo l’aggiornamento a AEM 6.5 LTS SP1. Gli utenti hanno riscontrato la mancanza di com.adobe.cq.social.commons.CollabUtil, che ha causato errori di compilazione JSP e azioni di invio e-mail non riuscite. (FORMS-23457)
* Gli utenti hanno riscontrato problemi con la traduzione di hCaptcha non corretta nei moduli adattivi basati sui componenti di base. Questo ha influito sulla capacità degli utenti non anglofoni di compilare i moduli con precisione. (FORMS-23426)
* Gli utenti hanno riscontrato errori durante l’invio di un modulo con SAXParseException: “Il contenuto non è consentito nel prologo” (HTTP 500). Questo problema si verificava a causa di un valore null nel file XML dei dati di precompilazione, causando un errore di analisi XML lato server. (FORMS-22633)
* Gli utenti hanno riscontrato errori negli audit delle linee guida WCAG (Web Content Accessibility Guidelines) dei moduli adattivi. Il motivo era la non validità del markup di navigazione tramite schede del modulo. In altre parole, viene eseguito il rendering di un elemento non di elenco come figlio diretto di un elenco, in cui sono consentite solo le voci di elenco. Questo problema impediva al modulo di passare le convalide di accessibilità e influiva sulle organizzazioni che dovevano soddisfare i requisiti di conformità legali o interni. (FORMS-22101)
* Gli utenti hanno riscontrato problemi di accessibilità con il Documento record (DoR)/PDF di invio, in cui i campi modulo vuoti non venivano taggati come elementi del modulo. Questo ha causato difficoltà agli assistenti vocali, compromettendo la capacità degli utenti con disabilità di navigare e completare i moduli in modo efficace. (FORMS-21989)
* Gli utenti hanno riscontrato un problema che impediva la visualizzazione delle note a piè di pagina per i componenti all’interno di un pannello secondario durante il caricamento del modulo. Questo problema si verificava quando l’elemento con la nota a piè di pagina era l’ultimo componente della pagina. (FORMS-21925)
* Gli utenti hanno riscontrato problemi durante la selezione dei componenti nell’editor Moduli AEM. Durante la navigazione tra le schede e il ritorno alla prima scheda, alcuni contenitori non sono più selezionabili, impedendo una facile identificazione e interazione. (FORMS-21814)
* Gli utenti hanno riscontrato una vulnerabilità di sicurezza nel dashboard dei moduli adattivi. Nello specifico, nel file startpointcontrol.js è stato identificato un problema di vulnerabilità cross-site scripting (XSS) che potrebbe potenzialmente consentire l’esecuzione di script dannosi. (FORMS-20679)
* Nelle distribuzioni del cluster AEM Forms 6.5 LTS in JBoss® EAP 8, i file `domain/configuration/domain_oracle.xml`, `domain_mysql.xml` e `domain_mssql.xml` non contengono più un tag `<security>` duplicato che ha causato un XML non valido e ha impedito l’avvio del controller di dominio. (FORMS-24687)
* In modalità preconfigurata, l’aggiornamento della porta del database viene ora applicato correttamente durante la nuova installazione e l’aggiornamento. Nella nuova modalità di installazione, gli utenti possono selezionare da tutte le porte disponibili e in modalità di aggiornamento; durante il processo di aggiornamento la porta del database aggiornata in lc_turnkey.xml viene indicata correttamente. (FORMS-24689)
* Durante la configurazione di JBoss® EAP 8.0 su Linux®, gli script della shell modificati in Windows non causano più errori `/bin/sh^M: bad interpreter or $'\r': command not found` a causa delle terminazioni della riga CRLF. (FORMS-24688)
* Nelle implementazioni Forms JEE LTS in esecuzione su JBoss® EAP 8, l’interfaccia utente delle estensioni Reader potrebbe non riuscire e generare un errore interno del server. (FORMS-24894)
* Su Linux®, gli utenti hanno riscontrato problemi di runtime o distribuzione quando Forms JEE LTS Configuration Manager è stato eseguito con un valore `OSFileSetIntendedFor` non impostato o non corretto in `configurationManager/config/solcomp/LFS_Foundation.properties`, che ha impedito la personalizzazione della configurazione per Linux®. Dopo l&#39;installazione e prima di eseguire Configuration Manager, impostare `OSFileSetIntendedFor=Linux` in tale file. (FORMS-24741)

<!--
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

* La sicurezza Sling Resource Access è ora in esecuzione sulla versione 1.1.2. ResourceAccessSecurityImpl non genera più un’eccezione ClassCastException durante l’inizializzazione quando vengono registrati più servizi ResourceAccessGateHandler. L’inizializzazione viene ora completata in modo affidabile ed evita errori di avvio in ambienti con più gestori. (NPR-42750)
* Console JMX e console Web ora inviano un `Content-Type: text/css header` per le risorse CSS della console. Il controllo MIME rigoroso non blocca più il caricamento del foglio di stile, pertanto nell’interfaccia utente `/system/console/jmx` viene eseguito il rendering con uno stile normale. (GRANITE-63677)
* AEM ora evita di duplicare le voci ACL per il gruppo `contributor` nel `WEB-INF/resources/provisioning/model.txt` generato. L’output WAR ora contiene un blocco ACL coerente, che impedisce la confusione delle diverse autorizzazioni durante la revisione. (GRANITE-63269)
* AEM non cancella più le impostazioni dell’elenco Consentiti e dell’elenco Bloccati del firewall di deserializzazione durante le operazioni di aggiornamento del bundle. La logica di registrazione del filtro aggiornata mantiene l’istanza del firewall attiva allineata con la configurazione salvata, pertanto la protezione rimane abilitata senza riavviare il sistema. (GRANITE-61382)
* La console Web Felix non genera più errori `NullPointerException` intermittenti durante l’accesso a `/system/console`. La gestione ServiceTracker aggiornata impedisce uno stato di tracciamento null. La navigazione e l’accesso alla console rimangono stabili durante le richieste ripetute e la convalida automatizzata. (GRANITE-61042)

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

CRXDE Lite non mostra più una scheda vuota quando si apre un file JSP dopo un aggiornamento del Service Pack. AEM ora distribuisce il codice principale e aggiuntivo di CodeMirror corrispondente, evitando in tal modo l’errore del browser irreversibile e mantenendo l’editor utilizzabile. (GRANITE-64333)

#### Granite{#foundation-granite-65-lts-sp2}

Convalida sicurezza espressione ora gestisce valori di configurazione OSGi null o vuoti. Applica i valori predefiniti sicuri, ignora gli array vuoti e registra i registri di cancellazione, impedendo NullPointerException e risultati di convalida imprevedibili. (NPR-43163)

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### Integrazioni{#foundation-integrations-65-lts-sp2}

AEM ora sincronizza le attività di Adobe Target anche quando esistono date di inizio e di fine. Il payload di Target ora formatta le date dell’attività come marche temporali ISO 8601 complete, che includono secondi, millisecondi e fuso orario. Target non rifiuta più la richiesta con `InvalidJson.Json`. Le attività pianificate ora passano a uno stato sincronizzato invece di rimanere non sincronizzate. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 

#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS Service Pack 2 richiede il connettore S3 1.60.10 o versione successiva. La configurazione dell’archivio dati S3 ora include `crossRegionAccess` e `mode`, pertanto gli amministratori possono abilitare l’accesso al bucket tra aree geografiche e passare l’archiviazione a GCP quando necessario. `s3EndPoint` prevede ora un’area allineata a `s3Region` oppure rimane vuota in modo che il driver generi l’endpoint. (GRANITE-64873)


#### Quickstart{#foundation-quickstart-65-lts-sp2}

* Sling aggiorna l’elenco Consentiti per l’accesso amministrativo per utilizzare la terminologia inclusiva e i nuovi PID di configurazione. Questa modifica è allineata con Sling JCR Base 3.2.0. (GRANITE-63756)

  **Impatto**

   * Sling depreca questi PID e devi rimuoverli dalle configurazioni:
      * PID factory: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * PID globale: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
Queste configurazioni meno recenti utilizzano proprietà quali `whitelist.name` e `whitelist.bundles`.

   * Sling fornisce ancora una parziale compatibilità con le versioni precedenti per i PID obsoleti, ma non li utilizza per le nuove configurazioni. Utilizza invece i PID `LoginAdminAllowList.*` più recenti.
   * Non eseguire contemporaneamente configurazioni di elenco Consentiti nuove e obsolete. Configurazioni miste possono creare ambiguità e produrre comportamenti non desiderati. Quando esegui la migrazione a AEM 6.5 LTS SP2, rimuovi completamente i PID obsoleti.

  **Azioni possibili**

   1. Trova configurazioni di elenco Consentiti che utilizzano PID `LoginAdminWhitelist*`.
   1. Sostituiscili con i nuovi PID appropriati:

      * PID factory: `org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * PID globale: `org.apache.sling.jcr.base.LoginAdminAllowList`

      Per ulteriori dettagli, consulta [Approccio obsoleto ai bundle dell’elenco Consentiti per l’accesso amministrativo](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login).

* AEM 6.5 LTS SP2 aggiorna il bundle di livello base impostato per Sling, Oak e Felix. Questi aggiornamenti rafforzano la stabilità del runtime principale e allineano le versioni delle dipendenze in tutta la piattaforma. (GRANITE-61874)

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311)
-->

#### Sling{#foundation-sling-65-lts-sp2}

AEM ora include Sling Engine 2.16.6. Questa modifica elimina le violazioni XSS segnalate dagli strumenti di sicurezza e migliora la sicurezza e la stabilità del rendering di base. (NPR-43105)

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

AEM Translations non genera più errori in Java 17 o Java 21 a causa di problemi di formato XLIFF. La pipeline di esportazione ora produce XLIFF conformi agli standard accettati dai provider di traduzione. Questa modifica rimuove le interruzioni del lavoro di traduzione e ripristina un handoff prevedibile tra AEM e i servizi di traduzione. I flussi di lavoro di traduzione ora rimangono stabili nei runtime Java supportati. (CQ-4360217)

#### Flusso di lavoro{#foundation-workflow-65-lts-sp2}

EmailNotificationService-Processor non attiva più errori ripetuti di tipo “Segmento non trovato” durante la gestione delle notifiche del flusso di lavoro. La gestione delle eccezioni aggiornata rileva SegmentNotFoundException e interrompe il ciclo di elaborazione invece di continuare con letture non valide. L’esecuzione del flusso di lavoro rimane stabile e il rumore del registro diminuisce durante l’accesso all’elemento di lavoro e alla casella in entrata. (GRANITE-62635)




## Informazioni su [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 LTS si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e dell’archivio dei contenuti Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x è utilizzato come motore servlet per Quickstart.

### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituisci i valori predefiniti del GC (catalogo globale) con altri valori. Per ulteriori informazioni, consulta la sezione [Installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuisce gli aggiornamenti di manutenzione Java™ 17 e Java™ 21 per l’utilizzo da parte del cliente nei progetti correlati ad AEM, se non disponibili pubblicamente da Oracle.

### Pacchetto Uberjar {#uber-jar-packaging}

Il pacchetto UberJar per AEM 6.5 LTS SP2 utilizza la versione AEM 6.5 LTS UberJar 6.6.2. Puoi recuperare gli artefatti UberJar corrispondenti dall’archivio centrale Maven. A differenza di AEM 6.5, AEM 6.5 LTS separa le API pubbliche e quelle obsolete in due artefatti diversi.

Per eseguire la compilazione in base alle API pubbliche, utilizza quanto segue:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

Se il codice dipende anche da API obsolete, aggiungi quanto segue:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

Consulta anche [Aggiornare la versione Uber Jar Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Aggiornamento {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).
* Per istruzioni sull’aggiornamento dettagliate, consulta la [Guida all’aggiornamento per AEM Forms 6.5 LTS SP1 su JEE](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

#### Best practice per gli aggiornamenti del Service Pack di AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**Ambiente**
Si applica a: clientela AEM 6.5 LTS (locale) che installa il Service Pack 2 (SP2). SP2 viene fornito come file Quickstart JAR.

**Perché questo aggiornamento è importante**
SP2 per AEM 6.5 LTS viene fornito come file Quickstart JAR anziché come file ZIP da installare tramite il gestore di pacchetti. I clienti on-premise possono eseguire l’aggiornamento sostituendo il file Quickstart JAR, decomprimendolo e riavviandolo. Questo metodo è coerente con la procedura di aggiornamento diretto di Adobe.

**Flusso di aggiornamento consigliato (authoring o pubblicazione)**

1. Verifica che l’istanza AEM 6.5 LTS sia integra e accessibile.
1. Scarica il file Quickstart JAR (ad esempio, `cq-quickstart-6.6.x.jar`) dalla distribuzione del software.
1. Arresta l&#39;istanza in esecuzione.
1. Nella directory di installazione di AEM (esterna a `crx-quickstart/`), sostituisci il file Quickstart JAR precedente con il file JAR SP2.
1. Decomprimi il file JAR:

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (Regola i flag dell&#39;heap in base alle esigenze).

1. Rinomina il file JAR decompresso in modo che corrisponda al ruolo e alla porta, ad esempio `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Avvia AEM e conferma l’aggiornamento nell’interfaccia utente (Guida > Informazioni) e nei registri.

**Buone pratiche**

* Esegui l’aggiornamento in ambienti di test o inferiori prima di eseguirlo in ambienti di produzione.
* Prima di iniziare, esegui backup completi e ripristinabili (archivio più eventuali datastore esterni).
* Consulta la guida all’aggiornamento diretto di Adobe e i requisiti tecnici (consigliato Java 17/21 per LTS).

>[!NOTE]
>
>I nomi dei file mostrati sopra (ad esempio, `cq-quickstart-6.6.x.jar`) riflettono la denominazione dell’artefatto Quickstart di questa versione LTS; utilizza sempre lo stesso nome di file scaricato dalla distribuzione del software.

## Installazione e aggiornarnamento{#install-update}

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

Adobe rivede continuamente le funzionalità del prodotto per offrire un valore aggiunto al cliente modernizzando o sostituendo le funzioni meno recenti. Queste modifiche vengono implementate prestando particolare attenzione alla compatibilità con le versioni precedenti.

Per garantire trasparenza e consentire una pianificazione adeguata, Adobe segue questo processo di deprecazione per Adobe Experience Manager (AEM):

* La deprecazione viene annunciata per prima. Le funzionalità obsolete rimangono disponibili ma non vengono più migliorate.
* La rimozione si verifica non prima della versione principale successiva. La timeline della rimozione pianificata viene comunicata separatamente.
* Prima della rimozione di una funzionalità, alla clientela è fornito almeno un ciclo di rilascio per la transizione alle alternative supportate.

### Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità che Adobe ha dichiarato obsolete in AEM 6.5 LTS. In genere, Adobe depreca le funzioni prima di rimuoverle in una versione futura e fornisce un’alternativa.

Si consiglia alla clientela di rivedere l’utilizzo o meno della funzione/funzionalità nell’implementazione corrente. Si consiglia inoltre di pianificare la modifica dell’implementazione adottando l’alternativa fornita.

| Area | Funzione | Sostituzione | Versione (SP) |
| --- | --- | --- | --- |
| Quickstart | API Mongo | Le API Mongo ora sono obsolete e la loro rimozione è pianificata per le versioni future. | 6.5 TS SP2 |
| Sites | Supporto ai frammenti di contenuto nell’API REST di AEM Assets | AEM 6.5 LTS SP2 fornisce OpenAPI moderne per la gestione dei modelli e frammenti di contenuto, pertanto gli endpoint precedenti per il supporto dei frammenti di contenuto nell’API REST di AEM Assets sono ora obsoleti.<br>Adobe intende mantenere questi endpoint precedenti disponibili fino a un annuncio di fine del ciclo di vita. Adobe non pianifica ulteriori miglioramenti per gli endpoint obsoleti. | 6.5 LTS SP2 |
| Sites | [Editor SPA](/help/sites-developing/spa-overview.md) | Gli editor preferiti per la gestione dei contenuti headless in AEM sono:<br>- [l’editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.<br>- [L’editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per modifiche basate sul modulo. | 6.5 LTS GA |
| [!DNL Foundation] | Supporto per com.adobe.granite.oauth.server | Integrazione di Adobe IMS |  |

### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità e le funzioni che sono state rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

* Il supporto per RDBMK per la persistenza dell’archivio CRX è stato rimosso.
* Negli ambienti cluster, MongoMK è ora l’unica opzione supportata per la persistenza dell’archivio.

| Area | Funzione | Sostituzione | Versione (SP) |
| --- | --- | --- | --- |
| Commerce | AEM CIF Classic non è supportato. | Esegui la migrazione a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluzioni | Social network e Communities non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
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

### AEM Forms

* In Gestione configurazioni, l’inizializzazione del database non riesce durante l’avvio in modalità personalizzata preconfigurata di AEM Forms 6.5 LTS JEE quando non è selezionato alcun modulo o sono selezionati solo componenti limitati. L’errore è dovuto a una dipendenza mancante (xalan-2.7.2.jar), che determina un errore. L’aggiunta del file JAR a adobe-livecycle-jboss.ear\lib risolve il problema. (FORMS-24690)
* In Forms JEE LTS in esecuzione su JBoss®, le funzionalità correlate all’e-mail potrebbero non riuscire. Quando si tenta di utilizzare le funzionalità di posta elettronica, il server registra un errore: `Error IMAPProvider not a subtype`. (FORMS-24892)
* Nelle implementazioni di Forms JEE LTS Service Pack 2 in esecuzione su WebSphere® Liberty Profile, la funzionalità e-mail potrebbe non riuscire. Quando si tenta di utilizzare le funzionalità di posta elettronica, il server registra un errore: `Could not convert socket to TLS`. (FORMS-24692)

### Danneggiamento dell’archivio durante la compattazione online dopo la compattazione offline (GRANITE-65146) {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

Gli utenti possono riscontrare un danneggiamento dell’archivio durante la compattazione online se in precedenza era stata eseguita la compattazione offline nell’archivio JCR. In questo scenario può verificarsi un `SegmentNotFoundException` (SNFE) che può danneggiare l’archivio.

Per risolvere il problema, installa l’hotfix dalla [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip). Poiché l’hotfix include un bundle `oak-segment-tar` di basso livello, l’istanza viene riavviata dopo l’installazione.

Pianifica i tempi di inattività dell’istanza durante la sua applicazione. Per la compattazione offline, utilizza il file jar [`oak-run`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar) corrispondente, disponibile anche in Distribuzione software.

>[!NOTE]
>
> * Per qualsiasi operazione `oak-run`, utilizza il file jar [`oak-run` 1.88.1-B006](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar).
>
> * Avvia AEM impostando la proprietà di sistema `oak.compaction.legacy=true`.

### Bundle `com.adobe.granite.apicontroller` mancante in AEM 6.5 LTS SP2 (GRANITE-67640) {#missing-apicontroller-bundle-granite-67640}

Il bundle `com.adobe.granite.apicontroller` non è presente in AEM 6.5 LTS SP2. Questo bundle controlla come vengono risolti i bundle OSGi e può impedire la risoluzione dei bundle in altri bundle, il che è utile per limitare le API esposte.

Installa l&#39;aggiornamento rapido da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip) per utilizzare questa funzionalità.

>[!NOTE]
>
> Dopo aver installato l&#39;hotfix, verificare lo stato del bundle di tutti i bundle installati per assicurarsi che la configurazione predefinita di `com.adobe.granite.apicontroller` non abbia introdotto restrizioni di risoluzione non intenzionali che potrebbero influire sulle implementazioni personalizzate esistenti.

### Commenti JSON non più supportati in Sling-Initial-Content (SP2) {#json-comments-no-longer-supported-in-sling-initial-content}

Questo problema riguarda sviluppatori e amministratori di bundle OSGi che implementano bundle che utilizzano `Sling-Initial-Content` con file JSON.

A partire da AEM 6.5 LTS SP2, i file JSON utilizzati nei bundle `Sling-Initial-Content` non accettano più commenti (`//` o `/* */`). Le versioni precedenti di AEM accettavano i commenti perché il provider `javax.json` era indulgente al riguardo. AEM 6.5 LTS SP2 ha aggiornato `org.apache.sling.jcr.contentloader` alla versione 2.6.0, cambiando il parser JSON in `jakarta.json`. Sebbene la [specifica JSON (RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259) non definisca la sintassi per i commenti, erano accettati nelle versioni precedenti di AEM grazie all’indulgenza del provider `javax.json`. Il provider `jakarta.json` non offre questa estensione.

L’errore è invisibile all’utente: i nodi di contenuto non vengono caricati all’attivazione del bundle e il programma di installazione non visualizza alcun messaggio di errore. Se manca inaspettatamente del contenuto dopo l’aggiornamento a SP2, controlla i registri del programma di installazione di OSGi per verificare la presenza di errori di analisi JSON. Per identificare i bundle interessati, cerca `//` o `/* */` all’interno dei file JSON elencati nelle intestazioni manifesto di `Sling-Initial-Content`.

>[!CAUTION]
>
> Rimuovi tutti i commenti dai file JSON nei bundle `Sling-Initial-Content` per evitare errori di caricamento del contenuto dopo l’aggiornamento ad AEM 6.5 LTS SP2.

### Installa gli indici Oak richiesti per le API headless di Sites{#site-headless-api}

Alcune API che sono state spostate in Sites Headless richiedono indici Oak aggiuntivi per garantire la piena funzionalità.

Installa il pacchetto `cq-dam-cfm-indices` per utilizzare le funzionalità seguenti:

* Elenco modelli per frammenti di contenuto
* Elenco frammenti di contenuto
* Ricerca API
* Flussi di lavoro

Scarica il pacchetto di indice [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip) dal portale di distribuzione software di Adobe.

### Errore di connessione di Dispatcher con la funzione solo SSL (risolto in AEM 6.5 LTS SP1 e versioni successive){#ssl-only-feature}

>[!NOTE]
>
> Questo problema è presente solo nella versione AEM 6.5 LTS GA.

Quando si abilita la funzione solo SSL nelle implementazioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze Dispatcher e AEM. Dopo aver abilitato questa funzione, le verifiche stato potrebbero non riuscire e la comunicazione tra le istanze Dispatcher e AEM potrebbe essere interrotta. Questo problema si verifica in modo specifico quando i clienti tentano di connettersi tramite `https + IP` dalle istanze Dispatcher ad AEM. È correlato a problemi di convalida SNI (Server Name Indication).

**Impatto**

* Errori di verifica integrità con codici di risposta HTTP 400.
* Traffico interrotto tra istanze Dispatcher e AEM.
* Il contenuto non può essere gestito correttamente tramite Dispatcher.
* Errori di connessione durante l’utilizzo di HTTPS con indirizzi IP nella configurazione di Dispatcher.
* HTTP 400: errori “SNI non valida” durante la connessione tramite HTTPS + IP.

**Ambienti interessati**

* Implementazioni di AEM con configurazioni Dispatcher.
* Sistemi in cui è stata abilitata la funzione solo SSL.
* Configurazioni di Dispatcher che utilizzano il metodo di connessione `https + IP` per le istanze AEM.

**Soluzione**

Se riscontri questo problema, contatta l’Assistenza Clienti di Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip). Non tentare di abilitare le funzioni solo SSL finché non viene applicato l’hotfix necessario.

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

I seguenti file zip contengono i documenti di testo che elencano i bundle OSGi e i pacchetti di contenuti inclusi in questa versione del Service Pack Experience Manager 6.5 LTS:

* [Bundle OSGi](/help/release-notes/assets/65lts_sp2_bundles.zip)
* [Pacchetti di contenuti](/help/release-notes/assets/65lts_sp2_packages.zip)

## Siti web con restrizioni{#restricted-sites}

Questi siti web sono disponibili solo per la clientela. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/it/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience).

