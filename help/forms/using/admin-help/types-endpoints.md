---
title: Tipi di endpoint
description: Scopri i diversi tipi di endpoint. Ai servizi è possibile aggiungere diversi tipi di endpoint, ad esempio E-mail, Cartella controllata e molto altro ancora.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Tipi di endpoint {#types-of-endpoints}

Prima di poter utilizzare un servizio, è necessario configurare e abilitare un endpoint. Un endpoint specifica la modalità di chiamata di un servizio.

>[!NOTE]
>
>In Workbench, gli endpoint sono denominati punti iniziali.

Ai servizi è possibile aggiungere i seguenti tipi di endpoint. Non tutti i servizi supportano tutti gli endpoint:

**E-mail:** consente a un utente di richiamare un servizio inviando un messaggio e-mail con uno o più file allegati a un account e-mail specificato. Prima di configurare un endpoint e-mail, è necessario configurare gli account e-mail richiesti. Consulta Configurazione degli endpoint e-mail.

**Cartella controllata:** consente a un utente di richiamare un servizio inserendo un file in una cartella, analizzata a un intervallo definito. Consulta Configurazione degli endpoint per cartelle controllate.

**TaskManager:** consente a un utente di Workspace di richiamare il servizio.

**Remoting:** consente a un&#39;applicazione generata con Flex di richiamare il servizio utilizzando (obsoleto per AEM forms) AEM forms Remoting. Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

**SOAP:** consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione AEM Forms di richiamare il servizio utilizzando la modalità SOAP. Per ogni servizio attivato viene creato automaticamente un endpoint SOAP.

**nota**: *È possibile rimuovere la protezione dai documenti di protezione dei documenti quando si utilizza l&#39;endpoint SOAP durante la visualizzazione dei documenti in Adobe Acrobat o Adobe Reader. Per informazioni dettagliate su come disabilitare gli endpoint SOAP nei documenti LCRM, vedere [Disabilitare gli endpoint SOAP per i documenti di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Abilita un&#39;applicazione client sviluppata utilizzando le API di programmazione di AEM Forms per richiamare il servizio utilizzando la modalità Enterprise JavaBeans (EJB). Per ogni servizio attivato viene creato automaticamente un endpoint EJB.

**WSDL:** consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione di AEM Forms di richiamare il servizio utilizzando il linguaggio WSDL (Web Service Definition Language). La pagina Configurazioni core contiene un&#39;opzione per abilitare la generazione WSDL per tutti i servizi che fanno parte di AEM Forms. Consulta Configurare le impostazioni generali di AEM Forms.

**REST:** I processi creati in Workbench possono essere configurati in modo da poterli richiamare tramite richieste REST (Managational State Transfer). Le richieste REST vengono inviate dalle pagine HTML. In altre parole, è possibile richiamare un processo AEM forms direttamente da una pagina web utilizzando una richiesta REST.

Gli endpoint E-mail, TaskManager, Cartella controllata e Remoting espongono solo un’operazione specifica del servizio. L&#39;aggiunta di questi endpoint richiede un secondo passaggio di configurazione per selezionare un metodo per richiamare il servizio, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.
