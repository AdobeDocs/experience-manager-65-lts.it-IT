---
title: Creare un modulo adattivo
description: Scopri come creare un modulo adattivo utilizzando  [!DNL Experience Manager Forms]. I Forms adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondisci le modalità di creazione di un modulo adattivo basato su un modello di dati modulo e uno schema XML o JSON.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: eb857ab1-ab1b-4c77-af3b-4507f53a8241
source-git-commit: 254366c95c1aa1e3f5ba01441741a8dc1cfed42c
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 24%

---

# Creazione di componenti core basati su Adaptive Forms {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe consiglia di utilizzare i Componenti core per [aggiungere Forms adattivo a una pagina AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) o per [creare Forms adattivo autonomo](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=it) |
| AEM 6.5 | Questo articolo |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. AEM Forms fornisce un’interfaccia utente intuitiva per la creazione rapida di Adaptive Forms. L’interfaccia utente offre una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati e creare un modulo adattivo.

Prima di iniziare, scopri i tipi di componenti dei moduli disponibili:

* [Componenti core dei moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it): si tratta di componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può facilmente personalizzare e assegnare uno stile a questi componenti. Adobe consiglia di utilizzare questi componenti moderni ed estensibili per sviluppare Forms adattivo.

* [Componenti di base dei moduli adattivi](creating-adaptive-form.md): si tratta dei classici (precedenti) componenti di acquisizione dati. Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando moduli, Adobe consiglia di utilizzare [Componenti core Forms adattivi](/help/forms/using/create-adaptive-form.md) per creare un Forms adattivo.

## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* **Abilita componenti core Forms adattivi per l&#39;ambiente**: è necessario il progetto Archetipo AEM versione 41 o successiva per [abilitare i componenti core per l&#39;ambiente](/help/forms/using/enable-adaptive-forms-core-components.md). Quando si abilitano i Componenti core per l&#39;ambiente, il modello **Forms adattivo (Componente core)** e il tema Canvas vengono aggiunti all&#39;ambiente.

* **Un modello di modulo adattivo**: un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. Fornisce inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’aspetto, mentre l’azione di invio definisce l’azione da intraprendere al momento dell’invio di un modulo adattivo. Puoi anche distribuire [modelli di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it) nel tuo ambiente. che consentono di iniziare a creare rapidamente i moduli.

  >[!NOTE]
  >
  > Se non disponi del modello **Moduli adattivi (componente core)** nell’ambiente, [abilita la funzione Componenti core dei moduli adattivi per il tuo ambiente](/help/forms/using/enable-adaptive-forms-core-components.md). Quando abiliti i componenti core per il tuo ambiente, viene aggiunto il modello **Moduli adattivi (componente core)**.

* **Un tema per moduli adattivi**: un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti.  Il tema `Canvas` viene aggiunto per impostazione predefinita quando si abilitano i Componenti core per il proprio ambiente. Puoi [scaricare e personalizzare i temi standard](create-or-customize-themes-for-adaptive-forms-core-components.md). Per **temi predefiniti** puoi distribuire [temi di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it) nel tuo ambiente. In questo modo è possibile iniziare a definire lo stile dei moduli e fornire una struttura di base per creare o personalizzare un tema in base alle proprie esigenze aziendali.

* **Autorizzazioni**: aggiungi gli utenti a un gruppo [!DNL forms-users]. I membri del gruppo [!DNL forms-users] dispongono delle autorizzazioni per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici per moduli, consulta [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Creare un modulo adattivo {#create-an-adaptive-form}

1. Accedi alla tua [istanza Autore AEM locale](/help/sites-deploying/deploy.md#author-and-publish-installs).

1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Crea Forms adattivo]**.

1. Seleziona un modello di Componenti core Forms adattivi e fai clic su **[!UICONTROL Avanti]**.

1. Viene visualizzato **[!UICONTROL Aggiungi proprietà]**. Specificare i valori per i seguenti campi proprietà. I campi Titolo e Nome sono obbligatori:

   * **[!UICONTROL Titolo:]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell’interfaccia utente di [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** specifica il nome del modulo. Nell’archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo del nome può contenere solo caratteri alfanumerici, trattini e trattini bassi.
   * **[!UICONTROL Descrizione:]** Specifica le informazioni dettagliate sul modulo.
   * **[!UICONTROL Libreria client temi]:** Specifica il tema per un modulo adattivo. Per impostazione predefinita, il tema `adaptiveform.theme.canvas3` è selezionato. Puoi anche scegliere un tema diverso dal menu a discesa **[!UICONTROL Libreria client tema]**.
   * **[!UICONTROL Contenitore configurazione:]** definisce un percorso in cui vengono archiviati i file di configurazione per Adaptive Forms. Questi file di configurazione contengono impostazioni e proprietà relative al comportamento e all’aspetto di Adaptive Forms.
   * **[!UICONTROL Tag:]** specifica i tag per identificare in modo univoco il modulo adattivo. Aiuto sui tag nella ricerca nel modulo. Per creare i tag, digitare i nuovi nomi dei tag nella casella **[!UICONTROL Tag]**.
1. Seleziona **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.


1. Seleziona **[!UICONTROL Modifica]** per aprire il modulo appena creato in una nuova scheda. Il modulo si apre per la modifica e visualizza il contenuto disponibile nel modello. Viene inoltre visualizzata la barra laterale per personalizzare il modulo appena creato.


## Utilizzare i componenti core di Forms adattivi per creare il modulo

Dopo aver aperto il modulo per la modifica, puoi utilizzare i componenti core Forms adattivi disponibili per aggiungere campi modulo al modulo. È possibile trascinare o utilizzare l&#39;opzione + [inserisci componente] per aggiungere questi componenti a un modulo. Per informazioni sui [Componenti core adattivi di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it#components) disponibili, consulta la documentazione dei Componenti core di AEM. Puoi anche visitare [https://aemcomponents.dev/](https://aemcomponents.dev/) per visualizzare i componenti core disponibili in azione.

## Configurare l’azione di invio per un modulo adattivo {#configure-submit-action-for-form}

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante Invia in un modulo adattivo. I moduli adattivi includono alcune azioni di invio pronte all’uso. Puoi anche estendere un’azione di invio predefinita per creare un’azione di invio personalizzata. Per configurare un&#39;azione di invio per il modulo:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).

1. Fare clic sulla scheda **[!UICONTROL Invio]**.

   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare un&#39;azione di invio](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Seleziona e configura un&#39;azione **[!UICONTROL Invia]** in base alle tue esigenze. Per informazioni dettagliate sulle azioni di invio, consulta [Azione di invio modulo adattivo](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Reindirizza l’utente a una pagina o mostra un messaggio di ringraziamento all’invio del modulo

All&#39;invio di un modulo è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o a un messaggio. Per reindirizzare l’utente o configurare il messaggio di ringraziamento:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri la scheda **[!UICONTROL Invio]**.

   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare una pagina di reindirizzamento o un messaggio di ringraziamento](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Per configurare un URL di reindirizzamento, per l&#39;opzione Invia selezionare l&#39;opzione **[!UICONTROL Reindirizza all&#39;URL]**, quindi sfogliare e selezionare una pagina AEM Sites o specificare l&#39;URL di una pagina esterna.

   * Per configurare un messaggio personalizzato o di ringraziamento, per l&#39;opzione Invia selezionare l&#39;opzione **[!UICONTROL Mostra messaggio]** e specificare un messaggio nella casella **[!UICONTROL Contenuto messaggio]**. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.

## Configurare uno schema o un modello di dati del modulo per un modulo adattivo {#configure-schema-or-data-model-for-form}

È possibile utilizzare il modello dati modulo per collegare un modulo a un’origine dati per inviare e ricevere dati in base alle azioni degli utenti. È possibile anche collegare un modulo a uno schema JSON per ricevere i dati inviati in un formato predefinito. In base al requisito, connetti il modulo a uno schema JSON o a un modello di dati del modulo:

* [Crea uno schema JSON e carica nell&#39;ambiente](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Crea modello dati modulo](/help/forms/using/create-form-data-models.md)

### Configurare uno schema JSON o un modello dati modulo per il modulo

Per configurare uno schema JSON o un modello dati modulo per il modulo:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri la scheda **[!UICONTROL Modello dati]**.

   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare uno schema JSON o un modello dati modulo](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Seleziona e configura uno schema JSON o un modello dati modulo, in base ai requisiti:

   * Quando si seleziona l&#39;opzione **[!UICONTROL Modello modulo]**, utilizzare l&#39;opzione **[!UICONTROL Seleziona modello dati modulo]** per selezionare un modello dati modulo preconfigurato.
   * Quando selezioni l&#39;opzione **[!UICONTROL Schema]**, utilizza l&#39;opzione **[!UICONTROL Schema]** per selezionare uno schema JSON per il modulo.

1. Fai clic su **[!UICONTROL Fine]**.

>[!NOTE]
>
> Puoi modificare lo schema JSON o il modello dati del modulo per un modulo adattivo utilizzando le proprietà Contenitore guida.

## Configurare un servizio di precompilazione  {#configure-prefill-service-for-form}

Puoi utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Operazioni disponibili:

* [Creare un servizio di precompilazione personalizzato](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Utilizza il servizio di precompilazione del modello dati del modulo](#fdm-prefill-service)

### Utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo {#fdm-prefill-service}

È possibile utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo utilizzando un modello dati modulo o un servizio di precompilazione personalizzato. Il servizio di precompilazione del modello dati modulo utilizza il servizio [Get Service del modello dati modulo configurato](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) per recuperare i dati. Per utilizzare il servizio di precompilazione del modello dati modulo per un modulo adattivo:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare una pagina di reindirizzamento o un messaggio di ringraziamento](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Seleziona un modello di dati modulo. Apri la scheda **[!UICONTROL Base]**. Nel servizio di precompilazione, selezionare **[!UICONTROL Servizio di precompilazione modello dati modulo]**.
1. Fai clic su **[!UICONTROL Fine]**. Il modulo adattivo è ora configurato per l’utilizzo della precompilazione del modello dati del modulo. Ora puoi utilizzare l&#39;[editor regole](rule-editor.md) per creare regole per precompilare i campi del modulo.

## Come rinominare un modulo adattivo AEM?{#rename-an-AEM-Adaptive-Form}

Per rinominare un modulo adattivo, effettua le seguenti operazioni:

1. Seleziona un modulo adattivo nell’interfaccia utente di AEM Forms.
1. Fai clic su **Proprietà** nella barra superiore.

   ![Proprietà](/help/forms/using/assets/rename-form-properties.png)

1. Modifica il nome del modulo nella scheda **Titolo**, come illustrato nell&#39;immagine seguente.
1. Fare clic su **Salva e chiudi**.

   ![Rinominare un modulo adattivo AEM](/help/forms/using/assets/rename-form-title.png)


<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## Passaggio successivo

* [Utilizza l’editor di regole per aggiungere un comportamento dinamico al modulo](rule-editor.md)
* [Creazione o personalizzazione di temi per Forms adattivo basato su Componenti core](create-or-customize-themes-for-adaptive-forms-core-components.md)


## Consulta anche

* [Creare componenti core basati sul modulo adattivo](create-an-adaptive-form-core-components.md)
* [Creare o aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Modelli di temi di esempio e modelli di dati modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it)
