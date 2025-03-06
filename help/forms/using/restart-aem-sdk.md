---
title: Come riavviare AEM SDK?
description: Best practice per il riavvio di AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
solution: Experience Manager, Experience Manager Forms
exl-id: 68935045-89b1-4219-b111-88a4600200df
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
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
