---
title: Integrazione di Salesforce con AEM Forms tramite il flusso delle credenziali del client OAuth 2.0
description: Passaggi per integrare l’integrazione di Salesforce con AEM Forms utilizzando il flusso di credenziali del client OAuth 2.0
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
exl-id: 56b4a767-1210-47f3-b022-766b0dda9943
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# Integrazione di Salesforce tramite il flusso di credenziali client OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

## Applicabile a {#applies-to}

Questa documentazione si applica a **AEM 6.5 LTS Forms**.

Per la documentazione di AEM as a Cloud Service, consulta [AEM Forms su Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration).

Puoi utilizzare le credenziali client OAuth 2.0 per integrare AEM Forms con l’applicazione Salesforce. Le credenziali client OAuth 2.0 sono un metodo standard e sicuro per la comunicazione diretta senza il coinvolgimento dell’utente.

![Flusso di lavoro durante l&#39;impostazione della comunicazione tra l&#39;applicazione AEM Forms e Salesforce](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms scambia le credenziali del client (chiave consumer e segreto consumer), definite nell’applicazione connessa Salesforce, per ottenere un token di accesso.

L’utilizzo delle credenziali del client OAuth 2.0 per l’autenticazione rispetto all’autenticazione del flusso del codice di autorizzazione offre diversi vantaggi:

* L&#39;autenticazione delle credenziali client OAuth 2.0 consente più di cinque connessioni per utente.
* La configurazione dell’origine dati di AEM continua a funzionare su disattivazione, modifiche all’accesso, aggiornamento della password per un utente di AEM.

## Prerequisiti {#prerequisites}

Prima di impostare la comunicazione tra un’applicazione Salesforce e un ambiente AEM:

* Crea un&#39;app connessa a [Salesforce con flusso di credenziali client OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5) e un utente solo API per la tua organizzazione e ottieni la chiave consumer e il segreto consumer per l&#39;app.

* Assicurati che il file Swagger sia configurato in modo appropriato per corrispondere alle API della tua organizzazione. In alternativa, puoi scegliere di [creare un file Swagger](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api) da zero, adatto all&#39;utilizzo nell&#39;ambiente AEM.
>[!NOTE]
>
> AEM 6.5 supporta solo le specifiche di file Swagger 2.0.

+++

## Passaggi per configurare Salesforce con il flusso delle credenziali del client {#steps-to-create-aem-datasource-configuration}

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Origini dati]**.
1. Seleziona la cartella di configurazione.
1. Fai clic su **[!UICONTROL Crea]** per visualizzare **[!UICONTROL Crea configurazione Data Source]**.
1. Specifica il **[!UICONTROL Titolo]** e seleziona il **[!UICONTROL Tipo di servizio]** come **[!UICONTROL Servizio RESTful]**.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona **[!UICONTROL Swagger Source]** come **[!UICONTROL File].**
   >[!NOTE]
   >
   > Non appena il file Swagger viene selezionato, lo Schema, il nome host e il percorso di base vengono popolati automaticamente.

1. Carica il file Swagger creato dal computer locale facendo clic su **[!UICONTROL Sfoglia]**.
1. Selezionare **[!UICONTROL Tipo di autenticazione]** come **[!UICONTROL OAuth 2.0]** e viene visualizzato il pannello **[!UICONTROL Impostazioni autenticazione]**.
1. Selezionare **[!UICONTROL Tipo di concessione]** come **[!UICONTROL Credenziali client]**.
1. Specifica l&#39;**[!UICONTROL ID client]** e il **[!UICONTROL Segreto client]** ottenuti dall&#39;app connessa a Salesforce.
1. Specifica l&#39;**[!UICONTROL URL token di accesso]** in formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Ogni organizzazione ha il proprio nome di dominio specifico.

1. Fare clic su **[!UICONTROL Verifica connessione]**.
1. Se la connessione riesce, fare clic sul pulsante **[!UICONTROL Crea]**.

Ora puoi [creare il modello dati del modulo](/help/forms/using/create-form-data-model.md) per integrare l&#39;origine dati configurata con il Forms adattivo.
