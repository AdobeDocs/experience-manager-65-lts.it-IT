---
title: Panoramica sulla configurazione di SSL
description: Scopri come migliorare la sicurezza delle comunicazioni configurando SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2e81b9b9-321d-4423-9748-6385956b1d90
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Panoramica sulla configurazione di SSL {#overview-of-configuring-ssl}

È possibile creare credenziali SSL (Secure Sockets Layer) e configurare SSL sul server applicazioni per migliorare la sicurezza delle comunicazioni con il server applicazioni.

In qualità di prodotto per la sicurezza, Rights Management richiede la configurazione di SSL. Durante la configurazione dei certificati SSL, accertati di utilizzare solo le chiavi RSA. I certificati SSL con chiavi DSA non sono supportati.

Le informazioni fornite si applicano alle installazioni chiavi in mano, automatiche e manuali. Offre un esempio di metodo per configurare SSL. È inoltre possibile utilizzare altri metodi più appropriati per la rete o l&#39;organizzazione.

>[!NOTE]
>
>Prima di configurare SSL sul server applicazioni, è consigliabile completare l&#39;installazione, la configurazione e la distribuzione dei moduli di AEM Form e verificare che i prodotti siano in esecuzione correttamente.

>[!NOTE]
>
>Quando si creano certificati e credenziali di protezione SSL, utilizzare gli stessi privilegi dell&#39;account utente utilizzati per eseguire il server applicazioni. Se il server applicazioni viene eseguito utilizzando altri privilegi utente, è possibile che il modulo non venga eseguito correttamente per le rappresentazioni di PDForm quando ContentRootURI punta a https.

Se si dispone di un server LDAP abilitato per SSL, configurare User Management per utilizzarlo. (Vedere [Configurare la gestione degli utenti per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
