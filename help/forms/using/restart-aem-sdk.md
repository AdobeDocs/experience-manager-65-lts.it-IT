---
title: Come riavviare AEM SDK?
description: Best practice per il riavvio di AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
solution: Experience Manager, Experience Manager Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# Riavvio di AEM SDK

Se riavvii AEM SDK arrestando i processi Java™, potrebbero verificarsi incongruenze nell’ambiente di sviluppo AEM, come segue:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Riavvia-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Soluzione

Per riavviare AEM SDK, passare alla finestra dei comandi attiva e premere il comando `Ctrl + C` per riavviare SDK.

Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java™, può causare incongruenze nell’ambiente di sviluppo AEM.
