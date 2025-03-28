---
title: Utilizzo del CAPTCHA nei moduli adattivi
description: Scopri come configurare il servizio AEM CAPTCHA o Google reCAPTCHA nei moduli adattivi.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 300fcbdc-d884-409b-9011-89cdf2706535
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 7%

---

# Utilizzo del CAPTCHA nei moduli adattivi{#using-captcha-in-adaptive-forms}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/captcha-adaptive-forms.html?lang=it) |
| AEM 6.5 | Questo articolo |


<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Il CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) è un programma comunemente utilizzato nelle transazioni online per distinguere tra esseri umani e programmi o bot automatizzati. Rappresenta una sfida e valuta la risposta dell’utente per determinare se si tratta di un essere umano o di un bot che interagisce con il sito. Impedisce all’utente di procedere se il test non riesce e contribuisce a rendere sicure le transazioni online impedendo ai bot di pubblicare spam o avere scopi dannosi.

AEM Forms supporta il CAPTCHA nei moduli adattivi. Puoi utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA.

>[!NOTE]
>
>* AEM Forms supporta reCAPTCHA v2 ed enterprise. Qualsiasi altra versione non è supportata.
>* Il CAPTCHA nei moduli adattivi non è supportato in modalità offline nell’app AEM Forms.

## Configurare il servizio reCAPTCHA di Google per Adaptive Forms {#google-reCAPTCHA}

Gli utenti di AEM Forms possono utilizzare il servizio reCAPTCHA di Google per implementare CAPTCHA nei moduli adattivi. Offre funzionalità CAPTCHA avanzate per proteggere il sito. Per ulteriori informazioni sul funzionamento di reCAPTCHA, vedere [Google reCAPTCHA](https://developers.google.com/recaptcha/). Il servizio reCAPTCHA, che include reCAPTCHA v2 e reCAPTCHA Enterprise, è integrato in AEM Forms. In base alle tue esigenze puoi configurare il servizio reCAPTCHA per abilitare:

* [reCAPTCHA Enterprise in AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 in AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### Configurare reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Crea un progetto [reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) abilitato con [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [Ottieni](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) l&#39;ID progetto.
1. Creare una [chiave API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) e una [chiave sito per siti Web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crea un contenitore di configurazione per i servizi cloud.

   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.
      1. Nel Browser configurazioni, selezionare la cartella **[!UICONTROL global]** e selezionare **[!UICONTROL Proprietà]**.
      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   1. Nel browser configurazioni, selezionare **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Seleziona **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.
1. Configura il servizio cloud per reCAPTCHA Enterprise.

   1. Nell&#39;istanza Autore Experience Manager, vai a ![strumenti-1](assets/tools-1.png) > **[!UICONTROL Servizi cloud]**.
   1. Selezionare **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato nel passaggio precedente e seleziona **[!UICONTROL Crea]**.
   1. Seleziona la versione come Enterprise reCAPTCHA e specifica Nome; ID progetto, Chiave sito e Chiave API (ottenuta nei passaggi 2 e 3) per il servizio Enterprise reCAPTCHA.
   1. Selezionare il tipo di chiave. Il tipo di chiave deve essere uguale a quello configurato nel progetto cloud Google, ad esempio **Chiave sito di casella di controllo** o **Chiave sito basata su punteggio**.
   1. Specifica un punteggio di soglia nell&#39;intervallo 0-1 ([Fai clic per ulteriori informazioni sul punteggio](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)). I punteggi superiori o uguali ai punteggi di soglia identificano l’interazione umana, altrimenti considerata interazione da bot.

      > Nota:
      >
      > * Gli autori dei moduli possono specificare un punteggio nell’intervallo idoneo per l’invio ininterrotto di moduli.

   1. Seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.

   1. Nella finestra di dialogo Modifica componente, specifica il nome, l’ID progetto, la chiave del sito e la chiave API (ottenuta nei passaggi 2 e 3), seleziona il tipo di chiave e immetti il punteggio di soglia. Seleziona **[!UICONTROL Salva impostazioni]**, quindi seleziona **[!UICONTROL OK]** per completare la configurazione.

Una volta abilitato, il servizio reCAPTCHA Enterprise è disponibile per l’utilizzo in moduli adattivi. Vedi [utilizzo del CAPTCHA nei moduli adattivi](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### Configurare Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Ottieni la coppia di chiavi API [reCAPTCHA](https://www.google.com/recaptcha/admin) da Google. Include una **chiave del sito** e una **chiave segreta**.
1. Crea un contenitore di configurazione per i servizi cloud.
   1. Vai a **[!UICONTROL Strumenti > Generale > Browser configurazioni]**. Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
   1. Effettua le seguenti operazioni per abilitare la cartella globale per le configurazioni cloud oppure ignora questo passaggio per creare e configurare un’altra cartella per le configurazioni del servizio cloud.

      1. Nel Browser configurazioni, selezionare la cartella **[!UICONTROL global]** e selezionare **[!UICONTROL Proprietà]**.

      1. Nella finestra di dialogo Proprietà di configurazione, abilita **[!UICONTROL Configurazioni cloud]**.
      1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare la configurazione e uscire dalla finestra di dialogo.

   1. Nel browser configurazioni, selezionare **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella e abilita **[!UICONTROL Configurazioni cloud]**.
   1. Seleziona **[!UICONTROL Crea]** per creare la cartella abilitata per le configurazioni del servizio cloud.

1. Configura il servizio cloud per reCAPTCHA v2.

   1. Nell&#39;istanza Autore AEM, vai a ![strumenti-1](assets/tools-1.png) > **Servizi cloud**.
   1. Selezionare **[!UICONTROL reCAPTCHA]**. Viene visualizzata la pagina Configurazioni. Seleziona il contenitore di configurazione creato nel passaggio precedente e seleziona **[!UICONTROL Crea]**.
   1. Seleziona la versione come reCAPTCHA v2, specifica il nome, la chiave del sito e la chiave segreta per il servizio reCAPTCHA (ottenuti nel passaggio 1), quindi seleziona **[!UICONTROL Crea]** per creare la configurazione del servizio cloud.
   1. Nella finestra di dialogo Modifica componente, specifica il sito e le chiavi segrete ottenuti nel passaggio 1. Seleziona **[!UICONTROL Salva impostazioni]**, quindi seleziona **OK** per completare la configurazione.

   Una volta configurato, il servizio reCAPTCHA è disponibile per l’utilizzo nei moduli adattivi. Per ulteriori informazioni, vedi [utilizzo del CAPTCHA nei moduli adattivi](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## Utilizzare reCAPTCHA nei moduli adattivi {#using-reCAPTCHA}

Per utilizzare reCAPTCHA nei moduli adattivi:

1. Apri un modulo adattivo in modalità di modifica.

   >[!NOTE]
   >
   >Assicurati che il contenitore di configurazione selezionato durante la creazione del modulo adattivo contenga il servizio cloud reCAPTCHA. Puoi anche modificare le proprietà dei moduli adattivi per cambiare il contenitore di configurazione associato al modulo.

1. Dal browser componenti, trascina il componente **Captcha** nel modulo adattivo.

   >[!NOTE]
   >
   >L’utilizzo di più componenti Captcha in un modulo adattivo non è supportato. Inoltre, si sconsiglia di utilizzare il CAPTCHA in un pannello contrassegnato per il caricamento lento o in un frammento.

   >[!NOTE]
   >
   >Il Captcha è sensibile al tempo e scade tra circa un minuto. Pertanto, si consiglia di inserire il componente Captcha subito prima del pulsante Invia nel modulo adattivo.

1. Seleziona il componente Captcha aggiunto e seleziona ![cmppr](assets/cmppr.png) per modificarne le proprietà.
1. Specificate un titolo per il widget CAPTCHA. Il valore predefinito è **Captcha**. Selezionare **Nascondi titolo** se non si desidera visualizzare il titolo.
1. Dall&#39;elenco a discesa del servizio **Captcha**, selezionare **reCAPTCHA** per abilitare il servizio reCAPTCHA se è stato configurato come descritto nel servizio [reCAPTCHA da Google](#google-reCAPTCHA).
1. Seleziona una configurazione dal menu a discesa Impostazioni.
1. **Se la configurazione selezionata include la versione reCAPTCHA Enterprise**:
   1. È possibile selezionare la configurazione cloud reCAPTCHA con **tipo chiave** come **casella di controllo**. In tasto casella di controllo, digita il messaggio di errore personalizzato come messaggio in linea se la convalida captcha non riesce. È possibile selezionare le dimensioni come **[!UICONTROL Normale]** e **[!UICONTROL Compatta]**.
   1. È possibile selezionare la configurazione cloud reCAPTCHA con **tipo chiave** come **punteggio basato**. In chiave basata su punteggio, il messaggio di errore personalizzato viene visualizzato come messaggio a comparsa se la convalida captcha non riesce.
   1. Quando si seleziona un **[!UICONTROL Riferimento associazione]**, i dati inviati sono dati associati, altrimenti si tratta di dati non associati. Di seguito sono riportati alcuni esempi XML di dati non associati e dati associati (con riferimento di associazione come SSN) rispettivamente, quando un modulo viene inviato.

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **Se la configurazione selezionata include la versione reCAPTCHA v2**:
   1. Selezionare la dimensione come **[!UICONTROL Normale]** o **[!UICONTROL Compatta]** per il widget reCAPTCHA. È inoltre possibile selezionare l&#39;opzione **[!UICONTROL Invisibile]** per visualizzare la richiesta CAPTCHA solo se è presente un&#39;attività sospetta. Il badge **protetto da reCAPTCHA**, visualizzato di seguito, viene visualizzato nei moduli protetti.

      ![Google protetto da badge reCAPTCHA](/help/forms/using/assets/google-recaptcha-v2.png)


   Il servizio reCAPTCHA è abilitato nel modulo adattivo. Puoi visualizzare l’anteprima del modulo e vedere il CAPTCHA che funziona.

1. Salva le proprietà.

>[!NOTE]
> 
> Non selezionare **[!UICONTROL Default]** dal menu a discesa del servizio Captcha poiché il servizio AEM CAPTCHA predefinito è obsoleto.

### Mostrare o nascondere il componente CAPTCHA in base alle regole {#show-hide-captcha}

Puoi scegliere di mostrare o nascondere il componente CAPTCHA in base alle regole applicate a un componente in un modulo adattivo. Selezionare il componente, selezionare ![modifica regole](assets/edit-rules-icon.svg) e selezionare **[!UICONTROL Crea]** per creare una regola. Per ulteriori informazioni sulla creazione di regole, vedere [Editor regole](rule-editor.md).

Ad esempio, il componente CAPTCHA deve essere visualizzato in un modulo adattivo solo se il campo Valore valuta nel modulo ha un valore superiore a 25000.

Selezionare il campo **[!UICONTROL Valore valuta]** nel modulo e creare le regole seguenti:

![Mostra o nascondi regole](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * Se selezioni la configurazione reCAPTCHA v2 con dimensioni pari a **[!UICONTROL Invisible]** o le chiavi basate su punteggio Enterprise reCAPTCHA, l&#39;opzione mostra/nascondi non è applicabile.

### Convalida CAPTCHA {#validate-captcha}

È possibile convalidare il CAPTCHA in un modulo adattivo quando si invia il modulo oppure basare la convalida CAPTCHA sulle azioni e condizioni dell’utente.

#### Convalida CAPTCHA all’invio del modulo {#validation-form-submission}

Per convalidare automaticamente un CAPTCHA quando si invia un modulo adattivo:

1. Selezionare il componente CAPTCHA e selezionare ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. Nella sezione **[!UICONTROL Convalida CAPTCHA]**, seleziona **[!UICONTROL Convalida CAPTCHA all&#39;invio del modulo]**.
1. Seleziona ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

#### Convalida CAPTCHA per azioni e condizioni dell’utente {#validate-captcha-user-action}

Per convalidare un CAPTCHA in base a condizioni e azioni dell’utente:

1. Selezionare il componente CAPTCHA e selezionare ![cmppr](assets/configure-icon.svg) per visualizzare le proprietà del componente.
1. Nella sezione **[!UICONTROL Convalida CAPTCHA]**, selezionare **[!UICONTROL Convalida CAPTCHA per un&#39;azione utente]**.
1. Seleziona ![Fine](assets/save_icon.svg) per salvare le proprietà del componente.

   >[!NOTE]
   >
   >
   > Se selezioni la configurazione reCAPTCHA v2 con dimensioni pari a **[!UICONTROL Invisible]** o le chiavi basate su punteggio Enterprise reCAPTCHA, l&#39;opzione Captcha valido in un&#39;azione utente non è applicabile.

[!DNL Experience Manager Forms] fornisce l&#39;API `ValidateCAPTCHA` per convalidare CAPTCHA utilizzando condizioni predefinite. Puoi richiamare l’API utilizzando un’azione di invio personalizzata o definendo regole sui componenti in un modulo adattivo.

Di seguito è riportato un esempio di API `ValidateCAPTCHA` per convalidare CAPTCHA utilizzando condizioni predefinite:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
        GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

L&#39;esempio indica che l&#39;API `ValidateCAPTCHA` convalida il CAPTCHA nel modulo solo se il numero di cifre nella casella numerica specificata dall&#39;utente durante la compilazione del modulo è maggiore di 5.

**Opzione 1: utilizzare l&#39;API ValidateCAPTCHA [!DNL Experience Manager Forms] per convalidare CAPTCHA tramite un&#39;azione di invio personalizzata**

Per utilizzare l&#39;API `ValidateCAPTCHA` per convalidare il CAPTCHA tramite un&#39;azione di invio personalizzata, eseguire la procedura seguente:

1. Aggiungere lo script che include l&#39;API `ValidateCAPTCHA` all&#39;azione di invio personalizzata. Per ulteriori informazioni sulle azioni di invio personalizzate, vedere [Creare un&#39;azione di invio personalizzata per Forms adattivo](custom-submit-action-form.md).
1. Seleziona il nome dell&#39;azione di invio personalizzata dall&#39;elenco a discesa **[!UICONTROL Azione di invio]** nelle proprietà **[!UICONTROL Invio]** di un modulo adattivo.
1. Seleziona **[!UICONTROL Invia]**. Il CAPTCHA viene convalidato in base alle condizioni definite nell&#39;API `ValidateCAPTCHA` dell&#39;azione di invio personalizzata.

**Opzione 2: utilizzare l&#39;API ValidateCAPTCHA [!DNL Experience Manager Forms] per convalidare CAPTCHA in un&#39;azione utente prima di inviare il modulo**

È inoltre possibile richiamare l&#39;API `ValidateCAPTCHA` applicando regole a un componente in un modulo adattivo.

Ad esempio, puoi aggiungere un pulsante **[!UICONTROL Convalida CAPTCHA]** in un modulo adattivo e creare una regola per richiamare un servizio facendo clic su un pulsante.

Nella figura seguente viene illustrato come richiamare un servizio facendo clic su un pulsante **[!UICONTROL Convalida CAPTCHA]**:

![Convalida CAPTCHA](assets/captcha-validation1.gif)

È possibile richiamare il servlet personalizzato che include l&#39;API `ValidateCAPTCHA` utilizzando l&#39;editor di regole e abilitare o disabilitare il pulsante di invio del modulo adattivo in base al risultato della convalida.

Allo stesso modo, puoi utilizzare l’editor di regole per includere un metodo personalizzato per convalidare il CAPTCHA in un modulo adattivo.

<!--
### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` Refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` Refers to the `g_reCAPTCHA_response` that gets generated after solving a CAPTCHA in a form. -->
