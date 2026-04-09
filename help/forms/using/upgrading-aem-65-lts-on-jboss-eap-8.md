---
title: Aggiornamento di AEM 6.5 LTS su JBoss EAP 8 (Windows)
description: Questa guida fornisce istruzioni dettagliate per l’aggiornamento di un’installazione Adobe Experience Manager (AEM) 6.5 LTS esistente da JBoss EAP 7.4 a JBoss EAP 8 su Windows, utilizzando JDK 21.
source-git-commit: 835530039678bc16a6de87b8d580be91a2026f94
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 3%

---

# Aggiornamento di AEM 6.5 LTS su JBoss EAP 8 (Windows)

## Panoramica

Questa guida fornisce istruzioni dettagliate per l’aggiornamento di un’installazione Adobe Experience Manager (AEM) 6.5 LTS esistente da JBoss EAP 7.4 a JBoss EAP 8 su Windows, utilizzando JDK 21.

**Percorso di aggiornamento:** JBoss EAP 7.4 (JDK 11) → JBoss EAP 8 (JDK 21)

## Avvisi importanti

>[!NOTE]
>
>Si tratta di una procedura di aggiornamento critica. Esegui sempre prima questo aggiornamento in un ambiente non di produzione e mantieni backup completi.
>
> PREREQUISITI **:** prima di procedere, è necessario completare il backup del sistema e un piano di rollback documentato.

## Requisiti pre-aggiornamento

### Requisiti di sistema

| Componente | Requisito |
|-----------|-------------|
| Sistema operativo | Windows Server 2016 o versione successiva (64 bit) |
| Ambiente Source | JBoss EAP 7.4 con AEM 6.5 LTS |
| Ambiente di destinazione | JBoss EAP 8.x |
| Java Development Kit | JDK 21 (Oracle o OpenJDK) |
| Versione di AEM | AEM 6.5 Service Pack (più recente consigliato) |
| Spazio su disco | Almeno 50 GB di spazio disponibile per il processo di aggiornamento |

### Download richiesti

Prima di iniziare l’aggiornamento, ottieni quanto segue:

1. Distribuzione **JBoss EAP 8.0**\
   Scarica da: [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. **Programma di installazione di JDK 21**\
   Scarica Oracle JDK 21 o OpenJDK 21 per Windows (64 bit)

3. **File WAR di AEM 6.5 LTS**\
   Ottieni la versione più recente di AEM 6.5 Service Pack WAR da Adobe Software Distribution

## Passaggio 1: creare un backup completo

>[!IMPORTANT]
>
> Eseguire backup completi prima di procedere.

### Elenco di controllo per il backup

- [ ] Backup completo della directory di installazione di JBoss EAP 7.4 esistente
- [ ] backup della cartella `crx-repository`
- [ ] backup della cartella `crx-quickstart`
- [ ] esportazione di tutte le configurazioni personalizzate
- [ Backup del database ] (se si utilizza un database esterno)
- [ ] Documenta lo stato e le configurazioni correnti del sistema

### Crea backup

```cmd
# Example backup location
C:\AEM-Backups\Pre-Upgrade-<date>

# Copy entire JBoss 7.4 directory
xcopy "C:\jboss-eap-7.4" "C:\AEM-Backups\Pre-Upgrade-<date>\jboss-eap-7.4" /E /I /H
```

**Operazione consigliata:** archiviare i backup in un&#39;unità o in un percorso di rete separato.

## Passaggio 2: installare JBoss EAP 8

### Estrai JBoss EAP 8

1. Estrai la distribuzione ZIP JBoss EAP 8 nella directory di installazione di destinazione:

   ```
   C:\jboss-eap-8.0
   ```

2. Prendere nota del percorso di questa directory come `<JBOSS_HOME>` da utilizzare in questa guida.

### Replica struttura directory

Assicurati che la nuova installazione di JBoss EAP 8 abbia la stessa struttura di directory personalizzata della precedente configurazione di JBoss EAP 7.4, in particolare:

- Directory di distribuzione personalizzate
- Cartelle di configurazione esterne
- Posizioni dei file di registro
- Qualsiasi modulo o libreria personalizzata

## Passaggio 3: eseguire la migrazione dei dati dell’archivio

### Copia archivio CRX

1. Passa all’installazione di JBoss EAP 7.4 esistente:

   ```
   <OLD_JBOSS_HOME>\bin\crx-repository
   ```

2. Copia l&#39;intera cartella `crx-repository` nella nuova installazione di JBoss EAP 8:

   ```cmd
   xcopy "C:\jboss-eap-7.4\bin\crx-repository" "C:\jboss-eap-8.0\bin\crx-repository" /E /I /H
   ```

**Importante:** questa cartella contiene l&#39;archivio dei contenuti e deve essere trasferita completamente.

### Verifica la copia dell’archivio

Dopo aver copiato, verifica che le dimensioni e la struttura dell’archivio corrispondano all’origine:

```cmd
dir "C:\jboss-eap-8.0\bin\crx-repository" /s
```

## Passaggio 4: arrestare l’istanza di AEM

Prima di apportare qualsiasi modifica, accertati che AEM sia completamente arrestato.

### Interrompi tramite Servizi Windows

1. Apri **Servizi** (Esecuzione: `services.msc`)
2. Individuare il servizio AEM/JBoss
3. Fare clic con il pulsante destro del mouse e selezionare **Interrompi**
4. Attendere il completamento dell&#39;arresto del servizio

### Arresta tramite riga di comando

Se AEM è stato avviato manualmente:

1. Passa alla finestra della console JBoss
2. Premi `Ctrl+C`
3. Attendere il completamento dell&#39;arresto normale

### Verifica arresto

Verificare che il processo Java non sia più in esecuzione:

```cmd
tasklist | findstr java
```

## Passaggio 5: Pulizia dei file legacy di AEM

Rimuovere i file obsoleti dalla directory `crx-quickstart` per garantire un aggiornamento corretto.

>[!CAUTION]
>
> Elimina solo i file e le cartelle specifici elencati di seguito. Non rimuovere altri file di configurazione, codice personalizzato o dati del repository.

### 5.1 Rimuovi cartella di avvio Launchpad

**Posizione:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\startup
```

**Azione:**

```cmd
rd /s /q "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\startup"
```

**Scopo:** questa cartella contiene i vecchi bundle OSGi che verranno rigenerati durante l&#39;aggiornamento.

### 5.2 Rimuovi file JAR di base

**Posizione:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar
```

**Azione:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar"
```

**Scopo:** questo file JAR verrà sostituito con la versione del nuovo file WAR.

### 5.3 Rimuovi file di comando di Bootstrap

**Posizione:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt
```

**Azione:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt"
```

**Scopo:** i comandi Bootstrap verranno rigenerati per il nuovo ambiente.

### 5.4 Rimuovi il file sling.options

**Posizione:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file
```

**Azione:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file"
```

### 5.5 Rimuovi il file sling_bootstrap.txt

**Posizione:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt
```

**Azione:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt"
```

### 5.6 Backup e rimozione del file sling.properties

Questo file contiene configurazioni specifiche dell’ambiente che potrebbero dover essere unite in un secondo momento.

**Posizione:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
```

**Azione:**

1. **Crea backup:**

   ```cmd
   copy "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties" "C:\AEM-Backups\sling.properties.backup"
   ```

2. **Elimina originale:**

   ```cmd
   del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties"
   ```

**Scopo:** Verrà generato un nuovo `sling.properties`. Rivedi il backup per ripristinare eventuali configurazioni personalizzate dopo l’aggiornamento.

## Passaggio 6: installare e configurare JDK 21

### Installare JDK 21

1. Eseguire il programma di installazione di JDK 21 per Windows
2. Eseguire l&#39;installazione in un percorso standard (ad esempio, `C:\Program Files\Java\jdk-21`)
3. Completare l&#39;installazione guidata

### Configurare le variabili di ambiente

#### Imposta JAVA_HOME

1. Apri **Proprietà sistema** → **Avanzate** → **Variabili ambiente**
2. In **Variabili di sistema**, fare clic su **Nuovo**
3. Imposta:
   - Nome variabile: `JAVA_HOME`
   - Valore variabile: `C:\Program Files\Java\jdk-21`
4. Fai clic su **OK**

#### Aggiorna variabile PERCORSO

1. In **Variabili di sistema**, selezionare `Path` e fare clic su **Modifica**
2. Aggiungi nuova voce:

   ```
   %JAVA_HOME%\bin
   ```

3. Sposta questa voce all’inizio dell’elenco per assicurarsi che JDK 21 abbia la precedenza
4. Fai clic su **OK** in tutte le finestre di dialogo

### Verifica installazione Java

1. Apri un prompt dei comandi **new** (per caricare le variabili di ambiente aggiornate)
2. Verifica versione Java:

   ```cmd
   java -version
   ```

   Output previsto:

   ```
   java version "21.0.x"
   Java(TM) SE Runtime Environment (build 21.0.x+...)
   Java HotSpot(TM) 64-Bit Server VM (build 21.0.x+..., mixed mode, sharing)
   ```

3. Verifica JAVA_HOME:

   ```cmd
   echo %JAVA_HOME%
   ```

## Passaggio 7: configurare le impostazioni JVM

Prima di distribuire AEM, configura le impostazioni di memoria JVM appropriate per l’utilizzo in produzione.

### Modifica standalone.conf.bat

1. Accedi a:

   ```
   <JBOSS_HOME>\bin
   ```

2. Apri `standalone.conf.bat` in un editor di testo (come amministratore)

3. Individuare o aggiungere la configurazione `JAVA_OPTS`:

   ```batch
   rem # AEM Production JVM Settings
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=768m"
   set "JAVA_OPTS=%JAVA_OPTS% -Djava.net.preferIPv4Stack=true"
   set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"
   set "JAVA_OPTS=%JAVA_OPTS% -server"
   ```

4. Salva e chiudi il file

**Impostazioni consigliate:**

| Parametro | Valore consigliato | Descrizione |
|-----------|-------------------|-------------|
| `-Xms` | 4096 m - 8192 m | Dimensione heap iniziale |
| `-Xmx` | 4096 m - 8192 m | Dimensione heap massima |
| `-XX:MaxMetaspaceSize` | 768 m - 1024 m | Limite spazio metaspace |

**Nota:** regola i valori in base ai requisiti di memoria e carico di lavoro disponibili del server.

## Passaggio 8: distribuire AEM 6.5 LTS WAR

### Prepara file WAR

Verifica che il file WAR di AEM sia configurato correttamente come indicato nella guida alla distribuzione:

- `jboss-deployment-structure.xml` è presente
- `web.xml` include impostazioni di configurazione multipart
- WAR viene reimballato se sono state apportate modifiche

### Implementare in JBoss

1. Copiare il file WAR di AEM 6.5 LTS nella directory di distribuzione:

   ```cmd
   copy "C:\AEM-Downloads\cq-quickstart-6.5.xx.war" "C:\jboss-eap-8.0\standalone\deployments\cq-quickstart.war"
   ```

**Importante:** assicurarsi che il nome file WAR corrisponda al percorso di contesto URL desiderato.

## Passaggio 9: avviare JBoss EAP 8 con AEM

### Avvia il server

1. Apri **Prompt dei comandi** come **Amministratore**

2. Passa alla directory bin JBoss:

   ```cmd
   cd C:\jboss-eap-8.0\bin
   ```

3. Avvia JBoss EAP 8:

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

### Monitora avvio iniziale

Osserva l’output della console per:

1. **Distribuzione WAR:**

   ```
   Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
   ```

2. **Messaggi di inizializzazione AEM:**

   ```
   Apache Sling Application Launcher
   Sling Home: crx-repository/crx-quickstart
   ```

3. **Aggiornamento archivio (se applicabile):**

   ```
   Performing repository migration...
   ```

**Tempo di avvio previsto:** 5-15 minuti a seconda delle dimensioni dell&#39;archivio e delle risorse di sistema.

## Passaggio 10: verificare il completamento dell&#39;aggiornamento

### Controlla avvio AEM

Monitora la console JBoss per il messaggio di avvio finale:

```
**** AEM started successfully ****
```

### Accedere all’interfaccia di AEM

1. Aprire un browser Web
2. Accedi a:

   ```
   http://localhost:8080/cq-quickstart
   ```

3. Accedi con le credenziali di amministratore:
   - Nome utente: `admin`
   - Password: `admin` (o password personalizzata)

### Verifica informazioni di sistema

1. Passa a **Strumenti** → **Operazioni** → **Console Web**

   ```
   http://localhost:8080/cq-quickstart/system/console
   ```

2. Fai clic su **Informazioni di sistema**

3. Verifica:

   - **Versione JVM:** deve mostrare Java 21
   - **JBoss versione:** deve mostrare EAP 8.x
   - **AEM versione:** deve mostrare 6.5.xx

### Verifica stato del sistema

Passa a **Strumenti** → **Operazioni** → **Diagnosi** per eseguire i controlli di integrità:

- Stato bundle: tutti i bundle devono essere &quot;Attivi&quot;
- Risoluzione risorsa: deve mostrare lo stato integro
- Prestazioni query: verifica eventuali degradi

## Attività post-aggiornamento

### Ripristina configurazioni personalizzate

1. Esaminare il file `sling.properties` di cui è stato eseguito il backup
2. Ripristina le modalità o configurazioni di esecuzione personalizzate nel nuovo file:

   ```
   <JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
   ```

3. Riavvia AEM in caso di modifica delle configurazioni

### Aggiorna agenti di replica

1. Passa a **Strumenti** → **Distribuzione** → **Replica** → **Agenti nell&#39;istanza di authoring**
2. Rivedi e verifica tutti gli agenti di replica
3. Aggiornare eventuali riferimenti hardcoded ai percorsi server precedenti

### Verifica funzionalità critica

- [ ] authoring e pubblicazione dei contenuti
- [ Caricamento ed elaborazione di ] risorse
- [ Esecuzione flusso di lavoro ]
- [ Autenticazione utente ]
- [ ] endpoint di integrazione
- [ ] modelli e componenti personalizzati

### Ottimizzazione delle prestazioni

1. Revisiona e cancella tutte le cache temporanee
2. Monitorare le prestazioni del sistema durante l&#39;utilizzo iniziale
3. Se necessario, regola le impostazioni JVM in base ai pattern di utilizzo effettivi

## Risoluzione dei problemi

### Problemi comuni

| Problema | Causa possibile | Soluzione |
|-------|---------------|----------|
| Avvio di AEM non riuscito | Versione Java errata | Verifica `JAVA_HOME` punti a JDK 21 |
| Errori di danneggiamento dell’archivio | Copia archivio incompleta | Ripristina dal repository di backup e copia |
| OutOfMemoryError | Memoria heap insufficiente | Aumenta `-Xmx` in `standalone.conf.bat` |
| Bundle in stato &quot;Installato&quot; | Dipendenze mancanti | Controllare le dipendenze del bundle nella console web |
| Porta 8080 già in uso | Un altro servizio che utilizza la porta | Arrestare il servizio in conflitto o modificare la porta JBoss |

### Posizioni dei file di registro

- **Registro server JBoss:**\
  `<JBOSS_HOME>\standalone\log\server.log`

- **Registro errori AEM:**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\error.log`

- **Registro di accesso AEM:**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\access.log`

### Procedura di ripristino

Se l’aggiornamento non riesce e non può essere risolto:

1. Interrompi EAP JBoss 8
2. Ripristina il backup completo di JBoss EAP 7.4
3. Ripristina la cartella `crx-repository`
4. Verifica `JAVA_HOME` punti a JDK 11 (se si esegue il rollback)
5. Avvia l’ambiente precedente

## Best practice

### Prima dell’implementazione in produzione

- [ ] Verificare l&#39;intero processo di aggiornamento in un ambiente di sviluppo
- [ ] Test in un ambiente di staging con dati di tipo produzione
- [ ] Documenta tutte le configurazioni e le integrazioni personalizzate
- [ ] Crea un piano di rollback dettagliato
- [ ] Pianifica aggiornamento durante la finestra di manutenzione
- [ ] Notifica a tutte le parti interessate i tempi di inattività pianificati

### Dopo l&#39;aggiornamento

- [ ] Monitoraggio dei registri di sistema per 48-72 ore
- [ ] Eseguire test di carico per identificare i problemi di prestazioni
- [ ] Aggiornare la documentazione di sistema
- [ ] Formazione del team su eventuali differenze EAP 8 JBoss
- [ ] Archivia tutta la documentazione di aggiornamento e i backup

## Documentazione correlata

- [Guida alla migrazione di JBoss EAP 8](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0/html/migration_guide/)
- [Guida all&#39;aggiornamento di Adobe Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html?lang=it)
- [Installazione dei Service Pack di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=it)

## Informazioni documento

| Campo | Valore |
|-------|-------|
| Versione documento | 1.0 |
| Ultimo aggiornamento | Febbraio 2026 |
| Versione di AEM | 6.5 LTS |
| Piattaforma Source | JBoss EAP 7.4/JDK 11 |
| Piattaforma di Target | JBoss EAP 8.x/JDK 21 |
| Sistema operativo | Windows Server |

**Note legali:** Adobe, Adobe Experience Manager e AEM sono marchi registrati di Adobe Inc. JBoss e Red Hat sono marchi registrati di Red Hat, Inc.
