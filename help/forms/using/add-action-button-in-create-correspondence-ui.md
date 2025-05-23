---
title: Aggiungi azione/pulsante personalizzato nell’interfaccia utente per la creazione di corrispondenza
description: Scopri come aggiungere un’azione/pulsante personalizzato nell’interfaccia utente per la creazione di corrispondenza
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 8294cbbe-f37f-41d0-b8e8-298f9413462e
source-git-commit: 79cce324382bada2e9aec107b8e494723bf490e9
workflow-type: tm+mt
source-wordcount: '1854'
ht-degree: 1%

---

# Aggiungere un pulsante di azione personalizzato nell’interfaccia utente per la creazione di corrispondenza {#add-custom-action-button-in-create-correspondence-ui}

## Panoramica {#overview}

La soluzione Gestione della corrispondenza consente di aggiungere azioni personalizzate all’interfaccia utente Crea corrispondenza.

Lo scenario di questo documento spiega come creare un pulsante nell’interfaccia utente per la creazione di corrispondenza per condividere una lettera come PDF di revisione allegato a un’e-mail.

### Prerequisiti {#prerequisites}

Per completare questo scenario, è necessario disporre dei seguenti elementi:

* Conoscenza di CRX e JavaScript
* Server LiveCycle

## Scenario: creare il pulsante nell&#39;interfaccia utente Crea corrispondenza per inviare una lettera per la revisione {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

L’aggiunta di un pulsante con un’azione (in questo caso, invia una lettera per la revisione) all’interfaccia utente per la creazione di corrispondenza include:

1. Aggiunta del pulsante all’interfaccia utente per la creazione di corrispondenza
1. Aggiunta della gestione delle azioni al pulsante
1. Aggiunta del processo LiveCycle per abilitare la gestione delle azioni

### Aggiungi il pulsante all’interfaccia utente Crea corrispondenza {#add-the-button-to-the-create-correspondence-user-interface}

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata `defaultApp` con un percorso/struttura simile alla cartella defaultApp (nella cartella di configurazione). Per creare la cartella, effettua le seguenti operazioni:

   1. Fare clic con il pulsante destro del mouse sulla cartella **defaultApp** nel percorso seguente e selezionare **Sovrapponi nodo**:

      /libs/fd/cm/config/defaultApp/

      ![Sovrapponi nodo](assets/1_defaultapp.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/config/defaultApp/

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** selezionata

      ![Sovrapponi nodo](assets/2_defaultappoverlaynode.png)

   1. Fai clic su **OK**.
   1. Fare clic su **Salva tutto**.

1. Crea una copia del file acmExtensionsConfig.xml (presente nel ramo /libs) nel ramo /apps.

   1. Vai a &quot;/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml&quot;

   1. Fare clic con il pulsante destro del mouse sul file acmExtensionsConfig.xml e selezionare **Copia**.

      ![Copia acmExtensionsConfig.xml](assets/3_acmextensionsconfig_xml_copy.png)

   1. Fare clic con il pulsante destro del mouse sulla cartella **defaultApp** in &quot;/apps/fd/cm/config/defaultApp/&quot; e selezionare **Incolla**.
   1. Fare clic su **Salva tutto**.

1. Fai doppio clic sulla copia di acmExtentionsConfig.xml appena creata nella cartella delle app. Il file viene aperto per la modifica.
1. Individua il seguente codice:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. Per inviare una lettera via e-mail, puoi utilizzare LiveCycle Forms Workflow. Aggiungi un tag customAction sotto il tag modelExtension in acmExtensionsConfig.xml come segue:

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![tag customAction](assets/5_acmextensionsconfig_xml.png)

   Il tag modelExtension dispone di un set di tag figlio customAction che configurano l’azione, le autorizzazioni e l’aspetto del pulsante di azione. Di seguito è riportato l’elenco dei tag di configurazione customAction:

   | **Nome** | **Descrizione** |
   |---|---|
   | nome | Nome alfanumerico dell’azione da eseguire. Il valore di questo tag è obbligatorio, deve essere univoco (all’interno del tag modelExtension) e deve iniziare con un alfabeto. |
   | etichetta | Etichetta da visualizzare sul pulsante di azione |
   | descrizione comando | Testo della descrizione del pulsante, visualizzato quando l’utente passa il puntatore sul pulsante. |
   | styleName | Nome dello stile personalizzato applicato al pulsante di azione. |
   | permissionName | L&#39;azione corrispondente viene visualizzata solo se l&#39;utente dispone dell&#39;autorizzazione specificata da permissionName. Quando si specifica permissionName come `forms-users`, tutti gli utenti hanno accesso a questa opzione. |
   | actionHandler | Nome completo della classe ActionHandler chiamata quando l&#39;utente fa clic sul pulsante. |

   A parte i parametri di cui sopra, ci possono essere configurazioni aggiuntive associate a un customAction. Queste configurazioni aggiuntive vengono rese disponibili al gestore tramite l&#39;oggetto CustomAction.

   | **Nome** | **Descrizione** |
   |---|---|
   | serviceName | Se un customAction contiene un tag figlio denominato serviceName, facendo clic sul pulsante o sul collegamento corrispondente viene chiamato un processo il cui nome è rappresentato dal tag serviceName. Assicurarsi che il processo abbia la stessa firma della lettera PostProcess. Aggiungi il prefisso &quot;Forms Workflow ->&quot; nel nome del servizio. |
   | Parametri contenenti il prefisso cm_ nel nome del tag | Se un customAction contiene tag figlio che iniziano con name cm_, durante la fase di post-elaborazione (che si tratti di Letter Post Process o del processo speciale rappresentato dal tag serviceName) questi parametri sono disponibili nel codice XML di input sotto il tag pertinente con il prefisso cm_ rimosso. |
   | actionName | Ogni volta che un processo di post è dovuto a un clic, il codice XML inviato contiene un tag speciale con un nome sotto il tag con il nome dell’azione utente. |

1. Fare clic su **Salva tutto**.

#### Creare una cartella locale con il file delle proprietà nel ramo /apps {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

Il file ACMExtensionsMessages.properties include etichette e messaggi di descrizione dei vari campi nell&#39;interfaccia utente Crea corrispondenza. Affinché le azioni/i pulsanti personalizzati funzionino, crea una copia di questo file nel ramo /apps.

1. Fare clic con il pulsante destro del mouse sulla cartella **locale** nel percorso seguente e selezionare **Sovrapponi nodo**:

   /libs/fd/cm/config/defaultApp/locale

1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

   **Percorso:** /libs/fd/cm/config/defaultApp/locale

   **Posizione sovrapposizione:** /apps/

   **Corrispondenza tipi di nodo:** selezionata

1. Fai clic su **OK**.
1. Fare clic su **Salva tutto**.
1. Fare clic con il pulsante destro del mouse sul file seguente e selezionare **Copia**:

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. Fare clic con il pulsante destro del mouse sulla cartella **locale** nel percorso seguente e selezionare **Incolla**:

   `/apps/fd/cm/config/defaultApp/locale/`

   Il file ACMExtensionsMessages.properties viene copiato nella cartella locale.

1. Per localizzare le etichette dell&#39;azione o del pulsante personalizzato appena aggiunto, creare il file ACMExtensionsMessages.properties per le impostazioni locali pertinenti in `/apps/fd/cm/config/defaultApp/locale/`.

   Ad esempio, per localizzare l’azione/pulsante personalizzato creato in questo articolo, crea un file denominato ACMExtensionsMessages_fr.properties con la seguente voce:

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   Allo stesso modo, in questo file è possibile aggiungere altre proprietà, ad esempio per la descrizione comando e lo stile.

1. Fare clic su **Salva tutto**.

#### Riavvia il bundle di blocchi predefiniti di Adobe Asset Composer {#restart-the-adobe-asset-composer-building-block-bundle}

Dopo aver apportato tutte le modifiche lato server, riavvia il bundle Adobe Asset Composer Building Block. In questo scenario, i file acmExtensionsConfig.xml e ACMExtensionsMessages.properties sul lato server vengono modificati e, pertanto, il bundle Adobe Asset Composer Building Block richiede un riavvio.

>[!NOTE]
>
>Potrebbe essere necessario cancellare la cache del browser.

1. Vai a `https://[host]:'port'/system/console/bundles`. Se necessario, accedi come amministratore.

1. Individua il bundle di blocchi predefiniti di Adobe Asset Composer. Riavvia il bundle: fai clic su Interrompi, quindi fai clic su Avvia.

   ![Blocco predefinito di Adobe Asset Composer](assets/6_assetcomposerbuildingblockbundle.png)

Dopo aver riavviato il bundle di Adobe Asset Composer Building Block, il pulsante personalizzato viene visualizzato nell’interfaccia utente per la creazione di corrispondenza. È possibile aprire una lettera nell’interfaccia utente Crea corrispondenza per visualizzare in anteprima il pulsante personalizzato.

### Aggiungi gestione azioni al pulsante {#add-action-handling-to-the-button}

Per impostazione predefinita, l’interfaccia utente per la creazione di corrispondenza presenta l’implementazione di ActionHandler nel file cm.domain.js nel percorso seguente:

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

Per la gestione delle azioni personalizzate, crea una sovrapposizione del file cm.domain.js nel ramo /apps di CRX.

La gestione dell’azione/pulsante al momento del clic sull’azione/pulsante include la logica per:

* Rendere visibile/invisibile l’azione appena aggiunta: operazione eseguita escludendo la funzione actionVisible().
* Abilitazione/disabilitazione dell’azione appena aggiunta: operazione eseguita escludendo la funzione actionEnabled().
* Gestione effettiva dell’azione quando l’utente fa clic sul pulsante: eseguita escludendo l’implementazione della funzione handleAction().

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de`. Se necessario, accedi come amministratore.

1. Nella cartella delle app, crea una cartella denominata `js` nel ramo /apps di CRX con una struttura simile a quella della cartella seguente:

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   Per creare la cartella, effettua le seguenti operazioni:

   1. Fare clic con il pulsante destro del mouse sulla cartella **js** nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** selezionata

   1. Fai clic su **OK**.
   1. Fare clic su **Salva tutto**.

1. Nella cartella js, crea un file denominato crcustomization.js con il codice per la gestione delle azioni del pulsante, seguendo la procedura riportata di seguito:

   1. Fare clic con il pulsante destro del mouse sulla cartella **js** nel percorso seguente e selezionare **Crea > Crea file**:

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      Denomina il file come customization.js.

   1. Fai doppio clic sul file ccrcustomization.js per aprirlo in CRX.
   1. Nel file, incolla il seguente codice e fai clic su **Salva tutto**:

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### Aggiungi il processo LiveCycle per abilitare l&#39;azione <span class="acrolinxCursorMarker"></code>gestione di  {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

In questo scenario, abilita i seguenti componenti, che fanno parte del file components.zip allegato:

* JAR del componente DSC (DSCSample.jar)
* Invia lettera per processo di revisione LCA (SendLetterForReview.lca)

Scarica e decomprimi il file components.zip per ottenere i file DSCSample.jar e SendLetterForReview.lca. Utilizzare questi file come specificato nelle procedure seguenti.
[Ottieni file](assets/components.zip)

#### Configurare LiveCycle Server per eseguire il processo LCA {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>Questo passaggio è necessario solo se siete in una configurazione OSGI e l&#39;integrazione LC è necessaria per il tipo di personalizzazione che state implementando.

Il processo LCA viene eseguito sul server LiveCycle e richiede l&#39;indirizzo del server e le credenziali di accesso.

1. Vai a `https://'[server]:[port]'/system/console/configMgr` e accedi come amministratore.
1. Individua la configurazione di Adobe LiveCycle Client SDK e fai clic su **Modifica** (icona Modifica). Viene visualizzato il pannello Configurazioni.

1. Immetti i dettagli seguenti e fai clic su **Salva**:

   * **Url server**: URL del server LC di cui viene utilizzato il codice del gestore di azioni nel servizio Send For Review.
   * **Nome utente**: nome utente amministratore del server LC
   * **Password**: password del nome utente amministratore

   ![Configurazione SDK client Adobe LiveCycle](assets/3_clientsdkconfiguration.png)

#### Installare LiveCycle Archive (LCA) {#install-livecycle-archive-lca}

Il processo LiveCycle richiesto che abilita il processo del servizio e-mail.

>[!NOTE]
>
>Per visualizzare le operazioni eseguite da questo processo o per creare un processo analogo, è necessario Workbench.

1. Accedi come amministratore all&#39;interfaccia utente di amministrazione del server LiveCycle® all&#39;indirizzo `https:/[lc server]/:[lc port]/adminui`.

1. Passa a **Home > Servizi > Applicazioni e servizi > Gestione applicazioni**.

1. Se l&#39;applicazione SendLetterForReview è già presente, ignorare i passaggi rimanenti di questa procedura, altrimenti continuare con i passaggi successivi.

   ![Applicazione SendLetterForReview nell&#39;interfaccia utente](assets/12_applicationmanagementlc.png)

1. Fai clic su **Importa**.

1. Fare clic su **Scegli file** e selezionare SendLetterForReview.lca.

   ![Seleziona il file SendLetterForReview.lca](assets/14_sendletterforreview_lca.png)

1. Fare clic su **Anteprima**.

1. Selezionare **Distribuisci risorse in fase di esecuzione al termine dell&#39;importazione**.

1. Fai clic su **Importa**.

#### Aggiunta di ServiceName all&#39;elenco di servizi di Inserisce nell&#39;elenco Consentiti di servizi di {#adding-servicename-to-the-allowlist-service-list}

Nel server di Experience Manager Experience Manager, indica i servizi LiveCycle a cui desideri accedere.

1. Accedere come amministratore a `https:/[host]:'port'/system/console/configMgr`.

1. Individua e fai clic su **Configurazione SDK client Adobe LiveCycle**. Viene visualizzato il pannello Configurazione SDK client Adobe LiveCycle.
1. Nell&#39;elenco Nome servizio fare clic sull&#39;icona + e aggiungere un serviceName **SendLetterForReview/SendLetterForReviewProcess**.

1. Fai clic su **Salva**.

#### Configurare il servizio e-mail {#configure-the-email-service}

In questo scenario, affinché Gestione della corrispondenza possa inviare un messaggio e-mail, configura il servizio e-mail nel server LiveCycle.

1. Accedi con le credenziali di amministratore all&#39;interfaccia utente di amministrazione di LiveCycle Server all&#39;indirizzo `https:/[lc server]:[lc port]/adminui`.

1. Passa a **Home > Servizi > Applicazioni e servizi > Gestione servizi**.

1. Individua e fai clic su **EmailService**.

1. In **Host SMTP**, configurare il servizio e-mail.

1. Fai clic su **Salva**.

#### Configurare il servizio DSC {#configure-the-dsc-service}

Per utilizzare l&#39;API di gestione della corrispondenza, scarica DSCSample.jar (allegato in questo documento come parte di components.zip) e caricalo sul server LiveCycle. Dopo che il file DSCSample.jar è stato caricato sul server LiveCycle, il server Experience Manager utilizza il file DSCSample.jar per accedere all’API renderLetter.

Per ulteriori informazioni, vedere [Connessione di AEM Forms con Adobe LiveCycle](/help/forms/using/aem-livecycle-connector.md).

1. Aggiorna l’URL del server Experience Manager in cmsa.properties in DSCSample.jar, che si trova nella seguente posizione:

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. Fornisci i seguenti parametri nel file di configurazione:

   * **crx.serverUrl**=https:/host:port/[percorso contestuale]/[URL AEM]
   * **crx.username**= nome utente Experience Manager
   * **crx.password**= password Experience Manager
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >Ogni volta che si apportano modifiche sul lato server, riavviare LiveCycle Server.

   Il file DSCSample.jar utilizza l’API renderLetter. Per ulteriori informazioni sull&#39;API renderLetter, vedere [Interface LetterRenderService](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

#### Importa DSC in LiveCycle {#import-dsc-to-livecyle}

Il file DSCSample.jar utilizza l&#39;API renderLetter per eseguire il rendering della lettera come byte PDF dai dati XML forniti da DSC come input. Per ulteriori informazioni su renderLetter e altre API, vedere [Servizio rendering lettere](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

1. Avvia Workbench e accedi.
1. Selezionare **Finestra > Mostra visualizzazioni > Componenti**. La vista Componenti viene aggiunta a Workbench ES2.

1. Fare clic con il pulsante destro del mouse su **Componenti** e selezionare **Installa componente**.

1. Seleziona il file **DSCSample.jar** tramite il browser dei file e fai clic su **Apri**.
1. Fare clic con il pulsante destro del mouse su **RenderWrapper** e selezionare **Avvia componente**. Se il componente viene avviato, accanto al nome del componente viene visualizzata una freccia verde.

## Invia lettera per revisione {#send-letter-for-review}

Dopo aver configurato l’azione e il pulsante per l’invio della lettera per la revisione:

1. Cancella la cache del browser.

1. Nell&#39;interfaccia utente per la creazione di corrispondenza, fare clic su **Revisione lettera** e specificare l&#39;ID e-mail del revisore.

1. Fai clic su **Invia**.

![sendreview](assets/sendreview.png)

Il revisore riceve un&#39;e-mail dal sistema con la lettera come allegato PDF.
