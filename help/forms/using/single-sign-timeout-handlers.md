---
title: Gestori di accesso singolo e timeout
description: Come impostare il valore di timeout della sessione per l’area di lavoro di AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: c6bdfa6f-0d9b-4473-a2e1-6cad73fbd1ed
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Gestori di accesso singolo e timeout {#single-sign-on-and-timeout-handlers}

L’area di lavoro di AEM Forms è abilitata per l’SSO. Se un utente ha effettuato l’accesso a un’applicazione AEM Forms come Forms Manager o l’interfaccia utente di PDF Generator e accede all’area di lavoro di AEM Forms nella stessa sessione del browser, l’utente ha effettuato l’accesso all’area di lavoro di AEM Forms e viceversa.

## Gestione del timeout del server nell’area di lavoro di AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Il timeout della sessione di un utente può essere configurato nella console di amministrazione.

Per impostare il timeout, accedere a `https://'[server]:[port]'/adminui`, passare a **Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati** e impostare le impostazioni desiderate.

In AEM Forms il timeout nell’area di lavoro viene gestito come:

* La durata della sessione per un utente è disponibile in risposta alla chiamata `initialize` che inizializza la sessione utente.
* Una finestra di dialogo a comparsa notifica all&#39;utente che la sessione sta per scadere, 15 secondi prima della scadenza.

In questa finestra di dialogo a comparsa:

* Fare clic su OK per terminare la sessione utente.
* Fare clic su Annulla per reinizializzare la sessione utente.

>[!NOTE]
>
>Se non viene eseguita alcuna azione, l’utente viene automaticamente disconnesso dall’area di lavoro di AEM Forms tre secondi prima della scadenza della sessione.
