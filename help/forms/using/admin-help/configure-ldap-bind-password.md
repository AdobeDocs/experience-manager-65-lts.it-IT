---
title: Configurare la password di binding LDAP
description: Scopri come configurare il campo bind password (password di associazione) prima di importare il file di configurazione in un altro sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 33e0f81f-7867-4c59-a9e5-75bf5182a27c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Configurare la password di binding LDAP{#configure-the-ldap-bind-password}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Per evitare rischi di sicurezza, il campo bind password (password di associazione) nel file di configurazione esportato (config.xml) non è configurato. Prima di importare il file di configurazione in un altro sistema, verificare di aver configurato la password. Questa password sostituisce una password esistente memorizzata nel database. Una password Null non sostituisce un valore esistente per una password non Null.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l&#39;impostazione di configurazione corrente in un file, fare clic su Esporta e salvare il file di configurazione in un&#39;altra posizione.
1. Nel file, individua il nodo `Domains` > *[Nome di dominio]* > `DirectoryConfigs` > `LDAPGroupConfig`. Ecco un esempio:

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Digitare un valore per `bindpassword` e salvare le modifiche.

1. Nel file, individuare il nodo `Domains` > *[Nome dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. Ecco un esempio:

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Digitare un valore per `bindpassword` e salvare le modifiche.

1. Per importare il file aggiornato, in Gestione utenti, fare clic su Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Sfoglia per trovare il file, su Importa e quindi su OK.
