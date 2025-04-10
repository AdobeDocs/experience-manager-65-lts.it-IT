---
title: Guida rapida all’authoring delle pagine
description: Guida rapida di alto livello alle azioni chiave per l’authoring dei contenuti di una pagina
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 5a962fd3-33bb-44df-a48d-416a04f393eb
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 60%

---

# Guida rapida all’authoring delle pagine{#quick-guide-to-authoring-pages}

Queste procedure sono intese come guida rapida (di alto livello) alle azioni chiave per l’authoring dei contenuti di pagine in AEM.

Si occupano di:

* Non sono intese come copertura completa.
* Fornisci collegamenti alla documentazione dettagliata.

Per maggiori dettagli sull’authoring con AEM consulta:

* [Primi passaggi per gli autori](/help/sites-authoring/first-steps.md)
* [Authoring delle pagine](/help/sites-authoring/page-authoring.md)

## Alcuni suggerimenti rapidi {#a-few-quick-hints}

Prima di fornire una panoramica delle specifiche, ecco una piccola raccolta di suggerimenti generali che vale la pena tenere a mente.

### Console Sites {#sites-console}

* **Crea**

   * Questo pulsante è disponibile in molte console; le opzioni visualizzate sono contestuali e quindi possono variare a seconda dello scenario.

* Riordinamento delle pagine in una cartella

   * Questa operazione può essere eseguita in [Vista elenco](/help/sites-authoring/basic-handling.md#list-view). Le modifiche vengono applicate e visualizzate in altre viste.

#### Authoring delle pagine {#page-authoring}

* Collegamenti di navigazione

   * ***I collegamenti non sono disponibili per la navigazione*** quando sei in modalità **Modifica**. Per spostarti con i collegamenti, devi [visualizzare l&#39;anteprima della pagina](/help/sites-authoring/editing-content.md#previewing-pages) utilizzando:

      * [Modalità Anteprima](/help/sites-authoring/editing-content.md#preview-mode)
      * [Visualizza come pubblicato](/help/sites-authoring/editing-content.md#view-as-published)

* Le versioni non vengono avviate/create dall&#39;editor di pagine, questa operazione è ora eseguita dalla console Sites (tramite **Crea** o [Timeline](/help/sites-authoring/basic-handling.md#timeline) per una risorsa selezionata).

>[!NOTE]
>
>Esistono diverse scelte rapide da tastiera che possono semplificare l’esperienza di authoring.
>
>* [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Scelte rapide da tastiera per le console](/help/sites-authoring/keyboard-shortcuts.md)
>

### Ricerca di una pagina {#finding-your-page}

Sono disponibili vari aspetti per individuare una pagina. Puoi navigare e/o eseguire ricerche:

1. Apri la console **Sites** (utilizzando l&#39;opzione **Sites** nella [Navigazione globale](/help/sites-authoring/basic-handling.md#global-navigation)). Questa operazione viene attivata (a discesa) quando selezioni il collegamento Adobe Experience Manager (in alto a sinistra).

1. Per spostarti verso il basso nella struttura, tocca o fai clic sulla pagina appropriata. La modalità di rappresentazione delle risorse di pagina dipende dalla visualizzazione in uso - [Scheda, Elenco o Colonna](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources):

   ![schermata_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Spostati verso l&#39;alto nella struttura utilizzando [la breadcrumb nell&#39;intestazione](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs), che consente di tornare alla posizione selezionata:

   ![qgtap-01](assets/qgtap-01.png)

1. È inoltre possibile eseguire la [Ricerca](/help/sites-authoring/search.md) di una pagina. Puoi selezionare la pagina dai risultati mostrati.

   ![qgtap-03](assets/qgtap-03.png)

### Creazione di una nuova pagina {#creating-a-new-page}

Per [creare una pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [Passare al percorso](#finding-your-page) in cui si desidera creare la pagina.
1. Utilizza l’icona **Crea** e seleziona **Pagina** dall’elenco:

   ![qgtap-02](assets/qgtap-02.png)

1. Verrà aperta la procedura guidata che ti guiderà attraverso la raccolta delle informazioni necessarie durante la [creazione della nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page). Seguire le istruzioni visualizzate.

### Selezione della pagina per ulteriori azioni {#selecting-your-page-for-further-action}

Puoi selezionare una pagina in modo da poter intervenire su di essa. Quando si seleziona una pagina, la barra degli strumenti viene aggiornata automaticamente in modo da visualizzare le azioni relative a tale risorsa.

La modalità di selezione di una pagina dipende dalla visualizzazione utilizzata nella console:

1. Vista a colonne:

   * Fai clic sulla miniatura della risorsa richiesta; sulla miniatura compare un segno di spunta per indicare che è stata selezionata.

1. Vista a elenco:

   * Fai clic sulla miniatura della risorsa richiesta; sulla miniatura compare un segno di spunta per indicare che è stata selezionata.

1. Vista a schede:

   * Attiva la modalità di selezione [selezionando la risorsa richiesta](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) con:

      * Dispositivo mobile: seleziona e mantieni
      * Desktop: [azione rapida](/help/sites-authoring/basic-handling.md#quick-actions) - icona di spunta:

   ![schermata_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * Sulla scheda compare un segno di spunta per indicare che è stata selezionata la pagina.

   >[!NOTE]
   >
   >Una volta attivata la modalità di selezione, l&#39;icona **Seleziona** (un segno di spunta) diventerà **Deseleziona** (un segno di spunta).

### Azioni rapide (solo vista a schede/desktop) {#quick-actions-card-view-desktop-only}

Sono disponibili delle [Azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions):

1. [Passa alla pagina](#finding-your-page) sulla quale desideri intervenire.
1. Passa il puntatore del mouse sulla scheda che rappresenta la risorsa desiderata; vengono visualizzate le azioni rapide:

   ![schermata_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Modifica del contenuto delle pagine {#editing-your-page-content}

1. [Passa alla pagina](#finding-your-page) da modificare.
1. [Apri la pagina per la modifica](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) tramite l’icona Modifica (matita):

   ![schermata_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   È accessibile da:

   * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa appropriata.
   * La barra degli strumenti, se la [pagina è stata selezionata](#selectiingyourpageforfurtheraction).

1. All’apertura dell’editor, puoi:

   * [Aggiungere un nuovo componente alla pagina](/help/sites-authoring/editing-content.md#inserting-a-component):

      * apertura del pannello laterale
      * selezione della scheda componenti (browser [componenti](/help/sites-authoring/author-environment-tools.md#components-browser))
      * trascinamento del componente richiesto sulla pagina.

     Il pannello laterale può essere aperto (e chiuso) con:

     ![Apri pannello laterale](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Modificare il contenuto di un componente esistente](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) sulla pagina:

      * Apri la barra degli strumenti del componente facendo clic su. Utilizza l’icona **Modifica** (matita) per aprire la finestra di dialogo.
      * Apri l’editor locale per il componente con la funzione di selezione e mantenimento o con un doppio clic lento. Vengono visualizzate le azioni disponibili (per alcuni componenti è una selezione limitata).
      * Per visualizzare tutte le azioni disponibili, entra in modalità a schermo intero utilizzando:

     ![Modalità a tutto schermo](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Configurare le proprietà di un componente esistente](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Apri la barra degli strumenti del componente facendo clic su. Utilizza l’icona **Configura** (chiave inglese) per aprire la finestra di dialogo.

   * [Sposta un componente](/help/sites-authoring/editing-content.md#moving-a-component) con una delle seguenti operazioni:

      * Trascina il componente richiesto nella nuova posizione.
      * Apri la barra degli strumenti del componente facendo clic su. Utilizza le icone **Taglia** e **Incolla** dove richiesto.

   * [Copiare (e incollare)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un componente:

      * Apri la barra degli strumenti del componente facendo clic su. Utilizza le icone **Copia** e **Incolla** come richiesto.

   >[!NOTE]
   >
   >È possibile utilizzare **Incolla** per collocare i componenti sulla stessa pagina o su una pagina differente. Se si incolla un componente in una pagina che era già aperta prima dell’operazione Taglia o Copia, sarà necessario aggiornare la pagina.

   * [Eliminare](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) un componente:

      * Apri la barra degli strumenti del componente facendo clic su, quindi utilizza l&#39;icona **Elimina**.

   * [Aggiungere annotazioni](/help/sites-authoring/annotations.md#annotations) alla pagina:

      * Selezionare la modalità **Annota** (icona a forma di fumetto). Aggiungi annotazioni utilizzando l&#39;icona **Aggiungi annotazione** (segno più). Esci dalla modalità di annotazione utilizzando la X in alto a destra.

     ![Annotazioni](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Visualizzare l’anteprima di una pagina](/help/sites-authoring/editing-content.md#preview-mode) (per vedere come apparirà nell’ambiente di pubblicazione)

      * Seleziona **Anteprima** dalla barra degli strumenti.

   * Torna alla modalità modifica (o seleziona un’altra modalità) utilizzando il selettore a discesa **Modifica**.

   >[!NOTE]
   >
   >Per spostarsi utilizzando i collegamenti nel contenuto, è necessario utilizzare la [modalità Anteprima](/help/sites-authoring/editing-content.md#preview-mode).

### Modifica delle proprietà pagina   {#editing-the-page-properties}

Esistono due metodi (principali) di [modifica delle proprietà di una pagina](/help/sites-authoring/editing-page-properties.md):

* Dalla console **Sites**:

   1. [Passa alla pagina](#finding-your-page) da pubblicare.
   1. Seleziona l’icona **Proprietà** da:

      * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa appropriata.
      * La barra degli strumenti, se la [pagina è stata selezionata](#selectiingyourpageforfurtheraction).

  ![schermata_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. Vengono visualizzate le proprietà della pagina. È possibile apportare le modifiche desiderate e poi selezionare Salva per applicarle

* Durante la [modifica della pagina](#editing-your-page-content):

   1. Apri il menu **Informazioni pagina**.
   1. Seleziona **Apri proprietà** per aprire la finestra di dialogo per la modifica delle proprietà.

  ![schermata_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### Pubblicazione della pagina (o annullamento della pubblicazione) {#publishing-your-page-or-unpublishing}

Esistono due metodi principali per la [pubblicazione della pagina](/help/sites-authoring/publishing-pages.md) (e anche di annullamento della pubblicazione):

* Dalla console **Sites**:

   1. [Passa alla pagina](#finding-your-page) da pubblicare.
   1. Seleziona l’icona **Pubblicazione rapida** da:

      * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa appropriata.
      * La barra degli strumenti, se la [pagina è stata selezionata](#selectiingyourpageforfurtheraction) (consente anche di accedere a [Pubblica più tardi](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

  ![schermata_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* Durante la [modifica della pagina](#editing-your-page-content):

   1. Apri il menu **Informazioni pagina**.
   1. Seleziona **Pubblica pagina**.

  ![schermata_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* L’annullamento della pubblicazione di una pagina dalla console può essere eseguito solo tramite l’opzione **Gestisci pubblicazione**, disponibile solamente nella barra degli strumenti (non tramite le azioni rapide).

  L’opzione **Annulla pubblicazione pagina** è ancora disponibile tramite il menu **Informazioni pagina** nell’editor.

  ![schermata_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

  Consulta [Pubblicazione delle pagine](/help/sites-authoring/publishing-pages.md#unpublishing-pages) per ulteriori informazioni.

### Spostamento, utilizzo di Copia e Incolla o eliminazione della pagina   {#move-copy-and-paste-or-delete-your-page}

Queste azioni possono essere tutte attivate nei seguenti modi:

1. [Passa alla pagina](#finding-your-page) da spostare, copiare e incollare o eliminare.
1. Seleziona l’icona Copia (e quindi Incolla), Sposta o Elimina, a seconda delle necessità, utilizzando:

   * [Azioni rapide (solo vista a schede/desktop)](#quick-actions-card-view-desktop-only) per la risorsa richiesta.
   * La barra degli strumenti, se la [pagina è stata selezionata](#selecting-your-page-for-further-action).

   Quindi, a seconda dell’azione:

   * Copia:

      * Passa alla nuova posizione e incolla.

   * Sposta:

      * Viene visualizzata la procedura guidata per raccogliere le informazioni necessarie per spostare la pagina. Seguire le istruzioni visualizzate.

   * Elimina:

      * Viene richiesto di confermare l’azione.

   >[!NOTE]
   >
   >Elimina non è disponibile come azione rapida.

### Blocco della pagina (e successivo sblocco) {#locking-your-page-then-unlocking}

[Il blocco di una pagina](/help/sites-authoring/editing-content.md#locking-a-page) non consente ad altri autori di utilizzarla mentre vi lavori. L’icona o il pulsante Blocca (e Sblocca) è disponibile:

* La barra degli strumenti, se la [pagina è stata selezionata](#selecting-your-page-for-further-action).
* Il [menu a discesa Informazioni pagina](#editing-the-page-properties) durante la modifica di una pagina.
* La barra degli strumenti della pagina durante la modifica di una pagina (quando la pagina è bloccata)

Ad esempio, l’icona Blocca ha l’aspetto di un lucchetto chiuso:

![schermata_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### Accesso ai riferimenti di pagina {#accessing-page-references}

[L&#39;accesso rapido ai riferimenti](/help/sites-authoring/author-environment-tools.md#references) a una pagina o da una pagina è disponibile nella barra laterale Riferimenti.

1. Seleziona l’icona **Riferimenti** dalla barra degli strumenti (prima o dopo aver [selezionato la pagina](#selecting-your-page-for-further-action)):

   ![schermata_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   Verrà visualizzato un elenco di tipi di riferimenti:

   ![schermata_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Fare clic sul tipo di riferimento richiesto per visualizzare ulteriori dettagli e, se necessario, eseguire ulteriori azioni.

### Creazione di una versione della pagina   {#creating-a-version-of-your-page}

Per creare una [versione](/help/sites-authoring/working-with-page-versions.md) di una pagina:

1. Per aprire la barra laterale Timeline, seleziona l’icona **[Timeline](/help/sites-authoring/basic-handling.md#timeline)** dalla barra degli strumenti (prima o dopo aver [selezionato la pagina](#selecting-your-page-for-further-action)):

   ![schermata_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. Fai clic sulla freccia su in basso a destra della colonna Timeline per visualizzare pulsanti aggiuntivi, tra cui **Salva come versione**.

   ![schermata_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Seleziona **Salva come versione** quindi **Crea**.

### Ripristino/confronto di una versione della pagina {#restoring-comparing-a-version-of-your-page}

Lo stesso meccanismo di base viene utilizzato per il ripristino e/o il confronto tra diverse versioni di una pagina:

1. Seleziona l’icona **[Timeline](/help/sites-authoring/basic-handling.md#timeline)** dalla barra degli strumenti (prima o dopo aver [selezionato la pagina](#selecting-your-page-for-further-action)):

   ![schermata_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Se una versione della pagina è già stata salvata, viene elencata nella Timeline.

1. Fare clic sulla versione che si desidera ripristinare. Verranno visualizzati pulsanti di azione aggiuntivi:

   * **Ripristina questa versione**

      * La versione viene ripristinata.

   * **Mostra differenze**

      * La pagina viene aperta evidenziando le differenze (tra le due versioni).
