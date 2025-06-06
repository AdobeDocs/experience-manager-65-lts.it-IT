---
title: Panoramica di AEM Document Services
description: AEM Document Services è un set di servizi OSGi per la creazione, l’assemblaggio e la protezione di documenti PDF.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Reader Extensions, Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 03e87c5a-c106-4b4c-9b42-8ce7a04d9c0c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 1%

---

# Panoramica di AEM Document Services{#overview-of-aem-document-services}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=it) |
| AEM 6.5 | Questo articolo |


AEM Document Services è un set di servizi OSGi per la creazione, l’assemblaggio e la protezione di documenti PDF. Document Services include i seguenti servizi:

## Servizio di output {#output-service}

Il servizio Output consente di creare documenti in diversi formati, tra cui PDF, formati di stampanti laser e formati di stampanti di etichette. I formati delle stampanti laser sono PostScript e Printer Control Language (PCL). Nell&#39;elenco seguente vengono specificati i formati della stampante di etichette:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Un documento può essere inviato a una stampante di rete, a una stampante locale o a un file nel file system. Il servizio di output unisce i dati del modulo XML con una struttura del modulo per generare un documento. Il servizio di output può generare un documento senza unire i dati del modulo XML nel documento. Tuttavia, il flusso di lavoro principale sta unendo i dati nel documento.

>[!NOTE]
>
>La progettazione di un modulo viene in genere creata utilizzando Designer. Per informazioni sulla creazione di progettazioni di moduli per il servizio di output, vedere la Guida in linea di Designer.

Quando si utilizza il servizio di output per unire i dati XML con una struttura di modulo, il risultato è un documento PDF non interattivo. Un documento PDF non interattivo non consente agli utenti di immettere dati nei relativi campi. È invece possibile utilizzare il servizio Forms per creare un modulo PDF interattivo che consenta agli utenti di immettere dati nei relativi campi.

Sono disponibili le seguenti quattro operazioni del servizio di output:

* **generatePDFOuput**: unisce la progettazione di un modulo ai dati per generare un documento PDF
* **generatePrintedOutput**: unisce la struttura di un modulo ai dati del modulo per generare un documento da inviare a una stampante laser o di rete di etichette

* **generatePDFOutputBatch**: unisce più modelli con più record di dati in una singola chiamata per generare un batch di file PDF. È inoltre possibile generare un singolo PDF combinando tutti i PDF
* **generatePrintedOutputBatch**: unisce più modelli con più record di dati in una singola chiamata per generare un batch di documenti di stampa (PS,PCL,ZPL,DPL,IPL,TPCL). È inoltre possibile generare un singolo documento di stampa.

## Servizio assemblatore {#assembler-service}

Il servizio Assembler consente di combinare, ridisporre e integrare i documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Ogni job inviato al servizio Assembler include un documento DDX (Document Description XML), documenti di origine e risorse esterne (stringhe e elementi grafici). Il documento DDX fornisce istruzioni su come utilizzare i documenti di origine per produrre un insieme di documenti risultanti.

Oltre alle funzionalità di cui sopra, il servizio Assembler:

* Converte i documenti PDF in PDF/A standard.
* Trasforma PDF forms, moduli XML (creati in Designer) e PDF forms (creati in Acrobat) in PDF/A-1b, PDF/A-2b e PDFA/A-3b.
* Converte documenti PDF firmati o non firmati (sono necessarie firme digitali).
* Convalida la conformità di un file PDF/A e, se necessario, lo converte.

### Informazioni su DDX {#about-ddx}

Quando si utilizza il servizio Assembler, utilizzare un linguaggio basato su XML denominato Document Description XML (DDX) per descrivere l&#39;output desiderato. DDX è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF, documenti XDP, frammenti di moduli XDP e altri elementi quali commenti, segnalibri e testo formattato.

Il documento DDX può specificare i documenti risultanti con le seguenti caratteristiche:

* Documento PDF assemblato da più documenti PDF
* Più documenti PDF separati da un singolo documento PDF
* PDF Portfolio che include un&#39;interfaccia utente autonoma e più documenti PDF e non PDF
* Documento XDP assemblato da più documenti XDP
* Documento XDP contenente frammenti XML inseriti in modo dinamico in un documento XDP
* Documento PDF che crea pacchetti per un documento XDP
* File XML che generano rapporti sulle caratteristiche di un documento PDF. Le caratteristiche segnalate includono testo, commenti, dati del modulo, file allegati, file utilizzati nei portfolio PDF, segnalibri e proprietà di PDF. Le proprietà di PDF includono le proprietà del modulo, la rotazione delle pagine e l’autore del documento.

È possibile utilizzare DDX per aumentare i documenti PDF come parte dell&#39;assemblaggio o del disassemblaggio del documento. È possibile specificare una combinazione qualsiasi dei seguenti effetti:

* Aggiungere o rimuovere filigrane o sfondi nelle pagine selezionate.
* Aggiungere o rimuovere intestazioni e piè di pagina nelle pagine selezionate.
* Rimuove la struttura e le funzionalità di navigazione di un pacchetto PDF o PDF Portfolio. Il risultato è un singolo file PDF.
* Rinumera le etichette delle pagine. Le etichette di pagina vengono in genere utilizzate per la numerazione delle pagine.
* Importa metadati da un altro documento di origine.
* Aggiungere o rimuovere file allegati, segnalibri, collegamenti, commenti e JavaScript.
* Imposta le caratteristiche della visualizzazione iniziale e ottimizza la visualizzazione sul Web.
* Impostare le autorizzazioni per PDF crittografato.
* Ruota le pagine o ruota e sposta il contenuto sulle pagine.
* Modifica le dimensioni delle pagine selezionate.
* Unisci i dati con un PDF basato su XFA.

È possibile utilizzare una mappa di input semplice per specificare le posizioni dei documenti di origine e dei documenti risultanti. Puoi inoltre utilizzare i seguenti tipi di URL di dati esterni:

* File
* FTP
* HTTP/HTTPS

## Servizio Doc Assurance {#doc-assurance-service}

Il servizio Doc Assurance consente di crittografare e decrittografare i documenti, estendere le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi e aggiungere firme digitali ai documenti. Gli utenti possono interagire facilmente con PDF forms e i documenti, mentre l&#39;organizzazione migliora la sicurezza, l&#39;archiviazione e la conformità.

Il servizio Doc Assurance contiene tre servizi: firma, crittografia ed estensione Reader.

### Servizio di firma {#signature-service}

Il servizio di firma consente di utilizzare firme digitali e documenti sul server AEM. Ad esempio, il servizio di firma viene utilizzato in genere nelle situazioni seguenti:

* Il server AEM certifica un modulo prima che venga inviato a un utente per l’apertura tramite Acrobat o Adobe Reader.
* Il server AEM convalida una firma aggiunta a un modulo tramite Acrobat o Adobe Reader.
* Il server AEM firma un modulo per conto di un notaio pubblico.

Il servizio di firma accede ai certificati e alle credenziali archiviati nell&#39;archivio fonti attendibili.

### Servizio Encryption {#encryption-service}

Il servizio Crittografia consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. È possibile crittografare l&#39;intero documento PDF (inclusi il contenuto, i metadati e gli allegati), tutti gli elementi diversi dai metadati o solo gli allegati. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al relativo contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Acrobat. Se un documento PDF è crittografato con un certificato, l&#39;utente deve decrittografare il documento PDF con una chiave privata (certificato). La chiave privata utilizzata per decrittografare il documento PDF deve corrispondere alla chiave pubblica utilizzata per crittografarlo.

### Servizio di estensione Reader {#reader-extension-service}

Il servizio Estensioni di Reader consente all’organizzazione di condividere facilmente documenti PDF interattivi estendendo le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio Estensioni di Reader funziona con Adobe Reader 7.0 o versione successiva. Il servizio aggiunge i diritti di utilizzo a un documento PDF. Questa azione attiva le funzioni che in genere non sono disponibili quando un documento di PDF viene aperto mediante Adobe Reader, ad esempio l&#39;aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con documenti abilitati per i diritti.

Quando ai documenti di PDF vengono aggiunti i diritti di utilizzo appropriati, i destinatari possono eseguire le seguenti attività da Adobe Reader:

* Compilare i documenti e i moduli di PDF online o offline, consentendo ai destinatari di salvare le copie in locale per i propri record e di mantenere intatte le informazioni aggiunte
* Salvare i documenti PDF su un disco rigido locale per conservare il documento originale ed eventuali commenti, dati o allegati aggiuntivi
* Allegare file e clip multimediali a documenti PDF
* Firmare, certificare e autenticare i documenti PDF applicando firme digitali utilizzando tecnologie PKI (Public Key Infrastructure) standard
* Inviare elettronicamente documenti PDF completati o con annotazioni
* Utilizzare i documenti e i moduli di PDF come front-end di sviluppo intuitivo per i database interni e i servizi Web
* Condividere documenti PDF con altri utenti in modo che i revisori possano aggiungere commenti utilizzando strumenti di markup intuitivi. Questi strumenti includono note adesive elettroniche, timbri, evidenziazioni e barrati di testo. Le stesse funzioni sono disponibili in Acrobat.
* Supporto della decodifica di moduli con codice a barre.

Queste speciali funzionalità utente vengono attivate automaticamente quando si apre un documento PDF con abilitazione per i diritti in Adobe Reader. Una volta terminato di lavorare con un documento abilitato ai diritti, tali funzioni vengono nuovamente disabilitate in Adobe Reader. Rimangono disattivati finché l’utente non riceve un altro documento PDF con abilitazione per i diritti.

Il servizio DocAssurance non è immediatamente disponibile. Per configurare il servizio DocAssurance, vedere [Installazione e configurazione di Document Services](../../forms/using/install-configure-document-services.md).

## Invia a servizio stampante {#send-to-printer-service}

Il servizio Send To Printer fornisce l&#39;API per inviare documenti alla stampante specificata per la stampa.
