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
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 100%

---

# Panoramica sulla configurazione di SSL {#overview-of-configuring-ssl}

Puoi creare credenziali SSL (Secure Sockets Layer) e configurare SSL sul server applicazioni per migliorare la sicurezza delle comunicazioni con il server applicazioni.

In qualità di prodotto per la sicurezza, Rights Management richiede la configurazione di SSL. Durante la configurazione dei certificati SSL, assicurati di utilizzare solo le chiavi RSA. I certificati SSL con chiavi DSA non sono supportati.

Le informazioni fornite si applicano alle installazioni preconfigurate, automatiche e manuali. Offre un esempio di metodo per configurare SSL. Puoi inoltre utilizzare altri metodi più appropriati per la rete o l’organizzazione.

>[!NOTE]
>
>Prima di configurare SSL sul server applicazioni, è consigliabile completare l’installazione, la configurazione e la distribuzione dei moduli di AEM Forms e verificare che i prodotti siano in esecuzione correttamente.

>[!NOTE]
>
>Quando crei certificati e credenziali di sicurezza SSL, utilizza gli stessi privilegi dell’account utente utilizzati per eseguire il server applicazioni. Se esegui server applicazioni utilizzando altri privilegi utente, è possibile che il modulo non venga eseguito correttamente per le rappresentazioni di PDForm quando ContentRootURI punta a https.

Se disponi di un server LDAP abilitato per SSL, configura la gestione utenti per utilizzarlo. Consulta [Configurare la gestione utenti per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).
