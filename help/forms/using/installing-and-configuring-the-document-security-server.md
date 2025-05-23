---
title: Installazione e configurazione del server di Document Security
description: Utilizza Document Security per distribuire in modo sicuro le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti.
contentOwner: khsingh
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,Document Security
exl-id: 97b93a5f-cea7-4d79-8ee1-c6a94b7a6983
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Installazione e configurazione del server di Document Security {#installing-and-configuring-the-document-security-server}

Utilizza Document Security per distribuire in modo sicuro le informazioni salvate in un formato supportato. Solo gli utenti autorizzati possono accedere ai documenti protetti.

La funzione di protezione dei documenti di Adobe Experience Manager Forms garantisce che solo gli utenti autorizzati possano utilizzare i documenti. Grazie alla protezione dei documenti è possibile distribuire in modo sicuro le informazioni salvate in un formato supportato. I formati di file supportati sono Adobe Portable Document Format (PDF) e Microsoft Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando le policy. Le impostazioni di riservatezza specificate in una policy determinano il modo in cui un destinatario può utilizzare un documento al quale si applica la policy. È ad esempio possibile specificare se i destinatari possono stampare o copiare testo, modificare testo o aggiungere firme e commenti ai documenti protetti.

Le policy vengono memorizzate nel server di Document Security e applicate ai documenti tramite l’applicazione client. Quando si applica una policy a un documento, le impostazioni di riservatezza specificate nella policy proteggono le informazioni contenute nel documento. Puoi distribuire il documento protetto tramite policy ai destinatari autorizzati dalla policy.

Document Security fornisce inoltre a client, visualizzatori e indicizzatori la protezione dei documenti, la visualizzazione dei documenti protetti e l’indicizzazione dei documenti protetti. Per informazioni dettagliate sulla protezione dei documenti, consulta [informazioni sulla protezione dei documenti](/help/forms/using/admin-help/document-security.md).

## Topologia di distribuzione  {#deployment-topology}

La funzionalità di protezione dei documenti è disponibile solo in AEM Forms su JEE. È necessaria una singola istanza di AEM Forms su JEE. Se necessario, puoi anche creare un cluster o una farm di server AEM Forms. La topologia seguente è indicativa per l’esecuzione della funzionalità di protezione dei documenti. Per informazioni dettagliate sulla topologia, vedere [Architettura e topologie di distribuzione per AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![Topologia del server di protezione dei documenti](do-not-localize/document-security-server_topology.png)

Il diagramma seguente mostra l’architettura tipica di AEM Forms Document Security:

![Ambiente tipico di Document Security](do-not-localize/document-security-typical-environment.png)

## Installazione di AEM Forms su JEE {#installing-aem-forms-on-jee}

Per installare e configurare AEM Forms su JEE, effettua le seguenti operazioni:

1. Scarica il programma di installazione di AEM 6.5 Forms su JEE dal [sito Web Adobe Licensing (LWS)](https://licensing.adobe.com/). Per scaricare il programma di installazione è necessario un contratto valido di manutenzione e supporto.
1. Leggi il documento [AEM Forms sulle piattaforme supportate da JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) e assicurati che il software, l&#39;hardware, i sistemi operativi, il server applicazioni, i database, i JDK e l&#39;altra infrastruttura siano pronti per installare AEM Forms su JEE.
1. (Solo installazioni non chiavi in mano) Leggi [Preparazione all&#39;installazione di AEM Forms single server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_it) o [Preparazione all&#39;installazione del cluster di server AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64_it) e prepara l&#39;ambiente per installare e configurare AEM Forms su JEE.
1. A seconda dell&#39;ambiente e del server applicazioni in uso, scegliere uno dei seguenti documenti e seguire le istruzioni per completare l&#39;installazione

   * [Installazione e distribuzione di AEM Forms in JEE con JBoss turnkey](https://www.adobe.com/go/learn_aemforms_installTurnkey_64_it)
   * [Installazione e distribuzione di AEM Forms in JEE per JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64_it)
   * [Installazione e distribuzione di AEM Forms in JEE per WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64_it)
   * [Installazione e distribuzione di AEM Forms in JEE per WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64_it)
   * [Configurazione di AEM Forms su JEE nel cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64_it)
   * [Configurazione di AEM Forms su JEE nel cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64_it)
   * [Configurazione di AEM Forms su JEE nel cluster WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64_it)

   >[!NOTE]
   >
   >Nella schermata di selezione del modulo di AEM Forms su JEE configuration manager, seleziona l’opzione Document Security. L’opzione Document Security non richiede la selezione di alcun altro modulo.

## Passaggi successivi {#next-steps}

* [Configurare le opzioni client e server](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Creare e gestire le policy](/help/forms/using/admin-help/creating-policies.md)
* [Creare e gestire set di criteri](/help/forms/using/admin-help/creating-policy-sets.md)
