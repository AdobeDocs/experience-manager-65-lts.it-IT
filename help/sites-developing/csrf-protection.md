---
title: Il framework di protezione CSRF
description: Il framework utilizza i token per garantire che la richiesta del cliente sia legittima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: d6bd4028-56c9-4e09-9bba-1199a41b41b8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Il framework di protezione CSRF{#the-csrf-protection-framework}

Oltre al filtro Apache Sling Referrer, Adobe fornisce anche un nuovo CSRF Protection Framework per la protezione contro questo tipo di attacchi.

Il framework utilizza i token per garantire che la richiesta del cliente sia legittima. I token vengono generati quando il modulo viene inviato al client e convalidati quando il modulo viene inviato nuovamente al server.

>[!NOTE]
>
>Le istanze di pubblicazione non contengono token per gli utenti anonimi.

## Requisiti {#requirements}

### Dipendenze {#dependencies}

Qualsiasi componente che si basa sulla dipendenza `granite.jquery` può beneficiare automaticamente del framework di protezione CSRF. In caso contrario, per qualsiasi componente è necessario dichiarare una dipendenza a `granite.csrf.standalone` prima di poter utilizzare il framework.

### Replica della chiave di crittografia {#replicating-crypto-keys}

Per utilizzare i token, devi replicare il file binario HMAC in tutte le istanze della distribuzione. Per ulteriori dettagli, vedere [Replica della chiave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key).

>[!NOTE]
>
>Assicurati anche di apportare le modifiche di configurazione Dispatcher necessarie per utilizzare il framework di protezione CSRF:
>
>* [Configurazione di Adobe Experience Manager Dispatcher per impedire attacchi CSRF](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/configuring/configuring-dispatcher-to-prevent-csrf)
>* [Panoramica di Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher)

>[!NOTE]
>
>Se utilizzi la cache del manifesto con l&#39;applicazione Web, assicurati di aggiungere &quot;**&ast;**&quot; al manifesto per assicurarti che il token non metta offline la chiamata di generazione del token CSRF. Per ulteriori informazioni, consulta questo [collegamento](https://www.w3.org/TR/offline-webapps/).
>
>Per ulteriori informazioni sugli attacchi CSRF e sui modi per mitigarli, consulta la [pagina OWASP Cross-Site Request Forgery](https://owasp.org/www-community/attacks/csrf).
