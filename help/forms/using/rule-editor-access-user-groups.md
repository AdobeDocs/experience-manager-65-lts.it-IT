---
title: Concedere l’accesso all’editor di regole a specifici gruppi di utenti
description: Concedi un accesso limitato all’editor di regole per selezionare i gruppi di utenti.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: a17cc96f-b0f0-48c7-9685-d065a6fc1514
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 4%

---

# Concedere l’accesso all’editor di regole a specifici gruppi di utenti{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

Potresti avere diversi tipi di utenti con diverse competenze che lavorano con Adaptive Forms. Anche se gli utenti esperti possono avere le giuste conoscenze per lavorare con script e regole complesse, ci possono essere utenti di livello base che devono lavorare solo con il layout e le proprietà di base dei moduli adattivi.

AEM Forms ti consente di limitare l’accesso all’editor di regole agli utenti in base al loro ruolo o funzione. Nelle impostazioni del servizio di configurazione di Forms adattivo è possibile specificare i [gruppi di utenti](/help/sites-administering/security.md) che possono visualizzare e accedere all&#39;editor di regole.

## Specificare i gruppi di utenti che possono accedere all’editor di regole {#specify-user-groups-that-can-access-rule-editor}

1. Accedi ad AEM Forms come amministratore.
1. Nell&#39;istanza di authoring, fare clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![hammer](assets/hammer.png) > Operazioni > Console Web. La console Web si apre in una nuova finestra.

   ![1-2](assets/1-2.png)

1. Nella finestra Console Web individuare e fare clic su **[!UICONTROL Modulo adattivo e configurazione canale Web comunicazione interattiva]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Configurazione modulo adattivo e canale web di comunicazione interattiva]**. Non modificare alcun valore e fai clic su **Salva**.

   Crea un file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config nell’archivio CRX.

1. Accedi a CRXDE come amministratore. Apri il file /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config per la modifica.
1. Utilizzare la proprietà seguente per specificare il nome di un gruppo che può accedere all&#39;editor di regole (ad esempio, RuleEditorsUserGroup) e fare clic su **Salva tutto**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Per abilitare l’accesso per più gruppi, specifica un elenco di valori separati da virgola:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crea utente](assets/create_user_new.png)

   Adesso, quando un utente che non fa parte del gruppo di utenti specificato (in questo caso RuleEditorsUserGroup) tocca un campo, l&#39;icona Modifica regola ( ![edit-rules1](assets/edit-rules1.png)) non è disponibile nella barra degli strumenti dei componenti:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra degli strumenti Componenti visibile a un utente con accesso all’editor di regole

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra degli strumenti Componenti visibile a un utente senza accesso all’editor di regole

   Per istruzioni sull&#39;aggiunta di utenti ai gruppi, vedere [Amministrazione utenti e sicurezza](/help/sites-administering/security.md).
