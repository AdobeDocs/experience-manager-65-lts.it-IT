---
title: Configurazione dell'autenticazione del nodo secondario (basata su Elytron)
description: JBoss EAP 8 utilizza Elytron per consentire la comunicazione e la registrazione sicure dei nodi secondari con il controller di dominio primario.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# Configurazione dell&#39;autenticazione del nodo secondario (basata su Elytron)

## Configurare L’Autenticazione Del Nodo Secondario Utilizzando Elytron

JBoss EAP 8 utilizza **Elytron** per autenticare le comunicazioni tra **nodi primari e secondari** in una distribuzione cluster. Questa configurazione garantisce la registrazione e la comunicazione sicure dei nodi secondari con il controller di dominio primario.

Sono disponibili due opzioni di configurazione a seconda dell’ambiente e dei requisiti di sicurezza.

## Prerequisiti

* È necessario creare un utente di gestione **denominato`secondary`** nel **nodo primario**.
* Eseguire questa configurazione **solo sui nodi secondari**.
* Ripetere la configurazione per **ogni nodo secondario** nel cluster.
* **JBoss deve essere completamente arrestato** sia sui nodi primari che secondari.
* Tutte le operazioni dell&#39;archivio credenziali devono essere eseguite in **modalità offline**.

Per arrestare JBoss se è in esecuzione:

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## Scegli un&#39;opzione di configurazione

* **Opzione 1: Impostazione Rapida Tramite L&#39;Archivio Delle Credenziali Predefinito**
Consigliato per ambienti e test di livello inferiore.

* **Opzione 2: Installazione archivio credenziali personalizzato**
Consigliato per ambienti di produzione e sicuri.

## Opzione 1: Impostazione rapida mediante l&#39;archivio credenziali predefinito

**Ideale per:** scenari di sviluppo, test e installazione rapida.

### Panoramica

* Un file dell&#39;archivio credenziali predefinito (`cs_secondary_hc.p12`) è preconfigurato.
* La password predefinita dell&#39;archivio credenziali è già impostata in `domain.conf`.
* È necessario aggiungere solo l&#39;alias della password di autenticazione.

### Passaggi di configurazione

#### Passaggio 1: verificare l&#39;archivio credenziali predefinito

Conferma l&#39;esistenza del file dell&#39;archivio credenziali predefinito:

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

Se il file non esiste, utilizzare **Opzione 2**.

#### Passaggio 2: aggiungere l’alias della password di autenticazione

Esegui il comando seguente da `<JBOSS_HOME>/bin`:

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> Il valore segreto deve corrispondere alla password utilizzata durante la creazione dell&#39;utente `secondary` sul nodo primario.

#### Passaggio 3: verificare la configurazione di domain.conf

Verifica che la seguente voce esista già (nessuna modifica richiesta):

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### Passaggio 4: avviare i nodi

1. Avviare il **nodo primario** e attenderne la completa inizializzazione.
2. Avvia il **nodo secondario**.

### Verifica

Controlla i registri:

* **Nodo primario**

  ```
  <JBOSS_HOME>/domain/log/host-controller.log
  ```

  ```
  Registered remote secondary host "secondary"
  ```

* **Nodo secondario**

  ```
  Connected to primary host controller
  ```

## Opzione 2: configurazione archivio credenziali personalizzate (produzione)

**Ideale per:** ambienti di produzione che richiedono una protezione avanzata.

### Passaggi di configurazione

#### Passaggio 1: rimuovere l&#39;archivio credenziali predefinito (se presente)

Se è presente l&#39;archivio credenziali predefinito, rinominarlo:

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### Passaggio 2: creare un archivio credenziali personalizzato

Da `<JBOSS_HOME>/bin`:

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### Passaggio 3: aggiungere l’alias della password di autenticazione

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### Passaggio 4: aggiornare domain.conf

Aggiorna il riferimento della password dell&#39;archivio credenziali:

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### Passaggio 5: verificare la configurazione XML

Verificare che `host-secondary.xml` contenga l&#39;archivio credenziali configurato e le voci client di autenticazione.
Se è presente la configurazione predefinita, non sono necessarie modifiche.


#### Passaggio 6: avviare i nodi

1. Avvia il **nodo primario** e attendi il completamento dell&#39;avvio.
2. Avvia il **nodo secondario**.

### Verifica

Confermare la corretta registrazione utilizzando i registri del controller host su entrambi i nodi.

## Riepilogo

* **L&#39;opzione 1** fornisce una configurazione rapida utilizzando un archivio credenziali preconfigurato.
* **L&#39;opzione 2** consente una maggiore protezione utilizzando una password personalizzata per l&#39;archivio credenziali.
* La configurazione deve essere completata **solo sui nodi secondari**.
* La configurazione del nodo principale viene riutilizzata automaticamente nel dominio.

