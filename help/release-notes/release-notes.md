---
title: Note sulla versione corrente per Adobe Experience Manager 6.5 LTS, SP3
description: Trova informazioni sulla versione corrente per Adobe Experience Manager 6.5 LTS, Service Pack 3.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: aa819778006a3acb0d02772156c2af820ed353bb
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 23%

---


# Note sulla versione corrente per Adobe Experience Manager 6.5 LTS, SP3 {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| Versione | Service Pack 3 (SP3) <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 20 agosto 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione del software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.3.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

<!-- **Mandatory Hotfix** – To avoid SNFE (SegmentNotFoundException) issues with offline compaction when installing SP2, install the hotfix described in [Known issues – Repository corruption during online compaction](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146). -->

## Cosa è incluso in [!DNL Adobe Experience Manager] 6.5 LTS, SP3 {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS, SP3 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Migliora le prestazioni, la sicurezza e la localizzazione in tutta la piattaforma dalla disponibilità iniziale di 6.5 LTS nel marzo 2025. [Installare il Service Pack](#install-update) su 6.5 LTS.

### Panoramica sui problemi risolti {#fixed-issues-overview}

[!DNL Adobe Experience Manager] 6.5 LTS, SP3 risolve i problemi in [!DNL Sites] e [!DNL Experience Manager Foundation]. Le correzioni apportate migliorano l’accessibilità, l’affidabilità dell’authoring, la distribuzione di contenuti headless, la gestione multisito e la stabilità della piattaforma. Nelle sezioni che seguono viene elencata ogni correzione con il relativo numero di riferimento.

La maggior parte delle modifiche si applica a [!DNL Sites]:

* Miglioramenti dell’accessibilità dal gruppo più ampio. Gli aggiornamenti migliorano la navigazione da tastiera, il feedback degli assistenti vocali, la gestione dell’attivazione, il markup semantico, il contrasto del testo e il dimensionamento del target touch nell’Editor pagina, nella barra laterale di Assets, nei filtri e nelle relative interfacce di authoring.
* Le correzioni in [!DNL Content Fragments] interessano l&#39;Editor frammento di contenuto, l&#39;Editor modelli, l&#39;API REST e l&#39;API GraphQL. Gli aggiornamenti correggono la localizzazione, la convalida dei campi, il comportamento di modifica e la gestione della risposta.
* Le correzioni delle Live Copy MSM consentono agli autori di implementare le modifiche in modo affidabile dalle pagine blueprint e di mantenere la configurazione di rollout esistente.
* Il supporto Crosswalk è disponibile su Adobe Managed Services, inclusi i bundle richiesti, gli utenti del sistema e la configurazione.
* Sono state apportate ulteriori correzioni alle interfacce classica e di amministrazione, ai componenti core, alla console Componenti, all’integrazione di Campaign, ai frammenti di esperienza e ai lanci.

Le modifiche rimanenti si applicano a [!DNL Experience Manager Foundation]:

* Gli aggiornamenti di localizzazione traducono in precedenza testo in lingua inglese nei rapporti di stato, nella console Operazioni e in diverse interfacce di authoring.
* Le correzioni di stabilità ripristinano l’endpoint di monitoraggio dello stato, mantengono il servizio di posta in esecuzione dopo errori di configurazione intermittenti e correggono la variabile di flusso di lavoro e la modifica del pacchetto di flusso di lavoro.
* Questa versione aggiunge anche il supporto di AEM Context Service e risolve problemi di sicurezza, traduzione e interfaccia utente.

Per l&#39;elenco completo, vedere [Problemi risolti in 6.5 LTS, Service Pack 3](#fixed-issues).


<!-- ## Key features and enhancements -->



<!-- UPDATE THE EACH RELEASE -->

## Sono stati risolti i problemi in 6.5 LTS, Service Pack 3 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP3}

* AEM 6.5 LTS, Service Pack 3 include i bundle Crosswalk, il pacchetto di contenuti, gli utenti del sistema, le mappature servizio-utente, gli interruttori delle funzioni e la configurazione OSGi richiesta. Le nuove installazioni forniscono automaticamente i prerequisiti di Crosswalk e richiedono solo la configurazione runtime specifica del cliente. (SITES-41596)
* AEM 6.5 LTS, Service Pack 3 aggiorna `cq-wcm-core` per supportare il Crosswalk su Adobe Managed Services. L’aggiornamento aggiunge la creazione del modello e l’accesso all’editor universale, rimuovendo al contempo i tag di funzionalità e codice personalizzato obsoleti. (SITES-37657)


#### Accessibilità {#sites-accessibility-65-lts-sp3}

* L’area di lavoro dell’Editor pagina ora supporta la gestione dei componenti solo da tastiera. Gli autori possono utilizzare Inserisci componente, Taglia, Incolla ed Elimina per aggiungere, riordinare e rimuovere componenti. (SITES-25359) CRITICO
* Gli utenti che utilizzano la tastiera ora possono riordinare le righe della tabella nella Vista a elenco Sites senza utilizzare i gesti di trascinamento della selezione. I controlli da tastiera consentono agli utenti di selezionare una riga, spostarla in un’altra posizione e completare il posizionamento. (SITES-24946) CRITICO

* L’editor delle proprietà personalizzate ora supporta l’interazione da tastiera con i relativi controlli di formattazione. Gli autori possono spostare lo stato attivo tra le opzioni della barra degli strumenti, selezionare uno stile di testo e formattare i valori delle proprietà utilizzando solo una tastiera. (SITES-40333) PRINCIPALE

* L’attivazione tramite tastiera ora ignora l’elenco dei componenti del pannello laterale quando l’interazione disponibile richiede il trascinamento della selezione. Questa modifica impedisce agli utenti che utilizzano la tastiera di accedere a un flusso di lavoro inutilizzabile per la selezione dei componenti. (SITES-40752)
* La chiusura di una sovrapposizione ora ripristina lo stato attivo sul relativo controllo di attivazione. Gli utenti che utilizzano la tastiera o l’assistente vocale non tornano più alla sovrapposizione o perdono la loro posizione nell’interfaccia. (SITES-40819)
* La navigazione tramite tastiera non sposta più lo stato attivo sul contenuto della pagina nascosta. Questa modifica mantiene una sequenza di attivazione prevedibile ed evita interruzioni della navigazione. (SITES-41430)
* Il pulsante Blocca fornisce ora un feedback preciso sull’utilità di lettura dello schermo in base al titolo. Gli utenti sentono un’etichetta di azione chiara invece di una descrizione lunga. (SITES-41431)
* Un indicatore visivo identifica ora l&#39;opzione selezionata nella casella di riepilogo Cambia file o cartella. L’indicatore aiuta gli utenti a comprendere il percorso della breadcrumb e a riconoscere la cartella corrente. (SITES-25532)
* Gli assistenti vocali ora annunciano una volta la direzione di ordinamento crescente o decrescente. Un’etichetta descrittiva identifica chiaramente l’azione del pulsante e rimuove il feedback duplicato. (SITES-25534)
* AEM Sites ora fornisce un supporto più ampio per l’accessibilità in tutti i flussi di lavoro di authoring comuni. Gli aggiornamenti migliorano l’interazione della tastiera, le etichette dell’interfaccia, la gestione dell’elemento attivo e il feedback sulla tecnologia per l’accessibilità. (SITES-38239)
* Gli elementi della barra degli strumenti ora visualizzano le etichette visibili quando ricevono lo stato attivo da tastiera. Gli utenti che utilizzano la tastiera possono identificare ogni controllo prima di attivarlo. (SITES-40751)
* Gli utenti che utilizzano la tastiera o l’utilità di lettura dello schermo possono ora uscire dal menu Posta in arrivo senza lasciarlo aperto. Il menu si chiude automaticamente e mantiene un percorso di navigazione chiaro. (SITES-25518)
* Nei campioni colore viene ora visualizzata un&#39;icona con lo stato selezionato e un contrasto sufficiente. L&#39;indicatore più chiaro consente agli utenti di riconoscere il campione attivo in diversi colori di sfondo. (SITES-25523)
* La barra degli strumenti Modifica layout segnala ora con precisione il dispositivo corrente alla tecnologia per l’accessibilità. I pulsanti del dispositivo non suggeriscono più che gli utenti possano accendere e spegnere ogni pulsante. (SITES-25524)
* Il modale di ricerca ora visualizza l&#39;etichetta **Ordina per** con un contrasto di testo sufficiente. Lo stile aggiornato migliora la leggibilità per gli utenti ipovedenti. (SITES-25531)
* I pulsanti di ordinamento Visualizzazione elenco siti ora soddisfano i requisiti minimi di contrasto. Gli utenti possono identificare più facilmente ogni controllo di ordinamento e il relativo stato sullo sfondo della tabella. (SITES-25372)
* L’elenco Assets della barra laterale non viene più ricaricato quando il campo Filtro viene attivato dalla tastiera. Gli utenti possono accedere al campo senza spostamenti imprevisti dei contenuti o ripetuti annunci di caricamento degli assistenti vocali. (SITES-25377)
* Le schede della barra laterale dei frammenti di contenuto ora forniscono etichette accessibili coerenti. NVDA annuncia il nome della scheda invece di annunciare l&#39;elemento di navigazione secondario selezionato. (SITES-25509)
* Il menu Aiuto ora si chiude quando la tastiera o l&#39;utilità di lettura dello schermo si sposta al di fuori di esso. Gli utenti possono continuare a navigare nei controlli dell’intestazione o nel contenuto della pagina senza lasciare aperto il menu. (SITES-25517)
* Il testo immesso nei campi della barra degli strumenti Demografia ora soddisfa i requisiti di contrasto minimi. Gli utenti possono leggere i valori del profilo più chiaramente sullo sfondo del campo di testo. (SITES-25318)
* Il menu Informazioni pagina ora visualizza le opzioni attivate con un contrasto di testo sufficiente. Grazie a uno stile più chiaro, gli utenti possono tenere traccia della messa a fuoco della tastiera in tutto il menu. (SITES-25321)
* Le caselle di controllo nelle finestre di dialogo Teaser, Immagine e Carosello ora espongono le relative istruzioni agli assistenti vocali. Gli utenti sentono la descrizione di supporto quando lo stato attivo della tastiera raggiunge ogni casella di controllo. (SITES-25364)
* I controlli dell’editor di testo ora comunicano il loro stato corrente alle tecnologie per l’accessibilità. Gli assistenti vocali identificano il formato di paragrafo attivo e l&#39;opzione di destinazione del collegamento ipertestuale selezionata. (SITES-25367)
* Gli assistenti vocali ora annunciano chiaramente il pulsante **Ruota dispositivo** e l&#39;orientamento corrente del dispositivo. L&#39;attivazione del controllo riporta il nuovo orientamento senza utilizzare un&#39;etichetta che descriva l&#39;azione opposta. (SITES-25292)
* La navigazione tramite tastiera ora ignora i controlli nascosti nella barra degli strumenti Demografia compressa. Gli utenti possono spostarsi nell’Anteprima layout senza incontrare opzioni della barra degli strumenti non disponibili. (SITES-25304)
* Le etichette di testo nella barra degli strumenti Demografia ora soddisfano i requisiti di contrasto minimo durante l’anteprima del layout. Gli utenti possono leggere più chiaramente etichette come Consigliato sullo sfondo della barra degli strumenti. (SITES-25307)
* La barra degli strumenti Demografia ora visualizza gli indicatori di focus dei pulsanti con un contrasto sufficiente. Gli utenti possono identificare il controllo Commerce, Persona o Device attivo durante la navigazione da tastiera. (SITES-25308)
* La barra degli strumenti Modifica layout utilizza un indicatore di stato attivo raggruppato per il selettore di dispositivi. La struttura include i controlli **Seleziona dispositivo** e **Ruota dispositivo** correlati come parte del comportamento previsto della barra degli strumenti. (SITES-25283)
* La barra degli strumenti Modifica layout non troncerà più l&#39;etichetta **iPhone 8 Plus** quando gli utenti selezioneranno un altro dispositivo. Il nome completo del dispositivo rimane visibile in tutti gli stati dei pulsanti. (SITES-25284)
* Il righello Modifica layout ora fornisce contesto di misurazione agli assistenti vocali. Gli utenti sentono un’etichetta descrittiva e il formato di misurazione invece di una serie di numeri inspiegabile. (SITES-25287)
* La barra degli strumenti Modifica layout evidenzia il pulsante **Desktop** quando è attiva la visualizzazione desktop. L&#39;indicatore visivo rende chiara la selezione del dispositivo corrente. (SITES-25290)
* Lo stato attivo sulla tastiera ora rimane visibile sul pulsante campione in tutti i colori disponibili. L&#39;aggiunta della spaziatura impedisce che l&#39;indicatore di stato attivo si fonda nel campione selezionato. (SITES-25253)
* Gli assistenti vocali ora identificano correttamente il campo Data timewarp. Il campo non fornisce più un feedback fuorviante che suggerisce di aprire una finestra di dialogo. (SITES-25263)
* L&#39;etichetta del pulsante Annotazione ora soddisfa i requisiti di contrasto minimo negli stati predefiniti e al passaggio del mouse. Gli utenti possono leggere chiaramente l’etichetta sullo sfondo del pulsante. (SITES-25267)
* Gli assistenti vocali ora visualizzano etichette significative per i controlli nella finestra di dialogo Annotazione. Ogni pulsante comunica la propria azione senza un prefisso di annotazione non necessario. (SITES-25277)
* Il pulsante Modifica nella barra laterale di Assets ora fornisce un target touch più grande. Gli utenti possono attivare il controllo in modo più affidabile senza selezionare un elemento nelle vicinanze. (SITES-25221)
* L’Editor pagina ora utilizza una gerarchia di intestazioni logica. Gli assistenti vocali identificano il titolo della pagina come intestazione principale e i titoli della barra laterale come intestazioni subordinate. (SITES-25222)
* La finestra di dialogo Annotazione ora espone il titolo come intestazione semantica. Gli utenti che usano un’utilità di lettura dello schermo possono identificare il titolo e navigare nella struttura della finestra di dialogo attraverso i comandi di intestazione. (SITES-25248)
* Gli utenti screen reader ricevono ora un feedback quando filtrano l’elenco Inserisci nuovo componente. Il campo di ricerca descrive il relativo comportamento di filtro e un messaggio di stato riporta il conteggio dei risultati. (SITES-25251)
* Il pannello Componenti della barra laterale ora utilizza il markup dell’elenco semantico. Gli assistenti vocali possono annunciare il conteggio delle voci e supportare una navigazione efficiente dell’elenco. (SITES-25214)
* I pulsanti Info ora utilizzano icone più grandi nel pannello Componenti. Gli utenti possono individuare e riconoscere più facilmente ogni controllo. (SITES-25217)
* I titoli dei componenti ora rimangono visibili quando gli utenti aumentano la spaziatura del testo. I titoli lunghi vanno a capo invece di essere troncati o sovrapposti a contenuti vicini. (SITES-25219)
* Il pulsante **Modifica** della barra laterale di Assets ora indica che verrà aperta una nuova scheda del browser. I suggerimenti visivi e di lettura dello schermo preparano gli utenti prima della navigazione. (SITES-25220)
* La modalità Annotazione consente ora di attivare la tastiera sulla barra degli strumenti delle annotazioni quando questa si apre. Gli utenti che utilizzano la tastiera e l&#39;utilità di lettura dello schermo possono spostarsi tra i controlli in una sequenza logica senza spostarsi all&#39;indietro dal pulsante **Chiudi**. (SITES-24996)
* I pulsanti di selezione per i campi Percorso e Tag non utilizzano più un&#39;icona di casella di controllo. L&#39;icona aggiornata mostra che il controllo apre una finestra di dialogo di selezione anziché modificare uno stato selezionato. (SITES-25210)
* Il campo Filtro nel pannello Componenti della barra laterale ora dispone di un’etichetta accessibile valida. Gli assistenti vocali annunciano lo scopo del campo invece di fare affidamento su un’icona o su un testo segnaposto. (SITES-25212)
* La barra laterale di Assets ora nasconde le miniature decorative agli assistenti vocali. Gli utenti non sentono più il nome della risorsa due volte quando navigano nella griglia delle risorse. (SITES-25213)
* I pulsanti a soffietto nella barra Filtri ora visualizzano gli indicatori di messa a fuoco con un contrasto sufficiente. Gli utenti di tastiera possono tenere traccia dello stato attivo durante la navigazione nelle categorie dei filtri. (SITES-24986)
* Nella barra Filtri viene ora visualizzato lo stato attivo della tastiera intorno ai pulsanti di scelta. L’aumento del contrasto consente agli utenti di tenere traccia della loro posizione tra le opzioni di filtro. (SITES-24987)
* Il caricamento dei messaggi di stato sulla pagina Filtri ora soddisfa i requisiti minimi di contrasto del testo. Gli utenti possono leggere il feedback sull’avanzamento durante il passaggio dalla vista a schede alla vista a elenco. (SITES-24991)
* Il titolo della pagina nell’area di lavoro dell’editor ora utilizza il markup di intestazione semantica. Le tecnologie per l’accessibilità possono annunciare il titolo e includerlo nell’intestazione della navigazione. (SITES-24993)
* L’espansione del menu Emulatore ora sposta lo stato attivo sulla tastiera sulla prima voce di menu. La compressione del menu mantiene lo stato attivo all’interno della sequenza logica secondaria della barra degli strumenti. (SITES-24954)
* Il testo nella tabella Vista dal vivo soddisfa ora i requisiti minimi di contrasto. Gli utenti possono leggere chiaramente i dettagli della Live Copy durante gli stati normali e al passaggio del mouse. (SITES-24956)
* La barra Riferimenti ora utilizza per il titolo il markup dell’intestazione semantico. Gli assistenti vocali annunciano l’intestazione durante il caricamento iniziale e mentre gli utenti sfogliano le cartelle. (SITES-24967)
* I link alle carte descrivono ora chiaramente le loro destinazioni. Chi usa un assistente vocale può identificare ogni collegamento senza ascoltare i metadati completi della scheda. (SITES-24975)
* I pulsanti del menu intestazione non segnalano più agli assistenti vocali che aprono le finestre di dialogo. Gli assistenti vocali invece annunciano lo stato espanso o compresso di ogni pulsante, che descrive con precisione il comportamento del menu. (SITES-24742)
* Il testo sul pulsante Elimina ora offre un contrasto sufficiente rispetto allo sfondo rosso. Gli utenti possono identificare l’azione più facilmente prima di confermarne l’eliminazione. (SITES-24772)
* Le schede Canvas non espongono più collegamenti immagine e intestazione separati che conducono alla stessa destinazione. Un singolo collegamento riduce le interruzioni della tastiera duplicate e gli annunci ripetuti degli assistenti vocali. (SITES-24947)
* In Vista a elenco ora viene visualizzato il pulsante di trascinamento con maggiore visibilità. Le dimensioni, lo spessore e il contrasto aggiornati dell&#39;icona facilitano l&#39;individuazione e l&#39;utilizzo del controllo. (SITES-24951)
* I pulsanti di intestazione ora forniscono nomi accessibili concisi: Ricerca, App, Guida, Casella in entrata e Utente. Gli assistenti vocali non annunciano più termini ridondanti come &quot;cliccabile&quot; o &quot;grafico&quot; durante la navigazione da tastiera. (SITES-24715)
* I collegamenti in Navigazione app ora presentano un’enfasi visiva maggiore. L&#39;aumento delle dimensioni e del peso del testo migliora la leggibilità per gli utenti ipovedenti o con differenze nella visione dei colori. (SITES-24723)
* I collegamenti della casella in entrata ora utilizzano il markup di elenco semantico. Gli assistenti vocali possono identificare i collegamenti come un gruppo correlato, annunciare il conteggio degli elementi e supportare una navigazione più efficiente. (SITES-24730)
* Nella finestra di dialogo Preferenze utente, i controlli di suggerimento ora espongono nomi descrittivi accessibili. Gli assistenti vocali annunciano lo scopo di ogni controllo invece di dire &quot;vuoto&quot; prima di leggere il contenuto della descrizione. (SITES-24732)
* Ogni punto di riferimento della barra dei filtri ora include un’etichetta accessibile univoca. Gli assistenti vocali possono distinguere la Barra dei filtri dalle altre aree della pagina e identificarla durante la navigazione. (SITES-24686)
* Le finestre di dialogo dell&#39;editor ora separano i pulsanti Guida in linea e Attiva/Disattiva schermo intero dall&#39;elemento intestazione. Gli assistenti vocali identificano accuratamente questi controlli interattivi e non li annunciano più come intestazioni. (SITES-24696)
* Il pulsante Rapporto CSV ora avvisa gli utenti prima di aprire una nuova scheda del browser. La relativa etichetta accessibile comunica il comportamento agli utenti di utilità di lettura dello schermo e tastiera prima dell’attivazione. (SITES-24704)
* La Barra dei filtri ora carica le etichette per Ricerche salvate e Seleziona directory di ricerca in modo coerente. Il pulsante Filtri non inserisce più elementi etichetta durante le interazioni con lo stato attivo, la tastiera o il mouse. (SITES-24706)
* I pulsanti Chiudi e Rimuovi posizione ora forniscono destinazioni touch più grandi. Gli utenti possono attivare entrambi i controlli in modo più affidabile senza selezionare elementi adiacenti. (SITES-24530)
* Il pulsante Remove Location (Rimuovi posizione) e il relativo indicatore di messa a fuoco ora soddisfano i requisiti di contrasto minimo. Un contrasto più elevato consente agli utenti di identificare il controllo e tenere traccia della messa a fuoco della tastiera. (SITES-24531)
* Gli iframe dell’editor ora includono titoli descrittivi nell’area di lavoro, barre laterali, finestre di dialogo dei componenti e anteprima del layout. Gli assistenti vocali possono identificare ogni fotogramma quando lo stato attivo entra. (SITES-24650)
* Il contrasto migliorato del testo facilita la lettura dei messaggi della barra dei riferimenti. La modifica chiarisce i prompt che richiedono una selezione o segnalano riferimenti non disponibili. (SITES-24666)
* Il pannello Componenti fornisce a ogni icona di informazioni un’etichetta accessibile significativa. Gli assistenti vocali identificano in modo coerente il controllo che mostra la descrizione di un componente. (SITES-24500)
* Lo stato attivo sulla tastiera ora circonda l’intero pulsante Mostra descrizione per Byline. La struttura visibile consente agli utenti di tenere traccia della loro posizione ed evitare di attivare un altro controllo. (SITES-24503)
* La finestra di dialogo del componente Teaser non espone più i pulsanti Guida in linea e Attiva/Disattiva schermo intero come intestazioni. Gli assistenti vocali annunciano entrambi i controlli come pulsanti e mantengono la struttura di intestazione corretta. (SITES-24525)
* Il controllo intestazione Adobe Experience Manager segnala correttamente lo stato espanso o compresso. Il controllo apre e chiude il contenuto di navigazione, in modo che gli assistenti vocali ricevano informazioni valide sullo stato. (SITES-24528)
* I risultati del filtro contrassegnano le icone a forma di globo come decorative e ne rimuovono i nomi accessibili. Gli assistenti vocali ignorano le icone invece di annunciare descrizioni fuorvianti. (SITES-3057)
* La finestra di dialogo Alterazione tempo ora associa gli errori di immissione ora al campo Ore o Minuti corrispondente. Gli assistenti vocali annunciano il campo interessato insieme al messaggio di convalida. (SITES-10980)
* L&#39;elemento della struttura contenuto selezionato non fa più parte dell&#39;etichetta di controllo Cambia file o cartella. Gli assistenti vocali sentono un nome di controllo chiaro senza testo di stato aggiuntivo. (SITES-24496)
* I punti di riferimento regionali nella barra laterale di Assets ora espongono nomi accessibili distinti. Gli utenti di utilità di lettura dello schermo possono identificare e navigare in ogni regione senza ambiguità. (SITES-24497)
* Gli assistenti vocali ora ignorano le icone decorative della Guida e Schermo intero della finestra di dialogo Carosello. La navigazione tramite tastiera non attiva più annunci di icone non necessari. (SITES-2912)
* Gli assistenti vocali ora ignorano le icone decorative della barra degli strumenti nella finestra di dialogo Teaser. I controlli Guida, Schermo intero, Formattazione e Collegamento non generano più annunci ridondanti. (SITES-2934)


#### Interfaccia utente amministratore{#sites-adminui-65-lts-sp3}

* AEM ora consente ai membri del gruppo Amministratore di sbloccare le pagine e rappresentare gli utenti. I membri del gruppo possono completare entrambe le attività amministrative tramite il proprio accesso esistente. (SITES-14732)
* Assets Admin View ora aggiorna una scheda di risorse dopo che gli autori hanno selezionato **Ripristina questa versione** nella timeline. La miniatura mostra immediatamente la versione ripristinata e non mostra più il contenuto di anteprima non aggiornato. (SITES-46590)


#### Interfaccia utente classica{#sites-classicui-65-lts-sp3}

Le proprietà della copia in lingua indonesiana mostrano il codice corretto per la lingua ID. La barra Riferimenti non sostituisce più IN quando gli autori creano o revisionano una copia in lingua indonesiana. (SITES-44918)


#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp3}

La console Assets ora risponde quando gli utenti applicano i filtri di ricerca. La modifica di un filtro Modello per frammenti di contenuto aggiorna i risultati invece di lasciare invariato l’elenco delle risorse corrente. (SITES-38686) PRINCIPALE


#### [!DNL Content Fragments] - Amministratore{#sites-admin-65-lts-sp3}

* La pagina Assets ora localizza la descrizione comando per un frammento di contenuto bloccato. Gli utenti visualizzano l&#39;etichetta **Estratto da** quando passano il puntatore sull&#39;indicatore del blocco. (SITES-42531) PRINCIPALE

* AEM localizza il messaggio di convalida del nome non valido fornito durante la creazione del frammento di contenuto. I caratteri di titolo non supportati non attivano più il testo inglese nelle interfacce non inglesi. (SITES-19796)
* AEM traduce la stringa Modelli per frammenti di contenuto durante la creazione del frammento di contenuto. L’interfaccia di Assets non mostra più il testo inglese per l’etichetta negli ambienti localizzati. (SITES-22336)
* I servizi per frammenti di contenuto non si basano più su una logica obsoleta di attivazione/disattivazione delle funzioni. L’implementazione semplificata rimuove i rami dipendenti dall’interruttore e mantiene coerente il comportamento del service pack. (SITES-38688)
* AEM traduce l’opzione Later (Più tardi) durante la pubblicazione pianificata del frammento di contenuto. Il flusso di lavoro di pubblicazione corrisponde alla lingua dell’interfaccia attiva. (SITES-42532)
* AEM traduce la stringa Main nella finestra di dialogo di download del frammento di contenuto. La sezione Elementi corrisponde al linguaggio di interfaccia attivo. (SITES-42534)


#### [!DNL Content Fragments] - Editor frammento{#sites-fragments-editor-65-lts-sp3}

* L’Editor frammento di contenuto ora posiziona correttamente i menu a discesa dell’Editor Rich Text. Ogni menu rimane allineato con il relativo controllo barra degli strumenti e mantiene visibili i controlli di formattazione adiacenti. (SITES-44005) CRITICO

* Ora viene visualizzato il pulsante Modifica frammento di contenuto e funziona immediatamente per le voci Multifield di riferimento. Gli autori non dovranno più salvare, chiudere e riaprire il frammento di contenuto principale prima di modificare un frammento incorporato. (SITES-43733) PRINCIPALE

* Quando gli autori selezionano un campo di testo su più righe, l’Editor frammenti di contenuto mostra un profilo di stato attivo. Il profilo non duplica più o si sovrappone ai controlli vicini. (SITES-39253)
* Durante la creazione di frammenti di contenuto viene visualizzato il testo segnaposto CJK senza stile corsivo. I caratteri giapponesi, coreani, cinesi semplificati e cinesi tradizionali mantengono l&#39;aspetto desiderato. (SITES-43548)
* L’Editor frammento di contenuto aggiorna il banner di stato dopo che gli autori hanno salvato o pubblicato un frammento. Gli autori possono confermare gli stati Modificato, Salvato o Pubblicato senza ricaricare la scheda del browser. (SITES-45897)
* L’Editor frammento di contenuto convalida i campi in modo coerente dopo le modifiche all’interfaccia utente di Granite. Le librerie client aggiornate ripristinano il comportamento di convalida previsto. (SITES-46650)


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-65-lts-sp3}

* Le risposte JSON GraphQL ora includono riferimenti a immagini incorporate quando i nomi di file DAM contengono spazi o caratteri non ASCII. Le applicazioni client possono recuperare ed eseguire il rendering di queste immagini senza rinominare le risorse. (SITES-42191) PRINCIPALE
* L’API GraphQL per frammenti di contenuto ora include diversi aggiornamenti per l’elaborazione delle query e la gestione delle risposte. Le modifiche impediscono la duplicazione di intestazioni e valori della cache, migliorano la codifica, mantengono le informazioni sullo stato delle query persistenti, gestiscono intestazioni vuote e restituiscono errori di endpoint appropriati. (SITES-40159) PRINCIPALE
* PersistedQueryServlet ora elabora variabili codificate in query GraphQL persistenti valide senza registrare falsi errori o avvisi. Le query continuano a restituire risposte riuscite, mentre i registri ne riflettono lo stato di esecuzione effettivo. (SITES-39354) PRINCIPALE

* Il ricaricamento della pagina Endpoint di GraphQL mantiene il messaggio localizzato a stato vuoto. La pagina non viene più ripristinata in inglese se non esiste alcun endpoint. (SITES-43586)


<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-65-lts-sp3}-->


#### [!DNL Content Fragments] - Editor modello{#sites-model-editor-65-lts-sp3}

* Nella console Modelli per frammenti di contenuto vengono ora visualizzate le miniature caricate per le configurazioni i cui nomi contengono caratteri localizzati. Gli autori non perdono più le anteprime delle miniature quando i nomi di configurazione utilizzano testo non inglese. (SITES-39242) PRINCIPALE

* L&#39;Editor modello per frammenti di contenuto visualizza il testo localizzato **Etichetta campo** non appena gli autori aggiungono un componente all&#39;area di lavoro. Gli autori non dovranno più salvare e riaprire il modello per visualizzare la traduzione. (SITES-45383)
* L’Editor modello per frammenti di contenuto localizza il messaggio di convalida visualizzato quando gli autori selezionano un tipo di modello non valido per un componente composito. Il messaggio ora corrisponde alla lingua attiva invece di essere visualizzato solo in inglese. (SITES-41117)
* L’Editor modello per frammenti di contenuto localizza tutto il testo nella finestra di dialogo Il modello è bloccato. La finestra di dialogo non combina più le etichette dei pulsanti e le istruzioni inglesi con il testo dell&#39;interfaccia tradotto. (SITES-28592)



#### [!DNL Content Fragments] - API REST{#sites-restapi-65-lts-sp3}

Il bundle API REST per frammenti di contenuto headless rimuove gli interruttori delle funzioni obsoleti e il relativo codice condizionale. Il comportamento API supportato rimane invariato, mentre il bundle mantiene solo gli interruttori necessari per le funzioni attive. (SITES-39113)



#### Console dei componenti{#sites-component-console-65-lts-sp3}

Content Finder ora elenca le risorse i cui nomi contengono caratteri non codificabili senza generare errori o eccezioni. La pagina Utilizzo live dei componenti carica anche set di risultati di grandi dimensioni in modo continuo, senza visualizzare righe vuote durante lo scorrimento. (SITES-44672) PRINCIPALE

<!--
#### Content API{#sites-content-api-65-lts-sp3}

#### Core backend{#sites-core-backend-65-lts-sp3}
-->

#### Componenti core{#sites-core-components-65-lts-sp3}

* I componenti con più campi ora memorizzano una selezione separata di risorse remote per ogni voce. Gli autori possono selezionare, modificare e salvare immagini remote senza duplicare un’immagine su ogni elemento con più campi. (SITES-42376) PRINCIPALE
* ThumbnailServlet ora interrompe l’elaborazione dopo aver reindirizzato una richiesta per una risorsa mancante. Questa modifica impedisce la ripetizione delle eccezioni Null-Pointer e la registrazione di errori eccessivi durante l’esplorazione di DAM e console. (SITES-41238) PRINCIPALE


#### Integrazione di Campaign{#sites-campaign-integration-65-lts-sp3}

Campaign ContentServlet ora mantiene il tipo di contenuto di risposta JSON durante le richieste di contenuto. Questa modifica arresta le voci di registro ripetute `WARN` e `ERROR` che si sono verificate dopo un aggiornamento da AEM 6.5.24. (SITES-46902) PRINCIPALE


#### Frammenti di esperienza{#sites-experiencefragments-65-lts-sp3}

Gli autori possono ora sfogliare più di 40 modelli durante la creazione di una variante del frammento di esperienza. Ogni pagina aggiuntiva mantiene il filtro della cartella originale e visualizza i modelli corrispondenti successivi. (SITES-41531) PRINCIPALE


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp3} -->


#### Lanci{#sites-launches-65-lts-sp3}

La cronologia delle promozioni di Launch ora visualizza il testo localizzato nella timeline dei siti. La Timeline traduce i messaggi &quot;Versione creata di&quot; e &quot;prima della promozione del lancio&quot; in tutte le lingue supportate. (SITES-13389)


<!-- #### Link Checker{#sites-link-checker-65-lts-sp3} -->



#### MSM - Live Copy{#sites-msm-live-copies-65-lts-sp3}

* Le cartelle Live Copy dei frammenti di contenuto ora mantengono cq:rolloutConfigs quando gli autori salvano le proprietà invariate. Gli autori possono in seguito aggiornare le impostazioni di rollout senza perdere la configurazione esistente. (SITES-43729) CRITICO

* Gli autori possono ora eseguire il rollout delle modifiche dei componenti dalla barra degli strumenti modificabile in una pagina blueprint. Il rollout viene completato senza un errore JavaScript e propaga le modifiche alla Live Copy. (SITES-46052) PRINCIPALE
* Gli autori possono ora completare i rollout MSM dalle pagine blueprint dopo un aggiornamento. La finestra di dialogo Rollout carica le Live Copy disponibili e abilita i relativi controlli di rollout invece di rimanere in uno stato di caricamento permanente. (SITES-43116) PRINCIPALE

* Panoramica Live Copy ora applica i formati di data localizzati in tutto lo stato della relazione. I campi **Ultima modifica Live Copy di Source**, **Ultima modifica Live Copy** e **Ultimo rollout** corrispondono alle impostazioni locali dell&#39;utente. (SITES-40756)
* La disattivazione di un elemento principale blueprint e delle relative pagine secondarie in una richiesta ora genera un evento di rollout per percorso. Il gestore di rollout non esegue più azioni duplicate per la stessa pagina secondaria. (SITES-44987)


#### Editor pagina{#sites-pageeditor-65-lts-sp3}

* Gli autori possono ora creare e applicare tag con lettere maiuscole o spazi durante il salvataggio delle Proprietà pagina. AEM memorizza immediatamente il valore del tag normalizzato e mantiene l’assegnazione della pagina. (SITES-42550) CRITICO

* Lo scorrimento del menu di stile non rimuove più l&#39;evidenziazione dallo stile selezionato. Gli autori possono confermare la selezione corrente esaminando altre opzioni disponibili. (SITES-30874) PRINCIPALE

* Il pulsante Rich Text Editor Link ora si apre quando gli autori accedono ad AEM tramite HTTP. La creazione del collegamento non attiva più l&#39;errore `crypto.randomUUID`. (SITES-39467)
* Gli autori possono ora copiare e incollare i componenti per frammenti di contenuto configurati in contenitori di layout vuoti. Il componente incollato mantiene il riferimento originale al frammento di contenuto e non visualizza più l&#39;errore *Scegli una variante di esperienza*. (SITES-41586)
* L’Editor immagini ora rispetta le proporzioni di ritaglio personalizzate durante la modifica ibrida in linea. Ogni destinazione di rilascio dell&#39;immagine utilizza la propria configurazione, pertanto le selezioni di ritaglio vengono applicate in modo corretto al di fuori della modalità a schermo intero. (SITES-45771)

<!--
#### Replication{#sites-replication-65-lts-sp3}

#### Rich Text Editor{#sites-rte-65-lts-sp3}

#### Template Editor{#sites-template-editor-65-lts-sp3}

#### Universal editor {#sites-universal-editor-65-lts-sp3}

### [!DNL Assets]{#assets-65-lts-sp3}

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp3}

#### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp3}
-->



### [!DNL Forms]{#forms-65-lts-sp3}

>[!NOTE]
>
> È ora disponibile AEM Forms 6.5 LTS Service Pack 3 (SP3) per le distribuzioni OSGi. Include correzioni di bug, miglioramenti della sicurezza e miglioramenti. **AEM Forms 6.5 LTS Service Pack 3 (SP3) per implementazioni JEE verrà rilasciato in un secondo momento.**

#### Miglioramenti {#forms-enhancements-65-lts-sp3}

* FORMS-24360: aggiunto il supporto di PDF Generator (PDFG) per Microsoft Office 2024.
* FORMS-24949: aggiunta del supporto dell&#39;agente Forms Builder in AEM Forms 6.5 LTS. In questo modo vengono supportate le API HTTP di Forms Manager e le API HTTP di IA per la generazione di moduli (GenAI) richieste dall’agente.
* FORMS-25180: è stato aggiunto il valore `daysUntilSigningDeadline` all&#39;interfaccia utente di AEM Forms, in modo che gli autori possano mostrare ai destinatari il numero di giorni rimanenti prima della scadenza della firma Adobe Sign.
* FORMS-25182: PDF Generator (PDFG) ora supporta le conversioni di documenti multithread se configurato con un singolo account utente.

#### Problemi risolti {#forms-fixed-issues-65-lts-sp3}

* FORMS-23726: applicazione di uno schema XML nelle proprietà di Adaptive Forms non riuscita a causa di un conflitto di libreria `xsom`. La selezione dello schema ora funziona.
* FORMS-24296: il campo Allegato file dei componenti di base ha accettato i tipi di file non consentiti (ad esempio, `.xsd`) al momento del caricamento e li ha rifiutati solo al momento dell&#39;invio, a differenza di altri tipi bloccati. I tipi non consentiti ora sono bloccati al caricamento.
* FORMS-24603: nelle lettere di Gestione della corrispondenza, i frammenti di testo che presentavano una condizione hanno perso le interruzioni di riga se salvati come bozza. Le bozze ora mantengono le interruzioni di riga originali.
* FORMS-24783: gli allegati sono stati eliminati dal passaggio `assignTask` nei flussi di lavoro Forms basati su Open Services Gateway initiative (OSGi). Gli allegati vengono ora mantenuti tramite l&#39;assegnazione di attività.
* FORMS-24877: l’icona del calendario Selezione data non mostrava alcuna etichetta accessibile quando veniva applicato un pattern di visualizzazione, pertanto l’assistente vocale NVDA annunciava solo &quot;cliccabile&quot;. L’icona fornisce ora un’etichetta descrittiva.
* FORMS-24913: i flussi di lavoro di AEM Forms si sono interrotti dopo il passaggio Adobe Sign perché lo stato di firma non è mai stato restituito. Al termine della firma, i flussi di lavoro ora continuano.
* FORMS-25033: il componente Firma scarabocchio è stato saltato nell’ordine di tabulazione della tastiera, creando una barriera di accessibilità per gli utenti che utilizzano solo la tastiera. La navigazione tramite scheda ora raggiunge il campo.
* FORMS-25045: le traduzioni in cinese tradizionale (Hong Kong) hanno smesso di eseguire il rendering dopo un aggiornamento, quindi i moduli sono tornati alla lingua predefinita. Il testo localizzato ora viene riprodotto correttamente.
* FORMS-25170: la chiamata a `addInstance()` non mostrava i pannelli aggiunti in modo dinamico quando il conteggio delle istanze iniziali era 0. I pannelli aggiunti ora vengono visualizzati immediatamente.
* FORMS-25225: il rinnovo lato server ha rimosso le traduzioni dei campi al di fuori dei frammenti in Adaptive Forms, ripristinando le etichette alla lingua di base. Tali traduzioni vengono ora mantenute.
* FORMS-25233: nelle distribuzioni OSGi (Open Services Gateway initiative), il servizio Assembler ha unito un XDP principale con il relativo frammento immediato, ma non ha risolto i riferimenti ai frammenti nidificati come intestazioni, piè di pagina e sottomoduli riutilizzabili, quindi mancavano dall’output assemblato. I frammenti nidificati ora vengono risolti.
* FORMS-25289: il servizio di rendering di Forms ha restituito un output diverso per lo stesso input in tutti i service pack, influendo sulle lettere di Gestione corrispondenza. L’output di rendering è ora coerente.
* FORMS-25290: le lettere di Gestione della corrispondenza salvate hanno perso spazi e hanno mostrato una &quot;x&quot; in alcuni punti quando sono state riaperte. Il contenuto della lettera salvata ora rimane intatto.
* FORMS-25346: dopo un aggiornamento del service pack, le lettere di comunicazione interattiva (IC) si bloccano durante un ciclo di caricamento e le lettere che hanno caricato hanno perso spazio nell’anteprima. Il caricamento e la spaziatura ora funzionano correttamente.
* FORMS-25431: la procedura guidata Crea frammento di modulo ha inviato una richiesta di rete a ogni sequenza di tasti nel campo del titolo. Le chiamate ridondanti sono state rimosse.
* FORMS-25645: creazione di un frammento di modulo adattivo basato su componenti core da uno schema JSON caricato in linea non riuscita con &quot;È stato specificato un modello di modulo non valido ALC-FMG-700-009.&quot; Gli schemi JSON in linea sono ora accettati.
* FORMS-25646: un frammento di modulo adattivo basato su componenti core e creato da uno schema JSON mostrava un pannello Origini dati vuoto nell’editor. Il pannello ora elenca le origini dati dello schema.
* FORMS-25674: l&#39;interfaccia utente dell&#39;agente di comunicazione interattiva (IC) è stata aperta in una pagina vuota, pertanto gli agenti non sono stati in grado di visualizzare il contenuto IC. Viene ora eseguito il rendering dell&#39;interfaccia utente dell&#39;agente.
* FORMS-25686: il passaggio dell’opzione di tipo schema nella procedura guidata Crea frammento di modulo adattivo non ha azzerato lo stato dell’opzione precedente, generando una mancata corrispondenza dello schema. La procedura guidata ripristina l&#39;opzione inattiva.
* FORMS-25757: l’applicazione di un tema non aggiorna la libreria client di base, pertanto le modifiche al tema sembrano non avere alcun effetto. I temi ora aggiornano la libreria client di base.
* FORMS-25825: Il menu dell’hamburger mobile non ha risposto ai tocchi, rendendo la navigazione inutilizzabile sui dispositivi mobili. Il menu ora si apre come previsto.
* FORMS-26333: l’azione Pubblica scompare dopo l’annullamento della pubblicazione di un modulo, impedendo in tal modo la ripubblicazione. La pubblicazione è ora disponibile dopo l’annullamento della pubblicazione.
* FORMS-26763: in Designer, la formattazione in grassetto sui collegamenti ipertestuali all’interno di un oggetto di testo statico veniva persa dopo eventuali modifiche al testo. La formattazione grassetto consente ora di mantenere le modifiche.
* FORMS-26817: facendo clic su Ripristina in un modulo adattivo, l’immagine configurata dall’autore nel componente Immagine viene cancellata e l’immagine non funziona più, mentre gli altri campi vengono ripristinati correttamente. L’operazione Reimposta mantiene l’immagine configurata.
* FORMS-26852: nell’interfaccia utente dell’agente, un campo data/ora mostrava la data un giorno prima del valore memorizzato. Il campo ora mostra la data corretta.

#### Problemi noti {#forms-known-issues-65-lts-sp3}

Per questa versione non vengono segnalati problemi noti.

#### Correzioni di sicurezza {#forms-security-fixes-65-lts-sp3}

Questa versione risolve le vulnerabilità relative alla sicurezza in AEM Forms, incluse più correzioni di vulnerabilità cross-site scripting (XSS), una correzione di SSRF (request forgery) lato server, una correzione di entità esterna XML (XXE) e aggiornamenti a librerie di terze parti.

<!-- TODO: Add security bulletin link. Open question, pending information from Sunny Marwaha. -->




### Foundation {#foundation-65-lts-sp3}

#### Servizio contestuale AEM {#foundation-aem-context-service-65-lts-sp3}

AEM 6.5 LTS introduce il supporto AEM Context Service. Il rollout aggiunge API di servizio, integrazione degli agenti, provisioning AMS, integrazione Experience Cloud, monitoraggio della produzione, runbook operativi e reporting sull’utilizzo. (GRANITE-65148)

#### Apache Felix {#foundation-apachefelix-65-lts-sp3}

Il servizio di posta di AEM ora continua a inviare e-mail quando si verificano errori di configurazione intermittenti. Gli amministratori non dovranno più riavviare il bundle Day Communique 5 Mailer per ripristinare la consegna delle e-mail. (GRANITE-66817) PRINCIPALE

<!--
#### Campaign{#foundation-campaign-65-lts-sp3}

#### Cloud Services{#foundation-cloudservices-65-lts-sp3}

#### Communities {#foundation-communities-65-lts-sp3}

#### Content distribution{#foundation-content-distribution-65-lts-sp3}

#### CRX {#foundation-crx-65-lts-sp3}

#### Granite{#foundation-granite-65-lts-sp3}

#### HTL{#foundation-htl-5-lts-sp3}

#### Integrations{#foundation-integrations-65-lts-sp3}

#### Jetty{#foundation-jetty-65-lts-sp3}
-->

#### Localizzazione{#foundation-localization-65-lts-sp3}

* La console Operazioni ora localizza il testo non tradotto in precedenza nei rapporti di stato. Gli utenti visualizzano messaggi di stato tradotti, avvisi, risultati di manutenzione e informazioni sulle prestazioni. (NPR-44280) PRINCIPALE

* L&#39;attività di manutenzione del registro di controllo visualizza ora una liberatoria localizzata. Prima di configurare la rimozione automatica dei registri di audit, gli amministratori possono consultare le linee guida legali e di conformità nella lingua selezionata. (NPR-44188)
* La pagina Modifica utente visualizza ora un errore localizzato quando gli utenti riordinano i profili modificati. Il messaggio spiega chiaramente che i profili modificati non possono essere spostati finché gli utenti non salvano le modifiche. (NPR-44282)
* AEM ora localizza le descrizioni comandi in tutte le proprietà dell’elenco di frammenti di contenuto. La guida tradotta spiega la selezione del modello, il filtraggio dei tag, i percorsi del contenuto, i limiti degli elementi e le impostazioni di ordinamento. (SITES-14969)
* Ora tramite i collegamenti della Guida dei componenti nell’Editor modelli viene aperta la documentazione localizzata. Gli autori ricevono indicazioni che corrispondono alla lingua selezionata, anziché pagine dei componenti in lingua inglese. (SITES-15058)
* L’editor dei criteri dei componenti ora localizza gli errori che segnalano una risorsa non modificabile o una creazione di nodo non riuscita. Gli autori dei modelli ricevono questi messaggi nella lingua selezionata. (SITES-17475)

<!-- #### Omnisearch{#foundation-omnisearch-65-lts-sp3} -->

#### Dashboard operazioni{#foundation-operations-dashboard-65-lts-sp3}

L&#39;endpoint `/system/health/systemalive.json` ora rimane disponibile dopo l&#39;aggiornamento di AEM LTS da parte dei clienti. Una configurazione corretta del contesto del servlet impedisce le risposte HTTP 404 e supporta i sistemi di monitoraggio dello stato che si basano sull’endpoint. (GRANITE-69457) CRITICO

#### Platform{#foundation-platform-65-lts-sp3}

L’elenco consentiti predefinito per l’opzione di espressione HTL riconosce ora `decorationTagName` e `cssClassName`. Il rendering della griglia reattiva standard non riempie più `error.log` con ripetuti avvisi di opzione sconosciuta. (GRANITE-67152)

<!--
#### Projects{#foundation-projects-65-lts-sp3}

#### Oak {#foundation-oak-65-lts-sp3}

#### Quickstart{#foundation-quickstart-65-lts-sp3} 
-->


#### Sicurezza{#foundation-security-65-lts-sp3}

L&#39;azione **Copia gruppo** apre il modulo previsto invece di visualizzare una pagina vuota. Gli amministratori possono immettere un nuovo ID gruppo e una nuova descrizione, quindi duplicare un gruppo di sicurezza esistente. (NPR-44302) PRINCIPALE


<!-- #### Sling{#foundation-sling-65-lts-sp3} -->


#### Traduzione{#foundation-translation-65-lts-sp3}

I progetti di traduzione ora mantengono un conteggio accurato dello stato durante l’avanzamento dei flussi di lavoro. La creazione del lancio e la propagazione dello stato seguono il comportamento previsto del flusso di lavoro, eliminando i metadati di progetto incoerenti. (NPR-43420)


#### Interfaccia utente{#foundation-ui-65-lts-sp3}

* L&#39;etichetta Paese viene ora visualizzata nella lingua dell&#39;interfaccia selezionata. Le interfacce localizzate non visualizzano più l&#39;etichetta inglese. (NPR-43883)
* Selezionando una pagina di pari livello ora si attiva **Select** nei selettori di percorsi compositi con più campi. Gli autori possono confermare il nuovo percorso senza ingrandire la finestra del browser o ripetere la selezione. (GRANITE-69323)


<!-- #### WCM{#foundation-wcm-65-lts-sp3} -->


#### Flusso di lavoro{#foundation-workflow-65-lts-sp3}

* Le pagine dei pacchetti del flusso di lavoro ora supportano la struttura del contenuto e i componenti di definizione delle risorse modificabili nell’Editor pagina dell’interfaccia utente touch. Gli autori possono navigare nel contenuto del pacchetto e ispezionarne o aggiornarne i componenti senza utilizzare l’interfaccia classica. (GRANITE-67348) PRINCIPALE
* L’Editor pagina dell’interfaccia touch ora esegue il rendering della struttura contenuto per le pagine dei pacchetti del flusso di lavoro. Gli autori possono esaminare la struttura del pacchetto e modificare i componenti Definizione risorsa tramite lo stesso editor. (GRANITE-67186) PRINCIPALE

* La finestra di dialogo delle variabili del flusso di lavoro visualizza ora i controlli corretti per le variabili Form Data Model, JSON, XML e Document. Gli autori non visualizzano più il markup HTML non elaborato quando creano queste variabili non primitive. (GRANITE-67915)


## Informazioni su [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 LTS si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e dell’archivio dei contenuti Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x è utilizzato come motore servlet per Quickstart.

### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituisci i valori predefiniti del GC (catalogo globale) con altri valori. Per ulteriori informazioni, consulta la sezione [Installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuisce gli aggiornamenti di manutenzione Java™ 17 e Java™ 21 per l’utilizzo da parte del cliente nei progetti correlati ad AEM, se non disponibili pubblicamente da Oracle.

### Pacchetto Uberjar {#uber-jar-packaging}

UberJar per AEM 6.5 LTS SP3 utilizza AEM 6.5 LTS UberJar versione 6.6.3. Puoi recuperare gli artefatti UberJar corrispondenti dall’archivio centrale Maven. A differenza di AEM 6.5, AEM 6.5 LTS separa le API pubbliche e quelle obsolete in due artefatti diversi.

Per eseguire la compilazione in base alle API pubbliche, utilizza quanto segue:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.3</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

Se il codice dipende anche da API obsolete, aggiungi quanto segue:

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.3</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

Consulta anche [Aggiornare la versione Uber Jar Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### Aggiornamento {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).
* Per istruzioni sull’aggiornamento dettagliate, consulta la [Guida all’aggiornamento per AEM Forms 6.5 LTS SP1 su JEE](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## Best practice per gli aggiornamenti del Service Pack di AEM 6.5 LTS

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

Applicabile a: clienti AEM 6.5 LTS (On-Premise) che installano Service Pack 3 (SP3). SP3 viene fornito come file JAR Quickstart.

**Perché questo aggiornamento è importante**
SP2 per AEM 6.5 LTS viene fornito come file Quickstart JAR anziché come file ZIP da installare tramite il gestore di pacchetti. I clienti on-premise eseguono l’aggiornamento sostituendo il file JAR Quickstart, disimballandolo e riavviandolo. Questo metodo è conforme alla procedura di aggiornamento standard di Adobe.


**Flusso di aggiornamento consigliato (authoring o pubblicazione)**

1. Verifica che l’istanza AEM 6.5 LTS sia integra e accessibile.
1. Scarica il file Quickstart JAR (ad esempio, `cq-quickstart-6.6.x.jar`) dalla distribuzione del software.
1. Arresta l&#39;istanza in esecuzione.
1. Nella directory di installazione di AEM (all&#39;esterno di `crx-quickstart/`), sostituire il file JAR Quickstart precedente con il file JAR SP3.
1. Decomprimi il file JAR:

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   (Regola i flag dell&#39;heap in base alle esigenze).

1. Rinomina il file JAR decompresso in modo che corrisponda al ruolo e alla porta, ad esempio `cq-author-4502.jar` o `cq-publish-4503.jar`.
1. Avvia AEM e conferma l’aggiornamento nell’interfaccia utente (Guida > Informazioni) e nei registri.

**Best practice**

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


Per istruzioni dettagliate, vedere la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md), in quanto la stessa documentazione si applica agli aggiornamenti del Service Pack LTS.

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

Si consiglia ai clienti di verificare se utilizzano la funzione/funzionalità nella distribuzione corrente. Pianifica la modifica dell’implementazione utilizzando l’alternativa fornita.

| Area | Funzione | Sostituzione | Versione (SP) |
| --- | --- | --- | --- |
| Quickstart | API Mongo | Le API Mongo ora sono obsolete e la loro rimozione è pianificata per le versioni future. | 6.5 TS SP2 |
| Sites | Supporto ai frammenti di contenuto nell’API REST di AEM Assets | AEM 6.5 LTS SP2 fornisce OpenAPI moderne per la gestione dei modelli e frammenti di contenuto, pertanto gli endpoint precedenti per il supporto dei frammenti di contenuto nell’API REST di AEM Assets sono ora obsoleti.<br>Adobe intende mantenere questi endpoint precedenti disponibili fino a un annuncio di fine del ciclo di vita. Adobe non pianifica ulteriori miglioramenti per gli endpoint obsoleti. | 6.5 LTS SP2 |
| Sites | [Editor SPA](/help/sites-developing/spa-overview.md) | Gli editor preferiti per la gestione dei contenuti headless in AEM sono:<br>- [l’editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.<br>- [L’editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per modifiche basate sul modulo. | 6.5 LTS GA |
| [!DNL Foundation] | Supporto per com.adobe.granite.oauth.server | Integrazione di Adobe IMS | |

### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità e le funzioni che sono state rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

* Il supporto per RDBMK per la persistenza dell’archivio Adobe CRX è stato rimosso.
* Negli ambienti cluster, MongoMK è ora l’unica opzione supportata per la persistenza dell’archivio.

| Area | Funzione | Sostituzione | Versione (SP) |
| --- | --- | --- | --- |
| Sites | Riepilogo del testo dei frammenti di contenuto | Nessuna sostituzione disponibile. | 6,5 LTS SP3 |
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

* In Gestione configurazioni, l’inizializzazione del database non riesce durante l’avvio in modalità personalizzata preconfigurata di AEM Forms 6.5 LTS JEE quando non è selezionato alcun modulo o sono selezionati solo componenti limitati. L’errore è dovuto a una dipendenza mancante (xalan-2.7.2.jar), che determina un errore. L’aggiunta del file JAR a Adobe-livecycle-jboss.ear\lib risolve il problema. (FORMS-24690)
* Nelle distribuzioni di Forms JEE LTS Service Pack 2 in esecuzione su WebSphere® Liberty Profile, la funzionalità e-mail non riesce. Quando si tenta di utilizzare le funzionalità di posta elettronica, il server registra un errore: `Could not convert socket to TLS`. (FORMS-24692)
* In Forms JEE LTS in esecuzione su JBoss®, la funzionalità relativa all’e-mail non riesce. Quando si tenta di utilizzare le funzionalità di posta elettronica, il server registra un errore: `Error IMAPProvider not a subtype`. Per risolvere il problema, installare l&#39;aggiornamento rapido da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-core-jboss.ear). (FORMS-24892)

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

Per utilizzare questa funzionalità, installare l&#39;aggiornamento rapido da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-67640-1.0.zip).

>[!NOTE]
>
> Per garantire che la configurazione predefinita di `com.adobe.granite.apicontroller` non introduca restrizioni di risoluzione non intenzionali che influiscono sulle implementazioni personalizzate esistenti, verificare lo stato del bundle di tutti i bundle installati dopo l&#39;installazione dell&#39;hotfix.

### Commenti JSON non più supportati in Sling-Initial-Content (SP2) {#json-comments-no-longer-supported-in-sling-initial-content}

Questo problema riguarda sviluppatori e amministratori di bundle OSGi che implementano bundle che utilizzano `Sling-Initial-Content` con file JSON.

A partire da AEM 6.5 LTS SP2, i file JSON utilizzati nei bundle `Sling-Initial-Content` non accettano più commenti (`//` o `/* */`). Le versioni precedenti di AEM accettavano i commenti perché il provider `javax.json` era indulgente al riguardo. AEM 6.5 LTS SP2 ha aggiornato `org.apache.sling.jcr.contentloader` alla versione 2.6.0, cambiando il parser JSON in `jakarta.json`. Sebbene la [specifica JSON (RFC 8259)](https://datatracker.ietf.org/doc/html/rfc8259) non definisca la sintassi per i commenti, erano accettati nelle versioni precedenti di AEM grazie all’indulgenza del provider `javax.json`. Il provider `jakarta.json` non offre questa estensione.

L’errore è invisibile all’utente: i nodi di contenuto non vengono caricati all’attivazione del bundle e il programma di installazione non visualizza alcun messaggio di errore. Se manca inaspettatamente del contenuto dopo l’aggiornamento a SP2, controlla i registri del programma di installazione di OSGi per verificare la presenza di errori di analisi JSON. Per identificare i bundle interessati, cerca `//` o `/* */` all’interno dei file JSON elencati nelle intestazioni manifesto di `Sling-Initial-Content`.

>[!CAUTION]
>
> Per evitare errori di caricamento del contenuto dopo l&#39;aggiornamento ad AEM 6.5 LTS SP2, rimuovere tutti i commenti dai file JSON nei bundle `Sling-Initial-Content`.

### L’aggiornamento del bundle Jackson influisce sul connettore GlobalLink {#jackson-upgrade-globallink-connector}

AEM 6.5 LTS SP3 aggiorna il bundle `jackson`. Questa modifica influisce sulle distribuzioni che utilizzano il connettore di traduzione GlobalLink.

Se utilizzi il bundle `gs4tr-globallink-adaptors-aem.core` in una versione precedente alla 3.4.0, aggiorna il bundle a una versione compatibile. La versione 3.4.0 o successiva funziona con il bundle `jackson` aggiornato in SP3.

>[!NOTE]
>
> Aggiornare il bundle `gs4tr-globallink-adaptors-aem.core` alla versione 3.4.0 o successiva prima o durante l&#39;aggiornamento di SP3 per evitare problemi di compatibilità con il connettore GlobalLink.


### Installa gli indici Oak richiesti per le API headless di Sites{#site-headless-api}

Alcune API che sono state spostate in Sites Headless richiedono indici Oak aggiuntivi per garantire la piena funzionalità.

Per utilizzare le funzionalità seguenti, installare il pacchetto `cq-dam-cfm-indices`:

* Elenco modelli per frammenti di contenuto
* Elenco frammenti di contenuto
* Ricerca API
* Flussi di lavoro

Scarica il pacchetto di indice [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fcq-dam-cfm-indices-1.1.5.zip) dal portale di distribuzione software di Adobe.

### Errore di connessione di Dispatcher con la funzione solo SSL (risolto in AEM 6.5 LTS SP1 e versioni successive){#ssl-only-feature}

>[!NOTE]
>
> Questo problema è presente solo nella versione AEM 6.5 LTS GA.

Quando si abilita la funzione solo SSL nelle implementazioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze Dispatcher e AEM. Dopo aver abilitato questa funzione, i controlli di integrità non riescono e la comunicazione tra le istanze Dispatcher e AEM viene interrotta. Questo problema si verifica in modo specifico quando i clienti tentano di connettersi tramite `https + IP` dalle istanze Dispatcher ad AEM. È correlato a problemi di convalida SNI (Server Name Indication).

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

Se riscontri questo problema, contatta l’Assistenza clienti Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip). Non tentare di abilitare le funzioni solo SSL finché non viene applicato l’hotfix necessario.

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

I seguenti file zip contengono i documenti di testo che elencano i bundle OSGi e i pacchetti di contenuti inclusi in questa versione del Service Pack Experience Manager 6.5 LTS:

* [Bundle OSGi](/help/release-notes/assets/65lts_sp3_bundles.zip)
* [Pacchetti di contenuti](/help/release-notes/assets/65lts_sp3_packages.zip)

## Siti web con restrizioni{#restricted-sites}

Questi siti web sono disponibili solo per la clientela. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/it/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience).

