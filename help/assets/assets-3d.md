---
title: Utilizzo di risorse 3D in Dynamic Media
description: Scopri come caricare, gestire, visualizzare e distribuire risorse 3D in Dynamic Media come esperienza coinvolgente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: f27b595b-24eb-444c-a598-6f70c59ed8fc
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 2%

---

# Utilizzare risorse 3D in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media consente di caricare, gestire, visualizzare e distribuire risorse 3D come esperienze coinvolgenti.

* Pubblicazione con un clic (utilizzando **[!UICONTROL Pubblicazione rapida]** sulla barra degli strumenti) di risorse 3D per generare un URL.
* Supporto ottimizzato per la visualizzazione di risorse 3D con il predefinito visualizzatore dimensionale interattivo di alta qualità basato su Adobe Dimension.
* Il componente WCM per contenuti multimediali 3D consente di aggiungere facilmente risorse 3D alle pagine Adobe Experience Manager Sites.

Non è necessaria alcuna configurazione aggiuntiva per utilizzare le risorse 3D in Dynamic Media.

![Scarpa in 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *Pagina dei dettagli di una scarpa tridimensionale.*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formati 3D supportati in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supporta i seguenti formati 3D.

Vedi anche [Formati 3D supportati](/help/assets/assets-formats.md).

| Estensione file 3D | Formato file | Tipo MIME | Note |
|---|---|---|---|
| GLB | Trasmissione GL binaria | model/gltf-binary | Include i materiali e le texture come un&#39;unica risorsa. |
| OBJ | File oggetto WaveFront 3D | application/x-tgif |  |
| STL | Stereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivio zip | model/vnd.usdz+zip | *Supporto solo per l&#39;acquisizione. Nessuna visualizzazione o interazione disponibile.* USDZ è un formato 3D proprietario che può essere visualizzato in modalità nativa dai dispositivi Safari e iOS. |

>[!NOTE]
>
>Il componente WCM per contenuti multimediali 3D e l’anteprima 3D nella pagina Dettagli di una risorsa non sono compatibili con la versione più recente di Chrome (97.x). Invece, per lavorare con risorse 3D, utilizza Firefox o Safari oppure una versione precedente di Chrome (96.x).

## Guida introduttiva: risorse 3D in Dynamic Media {#quick-start-three-d}

La seguente descrizione dettagliata del flusso di lavoro è progettata per aiutarti a iniziare rapidamente a utilizzare risorse 3D in modalità Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Le risorse 3D non sono supportate in modalità Dynamic Media - Hybrid.

Prima di lavorare con risorse 3D in Dynamic Media, assicurati che il tuo amministratore Experience Manager abbia già abilitato e configurato i servizi cloud per elementi multimediali dinamici in modalità Dynamic Media - Scene7.

Consulta [ConfigurE Dynamic Media Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) in Configurazione di Dynamic Media - Modalità Scene7 e [Risoluzione dei problemi di Dynamic Media - Modalità Scene7](/help/assets/troubleshoot-dms7.md).

1. **Carica risorse 3D**

   * [Carica le risorse 3D da utilizzare in Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formati di file 3D supportati per il caricamento in Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gestione risorse 3D**

   * Organizzare e cercare risorse 3D

      * [Organizza risorse digitali](/help/assets/organize-assets.md#organize-digital-assets).
      * [Cerca risorse 3D](/help/assets/search-assets.md).
      * [Utilizzare predicati personalizzati per filtrare i risultati della ricerca](/help/assets/search-assets.md#custompredicates).

   * Visualizzare risorse 3D

      * [Visualizzazione e interazione con risorse 3D](#viewing-three-d-assets).
      * [Gestisci predefinito visualizzatore dimensionale](/help/assets/managing-viewer-presets.md).

   * Utilizzare i metadati delle risorse 3D

      * [Gestione metadati per risorse digitali](/help/assets/metadata.md).
      * [Schemi metadati](/help/assets/metadata-schemas.md).

1. **Pubblicare risorse 3D**

   * [Pubblicare risorse 3D Dynamic Media statiche](#publishing-three-d-assets)
   * [Metodi alternativi per la pubblicazione di risorse Dynamic Media 3D tramite il visualizzatore dimensionale](#alternate-publish-methods)

## Informazioni sulla visualizzazione e l’interazione con risorse 3D {#viewing-three-d-assets}

Questa sezione descrive come visualizzare e interagire con le risorse 3D in due modi diversi: dalla pagina dei dettagli delle risorse e dal componente 3D Media di Experience Manager Sites.

Il visualizzatore 3D interattivo include, tra le altre cose, una raccolta di controlli interattivi della fotocamera che consentono di ruotare, ingrandire ed eseguire la panoramica della risorsa 3D.

Il tempo necessario per aprire una risorsa 3D nella visualizzazione della pagina Dettagli risorsa dipende da diversi fattori. Questi fattori includono ad esempio:

* Larghezza di banda al server.
* Latenze al server
* Complessità dell’immagine.

Inoltre, le funzionalità del computer client, ad esempio una workstation, un notebook o un dispositivo touch mobile, sono anch&#39;esse importanti da considerare quando si manipola la fotocamera in modo interattivo. Un sistema ragionevolmente potente con buone capacità grafiche può rendere l&#39;esperienza di visualizzazione 3D interattiva più fluida e più favorevole.

>[!TIP]
>
>Potete aprire il predefinito visualizzatore dimensionale nell&#39;Editor predefiniti visualizzatore per esercitarvi a navigare in una risorsa 3D senza dover prima caricare alcun file 3D. Il predefinito visualizzatore dimensionale dispone di una risorsa 3D incorporata con cui interagire.
>
>Consulta [Gestire i predefiniti visualizzatore](/help/assets/managing-viewer-presets.md).

## Visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa {#viewing-three-d-assets-from-asset-details-page}

Vedi anche [Anteprima delle risorse tramite l&#39;interfaccia software](/help/assets/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D dalla pagina dei dettagli della risorsa:**

1. Assicurati di aver caricato risorse 3D in Experience Manager.

   Consulta [Caricare le risorse 3D da utilizzare in Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. Da Experience Manager, nella pagina **[!UICONTROL Navigazione]**, passa a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Visualizza]** nell&#39;angolo superiore destro della pagina selezionare **[!UICONTROL Vista a schede]**.
1. Passa a una risorsa 3D che desideri visualizzare.
1. Seleziona la scheda della risorsa 3D.
1. Nella pagina di visualizzazione dei dettagli della risorsa 3D, effettua una delle seguenti operazioni:

   | Visualizzazione | Descrizione | Azione del mouse | Azione schermo tattile |
   | --- | --- | --- | --- |
   | **Ruota fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Fai clic con il pulsante sinistro del mouse e trascina. | Premete un solo dito e trascinate. |
   | **Sposta fotocamera** | Spostare la vista verso sinistra, destra, l&#39;alto o il basso. | Fare clic con il pulsante destro del mouse e trascinare. | Premete due dita + trascinate. |
   | **Zoom fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Rotellina di scorrimento. | Pizzico a due dita. |
   | **Reinserire la fotocamera** | Centra di nuovo la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic su. | Doppia selezione. |
   | **Reimposta** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione di visualizzazione al centro della risorsa 3D. L&#39;opzione Reimposta consente inoltre alla telecamera di essere più vicina o più lontana per mostrare l&#39;intera risorsa e una dimensione di visualizzazione ragionevole. |   |   |
   | **Modalità a tutto schermo** | Per accedere alla modalità a tutto schermo, seleziona l’icona Schermo intero nell’angolo inferiore destro della pagina. |   |   |

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Chiudi]** per tornare alla pagina Assets.

## Visualizzazione e interazione con una risorsa 3D all’interno di un componente 3D Media {#interacting-with-asset-inside-three-d-media-component}

Quando una pagina Web è in modalità **[!UICONTROL Modifica]**, non è possibile alcuna interazione con una risorsa 3D. Per rendere interattiva la risorsa, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell&#39;editor pagina con accesso completo alla funzionalità del componente multimediale 3D.

>[!IMPORTANT]
>
>Puoi eseguire questa attività solo dopo aver aggiunto un componente File multimediali 3D a una pagina web e aver assegnato una risorsa 3D al componente. Consulta [Aggiunta del componente 3D Media a una pagina Web](#adding-the-three-d-media-component-to-a-web-page) e [Assegnazione di una risorsa 3D a un componente 3D Media](#assigning-a-three-d-asset-to-the-component).

Vedi anche [Anteprima delle risorse tramite l&#39;interfaccia software](/help/assets/previewing-assets.md).

**Per visualizzare e interagire con una risorsa 3D all&#39;interno di un componente multimediale 3D:**

1. Quando una pagina Web è in modalità **[!UICONTROL Modifica]**, eseguire una delle operazioni seguenti:

   * Nella parte superiore destra della pagina, seleziona **[!UICONTROL Anteprima]** per accedere alla modalità **[!UICONTROL Anteprima]**.
   * Elimina `/editor.html` dall&#39;URL della pagina nel browser.

   ![risorsa 3D visualizzata nel componente 3D Media](/help/assets/assets-dm/3d-asset-in-3d-media.png)
Una risorsa 3D completamente interattiva visualizzata in modalità **[!UICONTROL Anteprima]**.

1. In modalità **[!UICONTROL Anteprima]**, eseguire una delle operazioni seguenti:

   | Visualizzazione | Descrizione | Azione del mouse | Azione schermo tattile |
   | --- | --- | --- | --- |
   | **Ruota fotocamera** | Ruota la vista attorno agli oggetti e alla scena 3D. | Fai clic con il pulsante sinistro del mouse e trascina. | Premete un solo dito e trascinate. |
   | **Sposta fotocamera** | Spostare la vista verso sinistra, destra, l&#39;alto o il basso. | Fare clic con il pulsante destro del mouse e trascinare. | Premete due dita + trascinate. |
   | **Zoom fotocamera** | Spostarsi all&#39;interno e all&#39;esterno delle aree della scena 3D. | Rotellina di scorrimento. | Pizzico a due dita. |
   | **Reinserire la fotocamera** | Centra di nuovo la fotocamera in un punto di un oggetto nella scena 3D. | Fare doppio clic su. | Doppia selezione. |
   | **Reimposta** | Nell’angolo in basso a destra della pagina, seleziona l’icona Ripristina per ripristinare il punto di destinazione di visualizzazione al centro della risorsa 3D. L&#39;opzione Reimposta consente inoltre alla telecamera di essere più vicina o più lontana per mostrare l&#39;intera risorsa e una dimensione di visualizzazione ragionevole. |   |   |
   | **Modalità a tutto schermo** | Per accedere alla modalità a tutto schermo, seleziona l’icona Schermo intero nell’angolo inferiore destro della pagina. |   |   |

## Informazioni sull&#39;utilizzo del componente 3D Media {#working-with-three-d-media-component}

Dynamic Media include un componente Dynamic Media 3D Media che puoi utilizzare in Adobe Experience Manager Sites per abilitare la visualizzazione interattiva di modelli 3D sulle pagine web.

* [Aggiungere il componente 3D Media al modello della pagina](#adding-three-d-media-component-to-page-template)
* [Aggiungere il componente 3D Media a una pagina web](#adding-the-three-d-media-component-to-a-web-page)
   * [Facoltativo - Configurare il componente 3D Media](#configuring-the-three-d-component)
* [Assegnare una risorsa 3D al componente File 3D](#assigning-a-three-d-asset-to-the-component)

## Aggiungere il componente 3D Media al modello della pagina {#adding-three-d-media-component-to-page-template}

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]**.
1. Passa al modello della pagina in cui desideri abilitare il componente 3D e seleziona il modello.
1. Seleziona **[!UICONTROL Modifica]** per aprire il modello.
1. Nella parte superiore destra della pagina, nel menu a discesa, selezionare la modalità **[!UICONTROL Struttura]**, se non è già attiva.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Selezionare un&#39;area vuota nell&#39;area **[!UICONTROL Contenitore di layout]**, quindi selezionarla e aprire la relativa barra degli strumenti associata.
1. Sulla barra degli strumenti, selezionare l&#39;icona **[!UICONTROL Policy]** per aprire **[!UICONTROL Policy Editor]**.
1. Nella sezione **[!UICONTROL Proprietà]**, nella scheda **[!UICONTROL Componenti consentiti]**, scorri fino a **[!UICONTROL Dynamic Media]**, quindi espandi l&#39;elenco e seleziona **[!UICONTROL 3D Media]**.
1. Seleziona **[!UICONTROL Fine]** per salvare le modifiche e chiudere **[!UICONTROL Editor criteri]**.

   Ora puoi inserire il componente Dynamic Media 3D Media in tutte le pagine che utilizzano questo modello.

## Aggiungere il componente 3D Media a una pagina web {#adding-the-three-d-media-component-to-a-web-page}

Se utilizzi Experience Manager come sistema di gestione dei contenuti web, puoi aggiungere risorse 3D alle pagine web tramite il componente Media 3D.

Vedi anche [Aggiungere risorse Dynamic Media alle pagine](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Per aggiungere il componente 3D Media in una pagina Web:**

1. Apri Experience Manager Sites e seleziona la pagina web alla quale desideri aggiungere il componente Dynamic Media 3D Media.
1. Seleziona l&#39;icona **[!UICONTROL Modifica]** (matita) per aprire la pagina nell&#39;editor pagina. Assicurarsi che la modalità **[!UICONTROL Modifica]** sia selezionata in alto a destra della pagina.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Sulla barra degli strumenti, seleziona l’icona Pannello laterale per attivare o disattivare la visualizzazione del pannello.

1. Nel pannello laterale, seleziona l&#39;icona del segno più per aprire l&#39;elenco **[!UICONTROL Componenti]**.

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. Trascina il componente **[!UICONTROL File 3D]** dall&#39;elenco **[!UICONTROL Componenti]** nella posizione nella pagina in cui vuoi visualizzare il visualizzatore 3D.

Ora puoi assegnare una risorsa 3D al componente.

Consulta [Assegnare una risorsa 3D al componente 3D Media](#assigning-a-three-d-asset-to-the-component).

### Facoltativo - Configurare il componente 3D Media {#configuring-the-three-d-component}

1. Nell&#39;editor pagina di Experience Manager Sites, selezionare il componente **[!UICONTROL Visualizzatore file multimediali 3D]** precedentemente aggiunto alla pagina.
1. Seleziona l&#39;icona **[!UICONTROL Configurazione]** (chiave inglese) per aprire la finestra di dialogo Configurazione componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Nella finestra di dialogo 3D Media, dall&#39;elenco a discesa Predefinito visualizzatore, selezionare **[!UICONTROL Dimensionale]** per assegnare il predefinito visualizzatore dimensionale al componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. Nell&#39;angolo superiore destro selezionare il segno di spunta per salvare le modifiche.

## Assegnare una risorsa 3D al componente File 3D {#assigning-a-three-d-asset-to-the-component}

Dopo aver aggiunto un componente 3D Media a una pagina web, puoi assegnargli una risorsa 3D.

Consulta [Aggiungere il componente 3D Media a una pagina Web](#adding-the-three-d-media-component-to-a-web-page).

**Per assegnare una risorsa 3D al componente File 3D:**

1. Nell&#39;editor pagina di Experience Manager Sites, seleziona l&#39;icona **[!UICONTROL Assets]** per aprire **[!UICONTROL Assets]** nel pannello laterale.
1. Nell&#39;elenco a discesa, selezionare **[!UICONTROL 3D]** per visualizzare solo i tipi di file di risorse 3D.
1. Nel pannello laterale, cerca o scorri fino alla risorsa 3D che desideri visualizzare nella pagina da modificare.
1. Trascina la risorsa 3D dal pannello laterale di Assets e rilasciala sul componente **[!UICONTROL 3D Media]** precedentemente aggiunto alla pagina.

   ![Assegna risorsa 3D al componente File 3D](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Quando una pagina Web è in modalità Experience Manager Sites **[!UICONTROL Modifica]**, il componente File 3D visualizza la risorsa 3D ma non è possibile alcuna interazione con la risorsa. Per rendere interattiva la risorsa, puoi utilizzare la funzione **[!UICONTROL Anteprima]** per visualizzare la pagina Web nell&#39;editor pagina con accesso completo alla funzionalità del componente multimediale 3D.

## Pubblicare risorse 3D Dynamic Media statiche {#publishing-three-d-assets}

Dynamic Media accetta vari formati di file 3D supportati come *contenuto statico* in Dynamic Media. Il contenuto statico consente di caricare e pubblicare risorse 3D, ma non è supportato il *adattamento di immagini* o variabili associato alla risorsa 3D. Il motivo è che Dynamic Media Imaging Server non riconosce i formati 3D. Di conseguenza, dopo aver pubblicato una risorsa 3D in Dynamic Media, disponi di un URL istantaneo da copiare. L’URL della risorsa 3D segue la consueta struttura URL di Dynamic Media. Tuttavia, a differenza delle risorse di immagini tradizionali in Dynamic Media, nell’URL della risorsa non è possibile modificare alcun parametro.

Vedi anche [Ottenere un URL per una risorsa statica](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa e a sinistra della sua data e ora viene visualizzata una piccola icona a forma di globo, per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

Se utilizzi Experience Manager come WCM, utilizza questo metodo di pubblicazione per aggiungere le risorse Dynamic Media 3D direttamente sulla pagina web.

Vedi anche [Pubblicare risorse Dynamic Media](publishing-dynamicmedia-assets.md).

Vedi anche [Pubblica pagine](/help/sites-authoring/publishing-pages.md).

**Per pubblicare risorse 3D Dynamic Media statiche:**

1. Apri una risorsa 3D (in formato GLB, OBJ o STL) per visualizzarla nella pagina dei dettagli della risorsa.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Seleziona **[!UICONTROL Chiudi]** per uscire dalla finestra di dialogo e tornare alla pagina dei dettagli della risorsa.
1. Dall&#39;elenco a discesa a sinistra del nome file della risorsa 3D, selezionare **[!UICONTROL Rappresentazioni]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. Seleziona **[!UICONTROL originale]**. Quando una risorsa 3D viene pubblicata (o &quot;attivata&quot;), il pulsante **[!UICONTROL URL]** viene visualizzato nell&#39;angolo inferiore sinistro della pagina se sono soddisfatte tutte le seguenti condizioni per le risorse 3D:
   * La risorsa 3D è un formato supportato (GLB, OBJ, STL e USDZ).
   * La risorsa 3D è stata acquisita in Dynamic Media Image Production System (IPS).
   * La risorsa 3D viene pubblicata.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Seleziona **[!UICONTROL URL]** per visualizzare l&#39;URL di produzione diretto della risorsa 3D che puoi copiare e utilizzare nelle pagine Web.

### Metodi alternativi per la pubblicazione di risorse Dynamic Media 3D tramite il visualizzatore dimensionale {#alternate-publish-methods}

Utilizza i due metodi seguenti per pubblicare risorse Dynamic Media 3D se *non* utilizzi Experience Manager come WCM.

* **[!UICONTROL URL]** - Utilizza **[!UICONTROL URL]** se utilizzi un sistema di gestione dei contenuti Web di terze parti e vuoi collegare le risorse Dynamic Media 3D alle tue pagine Web utilizzando il visualizzatore dimensionale.

  Consulta [Collegare gli URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorpora]** - Utilizza **[!UICONTROL Incorpora]** per visualizzare una risorsa 3D di Dynamic Media incorporata in una pagina Web utilizzando il visualizzatore dimensionale. Puoi copiare il codice da incorporare negli Appunti, per poi incollarlo nelle pagine web. La modifica del codice non è consentita nella finestra di dialogo **[!UICONTROL Incorpora]**.

  Vedi [Incorporare il video Dynamic Media, il visualizzatore di immagini o il visualizzatore dimensionale in una pagina Web](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
