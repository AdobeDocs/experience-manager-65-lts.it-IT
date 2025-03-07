---
title: File di registro
description: Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni, che possono essere aperti utilizzando qualsiasi editor di testo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# File di registro {#log-files}

Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni. In caso di problemi di distribuzione nel server applicazioni, è possibile utilizzare i file di registro per individuare il problema. È possibile aprire i file di registro utilizzando qualsiasi editor di testo.

(JBoss) I seguenti file di registro si trovano nella directory `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[aaaa-mm-gg]*
* server.log

(WebLogic) I file di registro del dominio si trovano nella directory `[appserverdomain]` e i file di registro del server si trovano nella directory `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) I seguenti file di log si trovano nella directory `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log
