---
title: Avviare e interrompere il server applicazioni WebSphere
description: Varie procedure richiedono l’interruzione o l’avvio dell’istanza di WebSphere in cui vuoi distribuire i prodotti AEM Forms. Questo documento descrive come avviare e arrestare il server applicazioni WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 20cd6efb-edcf-4c87-b0f5-bdec5a0f6280
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 95%

---

# Avviare e interrompere il server applicazioni WebSphere {#starting-and-stopping-websphere-application-server}

Varie procedure richiedono l’interruzione o l’avvio dell’istanza di WebSphere in cui vuoi distribuire i prodotti AEM Forms. Se non hai la certezza che il server applicazioni sia stato avviato, puoi innanzitutto visualizzare lo stato del server applicazioni WebSphere.

## Visualizzare lo stato del server applicazioni WebSphere {#view-the-status-of-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `serverStatus.bat`*nome_server*
   * (Linux, UNIX) ./ `serverStatus.sh`*nome_server*

## Avviare il server applicazioni WebSphere {#start-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `startServer.bat`*nome_server*
   * (Linux, UNIX) ./ `startServer.sh`*nome_server*

## Arrestare il server applicazioni WebSphere {#stop-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `stopServer.bat`*nome_server*
   * (Linux, UNIX) ./ `stopServer.sh`*nome_server*
