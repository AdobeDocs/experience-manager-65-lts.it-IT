---
title: Configurazione di una soluzione di gestione della corrispondenza
description: Scopri come configurare una soluzione di gestione della corrispondenza in un ambiente AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: da668935-9d16-49e1-8e7a-772fc4040c1d
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%
---
# Configurazione di una soluzione di gestione della corrispondenza {#configuring-a-correspondence-management-solution}

## Definizione dell’URL dell’istanza di authoring per VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Per definire l’URL di un’istanza di authoring per il ripristino della versione dell’istanza di authoring, effettua le seguenti operazioni:

1. Vai a *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Accedi con le credenziali utente di OSGi Management Console. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic sull&#39;icona **[!UICONTROL Modifica]** accanto all&#39;impostazione **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**.
1. Nel campo **[!UICONTROL URL autore VersionRestoreManager]** specificare l&#39;URL dell&#39;istanza di authoring di VersionRestoreManager.

   **Stringa URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se esistono più istanze di authoring (cluster) gestite da un load balancer, specificare l&#39;URL del load balancer nel campo **[!UICONTROL URL Author]** di VersionRestoreManager.

1. Fai clic su **[!UICONTROL Salva]**.

## Definizione dell’URL dell’istanza Publish per ActivationManagerImpl (public instance activation manager) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Segui questi passaggi per definire l’URL dell’istanza Publish per la gestione dell’attivazione di un’istanza pubblica:

1. Vai a *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Accedi con le credenziali utente di OSGi Management Console. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic sull&#39;icona **[!UICONTROL Modifica]** accanto all&#39;impostazione **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**.
1. Nel campo **[!UICONTROL URL pubblicazione di ActivationManager]**, specificare l&#39;URL per accedere all&#39;istanza di pubblicazione ActivationManager. Puoi fornire i seguenti URL.

   * **URL del load balancer (consigliato)**: fornire l&#39;URL del load balancer se un server Web funge da load balancer davanti alla farm di pubblicazione (più istanze di pubblicazione non cluster).
   * **URL istanza di pubblicazione**: fornire qualsiasi URL dell&#39;istanza di pubblicazione. Se si dispone di una singola istanza di pubblicazione o il server Web che esegue la farm di pubblicazione non è accessibile dall&#39;ambiente di authoring a causa di eventuali restrizioni. Se l’istanza Publish specificata non è disponibile, è disponibile un meccanismo di fallback da gestire dal lato dell’autore.
   * **Stringa URL**:

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Fai clic su **[!UICONTROL Salva]**.

Per ulteriori informazioni sulla configurazione di Gestione corrispondenza, vedere [Proprietà di configurazione di Gestione corrispondenza](https://helpx.adobe.com/it/aem-forms/6-2/cm-configuration-properties.html).
