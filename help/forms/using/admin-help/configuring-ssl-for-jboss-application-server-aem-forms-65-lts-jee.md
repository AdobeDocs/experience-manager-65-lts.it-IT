---
title: Configurazione di SSL per il server applicazioni JBoss (AEM 6.5 LTS JEE)
description: Scopri come configurare SSL per il server applicazioni JBoss.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
exl-id: 8a2fbfdc-2b6a-4c9d-beab-1908a9261003
source-git-commit: 96fe29ceae4c38238ccc40d456f2ad8e276788c7
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# Configurazione di SSL per il server applicazioni JBoss (AEM 6.5 LTS JEE)

## Panoramica

Per configurare SSL sul server applicazioni JBoss per Adobe Experience Manager (AEM) 6.5 LTS in esecuzione su Java EE, è necessario abilitare la comunicazione HTTPS protetta. L’abilitazione di SSL crittografa i dati scambiati tra i client e il server, rendendoli un requisito di sicurezza critico per qualsiasi implementazione di AEM Forms di produzione.

Il processo prevede due fasi principali:

- **Ottenimento di una credenziale SSL** mediante la generazione di un certificato autofirmato o la richiesta di un certificato a un&#39;autorità di certificazione (CA).
- **Abilitazione di SSL su JBoss** — utilizzando il sottosistema Elytron tramite comandi CLI JBoss.

In questa guida vengono utilizzati i seguenti valori segnaposto:

- `[appserver root]`: la home directory del server applicazioni JBoss che esegue AEM Forms.
- `[type]` — nome di cartella che varia a seconda del tipo di installazione eseguita.
- `[JAVA_HOME]`: la directory in cui è installato JDK.

## Parte 1: creare una credenziale SSL (autofirmato)

Se non si dispone di un certificato di una CA, è possibile generare una credenziale SSL autofirmata utilizzando l&#39;utilità Java `keytool`. Questa funzione è adatta per gli ambienti di sviluppo o test.

### Passaggio 1 — Generare il registro chiavi

Passare a `[JAVA_HOME]/bin` in un prompt dei comandi ed eseguire il comando seguente, sostituendo i valori con quelli appropriati per l&#39;ambiente. Il nome host deve essere il nome di dominio completo (FQDN) del server applicazioni:

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

Quando richiesto, immettere `keystore_password`. La password per il keystore e la chiave devono essere identiche.

### Passaggio 2 — Copia il registro chiavi nella directory di configurazione

Copia il keystore generato nella cartella di configurazione appropriata per il tipo di installazione:

```bash
# Windows Single Server
copy keystorename.keystore [appserver root]\standalone\configuration

# Windows Server Cluster
copy keystorename.keystore [appserver root]\domain\configuration

# Linux Single Server
cp keystorename.keystore [appserver root]/standalone/configuration

# Linux Server Cluster
cp keystorename.keystore [appserver root]/domain/configuration
```

### Passaggio 3 — Esportare il file del certificato

Esporta il certificato dal keystore utilizzando uno dei seguenti comandi:

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

Immetti `keystore_password` quando richiesto.

### Passaggio 4 — Copiare e verificare il certificato

Copiare `AEMForms_cert.cer` nella directory di configurazione, quindi verificarne il contenuto:

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### Passaggio 5: importare il certificato in Java Truststore

Prima di eseguire l&#39;importazione, verificare che il file `cacerts` sia scrivibile:

```bash
# Windows: Right-click cacerts → Properties → deselect Read-only

# Linux:
chmod 777 [JAVA_HOME]/jre/lib/security/cacerts
```

Importa quindi il certificato:

```bash
keytool -import -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [JAVA_HOME]/jre/lib/security/cacerts
```

Quando viene richiesta la password, digitare `changeit` (la password predefinita del truststore Java — verificare con l&#39;amministratore se è stata modificata). Quando viene chiesto a **Considerare attendibile il certificato? [no]**, tipo `yes`. Dovresti visualizzare un messaggio di conferma: *&quot;Il certificato è stato aggiunto al keystore.&quot;*

>[!NOTE]
>
> Se ti connetti a AEM Forms tramite SSL da Workbench, devi installare il certificato anche sul computer di Workbench.

## Parte 2: abilitare SSL su JBoss utilizzando il sottosistema Elytron

Con le credenziali SSL attive, ora è possibile abilitare HTTPS su JBoss utilizzando il sottosistema di sicurezza Elytron tramite l’interfaccia CLI di JBoss. Prima di procedere, verificare che il file keystore si trovi nella directory di configurazione appropriata.

>[!NOTE]
>
> In Windows, ogni comando CLI deve essere immesso come riga singola senza interruzioni di riga. Sostituisci `keystorename.keystore` con il tuo nome file effettivo e `changeit` con la tua password keystore/key.

### Passaggio 6a — Creare un registro chiavi di Elytron

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

Sostituisci `JKS` con `PKCS12` se il tuo keystore utilizza tale formato.

### Passaggio 6b — Creare il Key-Manager Elytron

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  credential-reference={clear-text="changeit"})
```

Se il keystore contiene più voci di certificato, specifica esplicitamente l’alias:

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  alias="AEMForms Cert",
  credential-reference={clear-text="changeit"})
```

### Passaggio 6c — Aggiornare il contesto SSL del server

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### Passaggio 6d — Configurare il listener HTTPS.

Collega il contesto SSL a Undertow (il server web JBoss) per abilitare il listener HTTPS:

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## Parte 3: Riavviare il server applicazioni

Dopo aver completato la configurazione di Elytron, riavvia JBoss per applicare le modifiche.

### Installazioni chiavi in mano (servizi Windows)

- Aprire **Pannello di controllo Campaign > Strumenti di amministrazione > Servizi**.
- Selezionare **JBoss per Adobe Experience Manager Form**.
- Selezionare **Azione > Arresta** e attendere l&#39;arresto del servizio.
- Seleziona **Azione > Avvia**.

### Installazioni JBoss preconfigurate o manuali

Dal prompt dei comandi passare a `[appserver root]/bin`:

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## Parte 4: Richiedi credenziali da un’autorità di certificazione

Per gli ambienti di produzione, è necessario utilizzare un certificato rilasciato da un’autorità di certificazione (CA) attendibile. Il processo comporta la generazione di una coppia di chiavi, la creazione di una richiesta di firma del certificato (CSR, Certificate Signing Request) e l’importazione del certificato firmato dalla CA.

### Generare il registro chiavi e creare una CSR

Passa a `[JAVA_HOME]/bin` e genera il keystore:

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

Quindi genera la CSR da inviare alla tua CA:

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

Invia il file `.csr` alla tua CA. Dopo aver ricevuto nuovamente il certificato firmato, segui la procedura indicata di seguito.

### Importa il certificato firmato dalla CA

Importa prima il certificato radice della CA:

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

Se il certificato radice non è già attendibile dal browser, importalo anche lì. Importa quindi il certificato firmato da una CA:

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> Il certificato firmato da una CA importato sostituirà qualsiasi certificato pubblico autofirmato esistente, se presente nel keystore.

Una volta importato il certificato CA, procedere con i **passaggi 6a-6d** nella parte 2 (configurazione Elytron), riavviare il server (parte 3) e verificare l&#39;accesso SSL.

## Verifica accesso SSL

Dopo aver riavviato il server, verifica che SSL funzioni correttamente accedendo alla console di amministrazione di AEM Forms tramite HTTPS. La porta SSL predefinita per JBoss è `8443`:

```
https://[host name]:8443/adminui
```

Se la console di amministrazione viene caricata correttamente su HTTPS, SSL è stato configurato correttamente. Utilizzare la porta `8443` per tutte le connessioni SSL successive ad AEM Forms.
