---
title: Integrazione con Adobe Analytics
description: Scopri come integrare Adobe Experience Manager (AEM) con Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 4f7e1794-af5a-45a2-8dc6-80029c47caeb
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 53%

---

# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione di Adobe Analytics e AEM consente di monitorare l’attività della pagina web:

* Una configurazione Adobe Analytics consente a AEM l’autenticazione con Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics.

I dati includono dati della pagina e dell’utente; ad esempio:

* dati raccolti dai componenti AEM
* clic sui collegamenti
* informazioni sull&#39;utilizzo dei video
* il numero di visite alla pagina da Adobe Analytics

Le pagine seguenti sono utili per configurare l’integrazione:

* [Connessione ad Adobe Analytics e creazione di framework](/help/sites-administering/adobeanalytics-connect.md)
* [Configurazione del tracciamento dei collegamenti per Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configurazione del tracciamento video per Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificazioni Adobe](/help/sites-administering/adobeanalytics-classifications.md)

È inoltre possibile utilizzare la procedura guidata [Opt-in](/help/sites-administering/opt-in.md) per eseguire facilmente l&#39;integrazione.

>[!NOTE]
>
>Consulta anche l&#39;articolo tutorial: [Integrazione di AEM con Adobe Target e Adobe Analytics utilizzando DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione dell&#39;integrazione Adobe Analytics](/help/sites-developing/extending-analytics.md) per informazioni sullo sviluppo di componenti che raccolgono dati utente e sulla personalizzazione del framework Adobe Analytics.

>[!NOTE]
>
>Se utilizzi Adobe Analytics con una configurazione proxy personalizzata, devi [configurare due bundle OSGi](/help/sites-deploying/configuring-osgi.md) (ad esempio, con la console web), necessari per le configurazioni proxy **Apache HTTP Client**. Entrambi sono necessari, poiché alcune funzionalità di AEM utilizzano le API 3.x, mentre altre le API 4.x. Configurare:
>
>* **Client HTTP Day Commons 3.1** per configurare l’API 3.x;
>  &#x200B;>  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configurazione proxy dei componenti HTTP Apache** per configurare l’API 4.x;
>  &#x200B;>  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
