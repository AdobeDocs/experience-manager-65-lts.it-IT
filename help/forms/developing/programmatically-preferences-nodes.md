---
title: Gestione programmatica di PreferencesNodes
description: Utilizza l’API del servizio Preferences Manager (Java) per gestire in modo programmatico i nodi delle preferenze.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 95a83858-c0b7-4c68-b4a9-d525bfc663c0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Gestione programmatica dei nodi delle preferenze {#programmatically-managing-the-preferencesnodes}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

In questo argomento viene descritto come utilizzare l&#39;API del servizio Preferences Manager (Java) per gestire in modo programmatico i nodi Preferences.

Puoi modificare manualmente le impostazioni di configurazione dall’interfaccia utente di Amministrazione. Per modificare le opzioni, passare a `Home>Settings>User Management> Configuration>Manual Configuration`. Importa `config.xml` dopo aver apportato le modifiche. Tutte le modifiche ad eccezione di quelle apportate al nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist` andranno perse. L&#39;anteprima di Importazione ed esportazione gestione utenti non supporta la modifica delle impostazioni di configurazione per altri componenti. Ora è possibile apportare queste modifiche utilizzando le API `PreferencesManagerServiceClient`.

**Riepilogo dei passaggi** Per gestire in modo programmatico i nodi delle preferenze, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PreferencesManagerService
1. Richiama le operazioni di ruolo o autorizzazione appropriate

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client PreferencesManagerService**

Prima di poter eseguire a livello di programmazione un&#39;operazione PreferencesManagerService di User Management, è necessario creare un client PreferencesManagerService. Con l’API Java questo viene effettuato creando un oggetto PreferencesManagerServiceClient.

**Richiama il ruolo o le operazioni di autorizzazione appropriate**

Dopo aver creato il client del servizio, è possibile richiamare le operazioni di Gestione preferenze. Il client del servizio consente di leggere e impostare le autorizzazioni.
