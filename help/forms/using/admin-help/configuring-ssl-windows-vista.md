---
title: Configurazione SSL in Windows Vista
description: Scopri come configurare SSL in Windows Vista. Utilizza ed esegui Keytool di Java per generare il certificato SSL con le chiavi RSA per l’autenticazione.
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
exl-id: ee73f6a1-712c-461f-95e8-85f8c5694293
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 100%

---

# Configurazione SSL in Windows Vista {#configuring-ssl-on-windows-vista}

Per configurare SSL in Windows Vista™, hai bisogno di un certificato SSL con chiavi RSA per l’autenticazione. Per generare il certificato puoi utilizzare Keytool di Java.

>[!NOTE]
>
>Windows Vista non funzionerà con le chiavi DSA.

Puoi eseguire keytool utilizzando un singolo comando che include tutte le informazioni necessarie per generare il certificato e il keystore.

**Generare un certificato SSL**

1. Al prompt dei comandi passa a *`[JAVA HOME]`*/bin e digita il comando seguente per generare il certificato e il keystore:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome società* `,L=`*Nome città* `, S=`*Stato* `, C=`*Codice paese* `" -alias`*“Certificato LC”* `-keypass` `key`*_* *password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all’ambiente.*

1. Digitare `changeit` come password. Questa password è l’impostazione predefinita per un’installazione Java e l’amministratore di sistema potrebbe averla modificata.
