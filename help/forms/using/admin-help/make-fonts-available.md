---
title: Rendere disponibili i font
description: Verifica che i font utilizzati in un modulo siano disponibili per l’utilizzo nel server applicazioni J2EE che ospita AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2861bde5-b373-4ab2-9808-7d32ef1dc925
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 100%

---

# Rendere disponibili i font {#make-fonts-available}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Verifica che i font utilizzati in un modulo siano disponibili per l’utilizzo nel server applicazioni J2EE che ospita AEM Forms. Ad esempio, prendi in considerazione lo scenario seguente. Un designer di moduli aggiunge un font alla directory dei font utilizzata dal designer e crea un modulo che utilizza tale font in un computer a parte. Affinché il servizio di output utilizzi il font, inseriscilo nella directory dei font del cliente. Se non esiste una directory dei font del cliente, crea una directory nel server applicazioni J2EE che ospita AEM Forms.

Per ulteriori informazioni sulle impostazioni dei font, consulta [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Specificare il percorso della directory dei font del cliente**

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
1. Nella casella Posizione della directory dei font di sistema digita il percorso della directory dei font del cliente. Puoi aggiungere più directory, separate da un punto e virgola **;**
1. Fai clic su OK.
1. Riavvia il sistema in cui è installato AEM Forms.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font del cliente, assicurati di riavviare il sistema in cui è installato AEM Forms.
