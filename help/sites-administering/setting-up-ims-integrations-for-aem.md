---
title: Configurazione delle integrazioni IMS per AEM
description: Scopri come impostare le integrazioni IMS per AEM
feature: Security
role: Admin
exl-id: 05ba39fc-4b53-43c0-9a9f-7da3293b1ca2
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 68%

---

# Configurazione delle integrazioni IMS per AEM {#setting-up-ims-integrations-for-aem}


>[!NOTE]
>
>I clienti Adobe utilizzano [Adobe Developer Console](https://developer.adobe.com/console) per generare credenziali che consentono l&#39;accesso a varie API. È possibile scegliere tra vari tipi di credenziali, da server a server OAuth ad applicazione a pagina singola. Il tipo di credenziale Account di servizio (JWT) è ora obsoleto, in favore delle credenziali server-to-server OAuth.

Adobe Experience Manager (AEM) può essere integrato con molte altre soluzioni Adobe. Ad esempio, Adobe Target, Adobe Analytics e altre.

Le integrazioni utilizzano un’integrazione IMS, configurata con OAuth S2S.

* Dopo aver creato:

   * [Credenziali in Developer Console](#credentials-in-the-developer-console)

* Quindi puoi:

   * Creare una (nuova) [Configurazione OAuth](#creating-oauth-configuration)

   * [Migrare una configurazione JWT esistente a una configurazione OAuth](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>In precedenza, le configurazioni venivano effettuate con [Credenziali JWT che ora sono obsolete in Adobe Developer Console](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>Tali configurazioni non possono più essere create o aggiornate, ma è possibile eseguirne la migrazione alle configurazioni OAuth.

## Credenziali in Developer Console {#credentials-in-the-developer-console}

Come primo passaggio, devi configurare le credenziali OAuth in Adobe Developer Console.

Per informazioni dettagliate su come eseguire questa configurazione, consulta la documentazione di Developer Console, a seconda dei requisiti:

* Panoramica:

   * [Autenticazione da server a server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* Creazione di nuove credenziali OAuth:

   * [Guida all’implementazione delle credenziali da server a server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)

* Migrazione di una credenziale JWT esistente a una credenziale OAuth:

   * [Migrazione dalle credenziali dell’account di servizio (JWT) alle credenziali da server a server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)

Ad esempio:

![Credenziali OAuth in Developer Console](assets/ims-configuration-developer-console.png)

## Creazione di una configurazione OAuth {#creating-oauth-configuration}

Per creare una nuova integrazione Adobe IMS utilizzando OAuth:

1. In AEM, passa a **Strumenti**, **Sicurezza**, **Integrazione Adobe IMS**.

1. Seleziona **Crea**.

1. Completa la configurazione in base ai dettagli di [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation). Ad esempio:

   ![Crea configurazione OAuth](assets/ims-create-oauth-configuration.png)

1. **Salva** le modifiche.

## Migrazione di una configurazione JWT esistente a una configurazione OAuth {#migrating-existing-JWT-configuration-to-oauth}

Per migrare un’integrazione Adobe IMS esistente basata sulle credenziali JWT:

>[!NOTE]
>
>Questo esempio mostra una configurazione di lancio di IMS.

1. In AEM, passa a **Strumenti**, **Sicurezza**, **Integrazione Adobe IMS**.

1. Seleziona la configurazione JWT di cui eseguire la migrazione. Le configurazioni JWT sono contrassegnate dall’avvertenza **Credenziali JWT (obsolete)**.

1. Seleziona **Proprietà**.

   ![Seleziona una configurazione JWT](assets/ims-migrate-jwt-select-configuration.png)

1. La configurazione si apre in sola lettura:

   ![Proprietà di configurazione: sola lettura](assets/ims-migrate-jwt-properties-read-only.png)

1. Seleziona **OAuth** dall’elenco a discesa **Tipo di autenticazione**:

   ![Seleziona tipo di autenticazione](assets/ims-migrate-jwt-authentication-type.png)

1. Le proprietà disponibili vengono aggiornate. Utilizza i dettagli da Developer Console per completarli:

   ![Completa dettagli OAuth](assets/ims-migrate-jwt-complete-oauth-details.png)

1. Utilizza **Salva e chiudi** per mantenere gli aggiornamenti.
Quando si torna alla console, l&#39;avviso **Credenziali JWT (obsoleto)** non viene più visualizzato.
