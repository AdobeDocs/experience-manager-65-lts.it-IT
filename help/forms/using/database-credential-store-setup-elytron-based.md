---
title: Configurazione archivio credenziali database (basato su Elytron)
description: JBoss EAP 8 supporta gli archivi di credenziali Elytron per la gestione sicura delle password del database in AEM Forms per la configurazione in modalità dominio.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: f093f39fb535209297940cff13a99c7631812152
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# Configurazione archivio credenziali database (basato su Elytron)

## Configurare l’archivio delle credenziali del database utilizzando Elytron

JBoss EAP 8 utilizza **archivi di credenziali Elytron** per gestire in modo sicuro le password del database per le distribuzioni AEM Forms. Adobe fornisce **script automatizzati** per semplificare la creazione e la configurazione dell&#39;archivio credenziali basato su Elytron in modalità dominio.


È necessario completare l&#39;installazione **prima di avviare il controller di dominio JBoss**.

### Prerequisiti

* Il server **JBoss deve essere completamente arrestato** prima di eseguire lo script di creazione dell&#39;archivio credenziali.
* La creazione dell&#39;archivio credenziali deve essere eseguita solo in **modalità offline**.

Per arrestare JBoss se è in esecuzione:

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### Scarica script

Scarica lo script appropriato in base al sistema operativo in uso:

| Nome script | Sistema operativo |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux/UNIX |

Per Linux, rendi eseguibile lo script:

```
chmod +x create-elytron-cred-domain.sh
```

### Passaggi di configurazione

#### Passaggio 1: Scaricare e inserire lo script

Scarica lo script appropriato e inseriscilo nella seguente directory:

```
<JBOSS_HOME>/bin
```

#### Passaggio 2: eseguire lo script

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux / UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### Passaggio 3: fornire le informazioni richieste

Durante l’esecuzione, lo script richiede i seguenti input:

1. **Percorso JBOSS_HOME**
Immetti il percorso completo della directory di installazione JBoss.

2. **Nome file di configurazione del database**
Immettere una delle seguenti opzioni in base al database:

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **Password archivio credenziali**
Immettere una password sicura per proteggere l&#39;archivio credenziali.

   > Questa password è nascosta durante l&#39;immissione e deve essere memorizzata per i passaggi successivi.

4. **Password database**
Immettere la password effettiva della connessione al database.

#### Passaggio 4: esecuzione e convalida degli script

Lo script esegue automaticamente le azioni seguenti:

* Crea `cred-store.p12` in:

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* Crea i seguenti alias di credenziali:

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* Verifica che tutti gli alias vengano aggiunti correttamente

L&#39;esecuzione è riuscita e conferma la creazione dell&#39;archivio credenziali e la verifica degli alias.

#### Passaggio 5: configurare le opzioni JVM

Aggiorna la configurazione di avvio del dominio JBoss per fornire la password dell’archivio credenziali.

* **Linux**
Modifica:

  ```
  <JBOSS_HOME>/bin/domain.conf
  ```

  Aggiungi:

  ```
  JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourCredStorePassword"
  ```

* **Windows**
Modifica:

  ```
  <JBOSS_HOME>/bin/domain.conf.bat
  ```

  Aggiungi:

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourCredStorePassword"
  ```

Sostituire `YourCredStorePassword` con la password immessa durante la creazione dell&#39;archivio credenziali.

I file di configurazione del dominio fanno riferimento a questo valore utilizzando la variabile `${CS_PASS}`.


#### Passaggio 6: verificare la configurazione del dominio

Aprire il file di configurazione del dominio del database:

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

Verificare che le origini dati facciano riferimento all&#39;archivio credenziali Elytron:

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

Ogni origine dati utilizza un alias specifico:

* **IDP_DS:** `EncryptDBPassword_IDP_DS`
* **DS_EDC:** `EncryptDBPassword_EDC_DS`
* **Servizi di dominio AEM:** `EncryptDBPassword_AEM_DS`
* **Servizi di dominio predefiniti / Servizi di dominio di esempio:** `EncryptDBPassword`

Tutti gli alias fanno riferimento alla stessa password del database memorizzata nell&#39;archivio credenziali.

>[!NOTE]
>
>* Configurare l&#39;archivio credenziali solo sul nodo primario.
>* I nodi secondari utilizzano automaticamente la configurazione del dominio sincronizzata dal nodo principale.
