---
title: Trasmettere le credenziali utilizzando le intestazioni WS-security
description: Scopri come trasmettere le credenziali utilizzando le intestazioni di sicurezza WS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 558d9b27-8734-4da2-b498-5bb2361ac65b
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Passaggio delle credenziali tramite intestazioni WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Quando si richiama un servizio AEM Forms su JEE utilizzando i servizi web, è possibile utilizzare le intestazioni WS-Security per trasmettere le informazioni di autenticazione client richieste da AEM Forms su JEE. WS-Security definisce le estensioni SOAP per implementare l&#39;autenticazione client, la riservatezza dei messaggi e l&#39;integrità dei messaggi. Di conseguenza, puoi richiamare AEM Forms sui servizi JEE quando AEM Forms su JEE viene distribuito come server autonomo o in un ambiente cluster.

La modalità di trasmissione delle intestazioni WS-Security ad AEM Forms su JEE dipende dal fatto che si utilizzino classi Java generate da Axis o assembly client .NET che utilizzano lo stack nativo di SOAP di un servizio.

>[!NOTE]
>
>Come esempio di chiamata di un servizio tramite intestazioni WS-Security, in questo argomento viene crittografato un documento PDF con una password richiamando il servizio Crittografia.

Questo documento tratta i seguenti argomenti:

* Passaggio dell&#39;autenticazione client tramite classi Java generate da Axis

* Generazione dei file della libreria Axis necessari per richiamare il servizio Crittografia

* Richiamare il servizio Encryption utilizzando un&#39;intestazione WS-Security

* Passaggio dell&#39;autenticazione client tramite un assembly client .NET

* Richiamare il servizio Encryption utilizzando un&#39;intestazione WS-Security


## Requisiti {#requirements}

Per trarre il massimo da questo documento, è necessario avere una solida conoscenza del software AEM Forms su JEE.

>[!MORELIKETHIS]
>
>* [Passaggio delle credenziali tramite intestazioni WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
