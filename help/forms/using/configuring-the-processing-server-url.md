---
title: Configurazione delle impostazioni di AEM DS
description: Scopri come specificare l’URL del server di elaborazione prima di inviare un modulo.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 8ad3afd6-e1c6-4f21-bb0f-4d97ef50710e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Configurazione delle impostazioni di AEM DS{#configuring-aem-ds-settings}

In questo articolo viene descritto come configurare il **Servizio impostazioni di AEM DS**. Questa impostazione può essere utilizzata in più scenari, ad esempio:

* Nella gestione della corrispondenza

   * Per la configurazione di AEM Forms Workflow
   * Quando si utilizza il portale Forms per il salvataggio remoto di bozze/invii

* Nei moduli adattivi, nei casi in cui un modulo adattivo viene inviato dall’istanza di pubblicazione

Di seguito sono riportati i passaggi per configurare le **[!UICONTROL impostazioni di AEM DS]**:

1. Apri Configuration Manager nell’istanza di pubblicazione utilizzando l’URL:\
   *https://localhost:port/system/console/configMgr*.

   ![Configurazione console Web AEM](assets/web_configuration_console_new.png)

1. Nella finestra **[!UICONTROL Configurazione console Web Adobe Experience Manager]**, individuare e fare clic sull&#39;opzione **[!UICONTROL Impostazioni DS AEM]**.

   ![Impostazioni DS](assets/ds_settings_new.png)

1. Nella finestra **[!UICONTROL Servizio impostazioni di AEM DS]** sono visualizzate le impostazioni di configurazione comuni per i componenti di AEM DS.

   ![Servizio impostazioni DS](assets/ds_settings_service_new.png)

1. Aggiungi le seguenti informazioni nei rispettivi campi:

   **[!UICONTROL URL server di elaborazione]**: il server di elaborazione è il server in cui deve essere attivato il flusso di lavoro di Forms o AEM. Può essere lo stesso dell’URL dell’istanza di authoring di AEM o dell’altro URL del server (ovvero, https://localhost:port/).

   **[!UICONTROL Elaborazione nome utente server]**: nome utente dell&#39;utente del flusso di lavoro [in base all&#39;URL del server utilizzato]

   **[!UICONTROL Elaborazione password server]**: password utente flusso di lavoro

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Quando si utilizzano flussi di lavoro Forms o AEM, prima di effettuare qualsiasi invio dal server di pubblicazione è necessario configurare il servizio delle impostazioni DS. In caso contrario, la presentazione del modulo non avrà esito positivo.
   >    
   >
