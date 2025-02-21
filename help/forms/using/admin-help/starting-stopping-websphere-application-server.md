---
title: Avvio e arresto dell'Application Server WebSphere
description: Diverse procedure richiedono l'arresto o l'avvio dell'istanza di WebSphere in cui si desidera distribuire i prodotti AEM Forms. Questo documento descrive come avviare e arrestare l'Application Server WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# Avvio e arresto dell&#39;Application Server WebSphere {#starting-and-stopping-websphere-application-server}

Diverse procedure richiedono l&#39;arresto o l&#39;avvio dell&#39;istanza di WebSphere in cui si desidera distribuire i prodotti AEM Forms. Se non si è certi che il server applicazioni sia stato avviato, è innanzitutto possibile visualizzare lo stato dell&#39;Application Server WebSphere.

## Visualizzare lo stato dell&#39;Application Server WebSphere {#view-the-status-of-websphere-application-server}

1. Dal prompt dei comandi passare alla directory `[appserver root]/bin`.
1. Immettere il comando seguente, sostituendo *nome_server* con il nome dell&#39;Application Server WebSphere:

   * (Windows) `serverStatus.bat`*nome_server*
   * (Linux, UNIX)./ `serverStatus.sh`*nome_server*

## Avvia Application Server WebSphere {#start-websphere-application-server}

1. Dal prompt dei comandi passare alla directory `[appserver root]/bin`.
1. Immettere il comando seguente, sostituendo *nome_server* con il nome dell&#39;Application Server WebSphere:

   * (Windows) `startServer.bat`*nome_server*
   * (Linux, UNIX)./ `startServer.sh`*nome_server*

## Arresta server applicazioni WebSphere {#stop-websphere-application-server}

1. Dal prompt dei comandi passare alla directory `[appserver root]/bin`.
1. Immettere il comando seguente, sostituendo *nome_server* con il nome dell&#39;Application Server WebSphere:

   * (Windows) `stopServer.bat`*nome_server*
   * (Linux, UNIX)./ `stopServer.sh`*nome_server*
