---
title: Configurare le impostazioni di blocco dell’account
description: Utilizza l’opzione Abilita blocco account per bloccare gli account utente dopo un numero specifico di errori di autenticazione consecutivi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: e78860dc-9375-465c-b1fa-2a4827ca8dce
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 100%

---

# Configurare le impostazioni di blocco dell’account {#configure-account-locking-settings}


>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Quando aggiungi un dominio, specifica se abilitare il blocco dell’account. Quando l’opzione Abilita blocco account è selezionata, gli account utente vengono bloccati dopo un numero specificato di errori di autenticazione consecutivi. Dopo un periodo di tempo specificato, l’utente può tentare di eseguire nuovamente l’autenticazione. Questa funzione impedisce agli utenti di provare diverse combinazioni di credenziali per accedere al sistema.

Utilizza le impostazioni nella pagina Gestione dominio per specificare il numero massimo di errori di autenticazione e il periodo di tempo di blocco degli account. Queste impostazioni si applicano a tutti i domini in cui è abilitato il blocco account.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Gestione dominio]**.
1. Nella casella Numero massimo di errori di autenticazione consecutivi immetti il numero massimo di tentativi di accesso non riusciti di un utente prima che l’account venga bloccato. Il valore predefinito è 20.
1. Nella casella Sblocca account dopo (minuti) immetti il numero di minuti di blocco dell’account utente. Dopo il numero di minuti specificato, l’utente può tentare di accedere di nuovo. Il valore predefinito è 30.
1. Fai clic su **[!UICONTROL Salva]**.
