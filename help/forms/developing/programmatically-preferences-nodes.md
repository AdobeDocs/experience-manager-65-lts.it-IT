---
title: Gestione programmatica di PreferencesNodes
description: Utilizza l’API del servizio Preferences Manager (Java) per gestire i nodi delle preferenze a livello di programmazione.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 95a83858-c0b7-4c68-b4a9-d525bfc663c0
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 2%
---
# Gestione a livello di programmazione dei nodi delle preferenze {#programmatically-managing-the-preferencesnodes}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms nell&#39;ambiente JEE.**

In questo argomento viene descritto come utilizzare l&#39;API del servizio Preferences Manager (Java) per gestire i nodi delle preferenze a livello di programmazione.

Puoi modificare manualmente le impostazioni di configurazione dall’interfaccia utente di Amministrazione. Per modificare le opzioni, passare a `Home>Settings>User Management> Configuration>Manual Configuration`. Importa `config.xml` dopo aver apportato le modifiche. Tutte le modifiche ad eccezione di quelle apportate al nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist` andranno perse. L&#39;anteprima di Importazione ed esportazione gestione utenti non supporta la modifica delle impostazioni di configurazione per altri componenti. Ora è possibile apportare queste modifiche utilizzando le API `PreferencesManagerServiceClient`.

**Riepilogo dei passaggi**
Per gestire i nodi delle preferenze a livello di programmazione, effettuare le seguenti operazioni:

1. Includi i file di progetto.
1. Crea un client `PreferencesManagerService`.
1. Richiama le operazioni di ruolo o autorizzazione appropriate.

**Includi i file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Crea un client `PreferencesManagerService`**

Prima di poter eseguire a livello di programmazione un&#39;operazione di gestione utenti `PreferencesManagerService`, è necessario creare un client `PreferencesManagerService`. Con l&#39;API Java, creare un oggetto `PreferencesManagerServiceClient`.

**Richiama il ruolo o le operazioni di autorizzazione appropriate**

Dopo aver creato il client del servizio, è possibile richiamare le operazioni di Gestione preferenze. Il client del servizio consente di leggere e impostare le autorizzazioni.
