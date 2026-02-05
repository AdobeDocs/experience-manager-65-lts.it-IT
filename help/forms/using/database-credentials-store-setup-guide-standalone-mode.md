---
title: Guida alla configurazione dell'archivio credenziali del database (modalità standalone)
description: Trova la configurazione dell’archivio credenziali del database per AEM Forms JEE su JBoss/Red Hat EAP in modalità autonoma.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: f093f39fb535209297940cff13a99c7631812152
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Guida alla configurazione dell&#39;archivio credenziali del database (modalità standalone)

## Panoramica

Questa guida descrive la **configurazione dell&#39;archivio credenziali del database** per AEM Forms JEE su JBoss/Red Hat EAP in **modalità autonoma**. Questa opzione è necessaria quando si esegue l&#39;installazione manuale.


**Questa guida tratta:**

- Creazione dell&#39;archivio credenziali del database (`cred-store.p12`)
- Aggiunta sicura degli alias delle password del database
- Configurazione di JBoss per l’utilizzo dell’archivio credenziali

**CRITICO:** Questi script operano IN **MODALITÀ SOLO OFFLINE**. È necessario arrestare JBoss prima di eseguire questi script. Gli script utilizzano la modalità `embed-server` che richiede l&#39;arresto del server.

**Nota:** questa è **not** una guida di installazione autonoma completa. Questo documento presuppone:

- JBoss è già installato
- I file di configurazione autonomi (`lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`) sono già configurati
- Il database è configurato e accessibile

Se sono necessarie istruzioni di installazione indipendenti complete, consultare la guida all&#39;installazione principale.

## Prerequisiti

Prima di eseguire questi script, assicurati:

1. **JBoss DEVE essere arrestato**
   - Questi script funzionano SOLO in **MODALITÀ OFFLINE**
   - Gli script utilizzano `embed-server` che richiede l&#39;arresto del server
   - Se JBoss è in esecuzione, gli script avranno esito negativo
   - Verifica se JBoss è in esecuzione:
      - Windows: controllare Gestione attività per il processo `java.exe`
      - Linux: `ps aux | grep jboss` o `ps aux | grep java`
   - Arresta JBoss se in esecuzione:
      - Premi `Ctrl+C` nel terminale in cui è in esecuzione JBoss
      - Oppure terminare il processo manualmente

2. **La password del database è pronta**

3. **Hai deciso una password sicura per l&#39;archivio credenziali**

4. **È noto il file di configurazione del database in uso:**
   - `lc_oracle.xml` (per database Oracle)
   - `lc_mysql.xml` (per il database MySQL)
   - `lc_mssql.xml` (per database Microsoft SQL Server)

## Passaggi di configurazione

### Passaggio 1: creazione dell&#39;archivio credenziali del database

Utilizza gli script forniti per creare l’archivio delle credenziali del database e aggiungere tutti gli alias password richiesti.

#### In Windows:

**Posizione script:** `create-elytron-cred-standalone.bat`

`batch cd path\to\script\location create-elytron-cred-standalone.bat`

**Lo script richiederà:**
1. **Percorso JBOSS_HOME** (ad esempio, `C:\Adobe\Adobe_Experience_Manager_Forms\jboss`)
2. **Nome file di configurazione** (ad esempio `lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`)
3. **Password archivio credenziali** (protegge il file registro chiavi - ricorda questa password)
4. **Password del database** (la password effettiva del database)

**Funzionamento dello script:**

- Crea archivio credenziali in: `JBOSS_HOME\standalone\configuration\cred-store.p12`
- Modifica temporaneamente il file di configurazione per abilitare la creazione dell&#39;archivio credenziali
- Aggiunge i seguenti alias con la password del database:
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- Ripristina lo stato originale del file di configurazione
- Verifica che tutti gli alias siano stati aggiunti correttamente

#### Su Linux:

**Posizione script:** `create-elytron-cred-standalone.sh`

`bash cd /path/to/script/location chmod +x create-elytron-cred-standalone.sh./create-elytron-cred-standalone.sh`

**Lo script richiederà:**

1. **Percorso JBOSS_HOME** (ad esempio, `/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`)
2. **Nome file di configurazione** (ad esempio `lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`)
3. **Password archivio credenziali** (protegge il file registro chiavi - ricorda questa password)
4. **Password del database** (la password effettiva del database)

**Funzionamento dello script:**

- Crea archivio credenziali in: `JBOSS_HOME/standalone/configuration/cred-store.p12`
- Modifica temporaneamente il file di configurazione per abilitare la creazione dell&#39;archivio credenziali
- Aggiunge i seguenti alias con la password del database:
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- Ripristina lo stato originale del file di configurazione
- Verifica che tutti gli alias siano stati aggiunti correttamente

**Output previsto:**

```
=== JBoss Elytron Credential Store Setup ===
Enter JBOSS_HOME path (e.g. /opt/jboss): /opt/Adobe/Adobe_Experience_Manager_Forms/jboss
Enter configuration file name (e.g. lc_oracle.xml): lc_oracle.xml
Enter credential store password: ********
Confirm credential store password: ********
Enter database password: ********
Creating credential store using JBoss CLI...
Adding aliases to credential store...
Verifying credential store aliases...

All 4 aliases verified successfully!
- EncryptDBPassword
- EncryptDBPassword_IDP_DS
- EncryptDBPassword_EDC_DS
- EncryptDBPassword_AEM_DS

Credential store setup completed successfully!
```

### Passaggio 2: aggiornare il file di configurazione autonomo

Dopo aver eseguito lo script, è necessario configurare JBoss per la lettura della password dell&#39;archivio credenziali all&#39;avvio.

#### In Windows:

**Percorso file:** `<JBOSS_HOME>\bin\standalone.conf.bat`

Esempio: `C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

Aggiungi o aggiorna la seguente riga:

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

Sostituisci `YourActualPassword123` con la **password dell&#39;archivio credenziali** utilizzata nel passaggio 1.

#### Su Linux:

**Percorso file:** `<JBOSS_HOME>/bin/standalone.conf`

Esempio: `/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

Aggiungi o aggiorna la seguente riga:

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

Sostituisci `YourActualPassword123` con la **password dell&#39;archivio credenziali** utilizzata nel passaggio 1.

### Passaggio 3: avviare JBoss

Dopo aver completato la configurazione dell’archivio credenziali, avvia JBoss con il file di configurazione appropriato.

**Nota:** per informazioni sui comandi e le procedure di avvio esatti per avviare JBoss in modalità standalone, fare riferimento alla **guida all&#39;installazione principale**. I comandi di avvio possono variare a seconda della configurazione e del tipo di database specifici (`lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`).

## Verifica

### Verifica registri server

**Posizione registro:**

- Windows: `<JBOSS_HOME>\standalone\log\server.log`
- Linux: `<JBOSS_HOME>/standalone/log/server.log`

**Ricerca dei messaggi di avvio riusciti:**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**Nessun errore relativo a:**

- Caricamento archivio credenziali
- Connessione al database
- Alias mancanti

## Risoluzione di problemi

### Problema 1: archivio credenziali non trovato

**Messaggio di errore:**

```
ERROR Unable to load credential store
```

**Soluzione:**

1. Verificare che esista il file dell&#39;archivio credenziali:
   - Windows: `dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. Se manca, rieseguire lo script di creazione dell&#39;archivio credenziali (passaggio 1)

### Problema 2: password archivio credenziali errata

**Messaggio di errore:**

```
ERROR Unable to load credential store - Invalid password
```

**Soluzione:**
Verificare che la password in `standalone.conf.bat` / `standalone.conf` (passaggio 2) corrisponda alla password utilizzata durante la creazione dell&#39;archivio credenziali (passaggio 1).

**Da correggere:**
Modifica `standalone.conf.bat` / `standalone.conf` e aggiorna la password:

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### Problema 3: connessione al database non riuscita

**Messaggio di errore:**

```
ERROR Failed to obtain connection
```

**Soluzione:**

1. Verificare che la password del database utilizzata nell&#39;archivio credenziali sia corretta
2. Verifica che la configurazione dell’origine dati faccia riferimento all’alias corretto
3. Verificare la connettività di rete al server di database

**Per ricreare l&#39;archivio credenziali:**

1. Interrompi JBoss
2. Elimina l&#39;archivio credenziali esistente:
   - Windows: `del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. Rieseguire lo script di creazione dell&#39;archivio credenziali con la password di database corretta

### Problema 4: Errore Dello Script Durante L’Esecuzione

**Messaggio di errore:**

```
ERROR: jboss-cli.bat is not found
```

**Soluzione:**
Verificare che il percorso JBOSS_HOME sia corretto e punti alla directory di installazione JBoss.

**Messaggio di errore:**

```
ERROR: Configuration file not found
```

**Soluzione:**

1. Verificare che il nome del file di configurazione sia corretto
2. Verificare che il file esista nella directory `JBOSS_HOME\standalone\configuration\`
3. Assicurarsi di utilizzare il file di configurazione specifico per il database corretto

## Riferimento rapido

### Archivio credenziali database (modalità standalone)

**Scopo:** Archiviare le password del database in modo sicuro

**Script:**

- Windows: `create-elytron-cred-standalone.bat`
- Linux: `create-elytron-cred-standalone.sh`

**Creazioni:**

- File: `standalone/configuration/cred-store.p12`
- Alias: `EncryptDBPassword`, `EncryptDBPassword_IDP_DS`, `EncryptDBPassword_EDC_DS`, `EncryptDBPassword_AEM_DS`

**Configurazione:**

- Variabile: `-DCS_PASS=password`
- File: `standalone.conf.bat` (Windows) o `standalone.conf` (Linux)

