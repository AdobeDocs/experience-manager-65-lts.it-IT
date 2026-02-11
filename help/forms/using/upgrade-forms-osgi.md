---
title: Aggiornamento ad AEM 6.5 Forms LTS su OSGi
description: È possibile eseguire un aggiornamento diretto da AEM 6.5.22.0 Forms a AEM 6.5 Forms LTS.
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b7aa877f9e782b0568adc7baa440dc630c690454
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 6%

---

# Aggiornamento ad AEM 6.5 Forms LTS su OSGi {#upgrade-to-aem-forms-osgi}

Per [eseguire l&#39;aggiornamento da AEM 6.5 a AEM 6.5 LTS](/help/sites-deploying/upgrade.md), eseguire l&#39;aggiornamento a AEM 6.5.22.0 Forms o versione successiva. È supportato un aggiornamento diretto da AEM 6.5.22.0 a AEM 6.5 Forms LTS.

Se utilizzi AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms, AEM 6.3 Forms, AEM 6.4 Forms o AEM 6.5 Forms, non è disponibile un aggiornamento diretto a AEM 6.5 Forms LTS. Per i percorsi di aggiornamento dettagliati, consulta la documentazione sui [percorsi di aggiornamento](/help/forms/using/upgrade.md).

Dopo l&#39;aggiornamento al service pack AEM Forms 6.5.22.0, eseguire la procedura seguente per eseguire l&#39;aggiornamento ad AEM 6.5 LTS Forms:

1. Installa il pacchetto del componente aggiuntivo AEM Forms. I passaggi sono elencati di seguito:

   1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
   1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
   1. Nella sezione **[!UICONTROL Filtri]**:
      1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
      1. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
   1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
   1. Apri [Gestione pacchetti](/help/sites-administering/package-manager.md) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
   1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

      Puoi scaricare il pacchetto anche utilizzando il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

      Dopo l’installazione del pacchetto, viene richiesto di riavviare l’istanza di AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel file &lt;crx-repository>/error.log e che il registro sia stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Puoi ignorare lo stato di questi pacchetti.


      **Riavviare l&#39;istanza di AEM con i seguenti parametri della riga di comando JVM aggiuntivi**:
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      Se il server viene avviato tramite uno script o un servizio, aggiornarlo di conseguenza in modo da includere quanto riportato sopra, in modo che siano effettivi anche dopo i riavvii successivi.

      >[!NOTE]
      >
      > Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Eseguire attività successive all&#39;installazione.

   * **Esegui utilità di migrazione**

     L’utility di migrazione rende compatibili con AEM 6.5 forms i moduli adattivi e le risorse di gestione della corrispondenza delle versioni precedenti. Puoi scaricare l’utility da AEM Software Distribution. Per informazioni dettagliate sulla configurazione e l&#39;utilizzo dell&#39;utilità di migrazione, vedere [utilità di migrazione](../../forms/using/migration-utility.md).

     Se si utilizza [Esempio per l&#39;integrazione del componente Bozze e invii](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con il database e l&#39;aggiornamento da una versione precedente, eseguire le query SQL seguenti dopo l&#39;aggiornamento:

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(Se si esegue l&#39;aggiornamento da AEM 6.2 Forms o solo dalle versioni precedenti) Riconfigura Adobe Sign**

     Se nella versione precedente di AEM Forms hai configurato Adobe Sign, riconfigura Adobe Sign da AEM Cloud Services. Per ulteriori dettagli, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

     In AEM 6.5 Forms, la versione di jQuery è aggiornata alla 3.2.1 e la versione dell’interfaccia utente jQuery è aggiornata alla 1.12.1. AEM Form utilizza JQuery in modalità **noConflict**. Pertanto, se utilizzi un’altra versione di jQuery, non vengono visualizzati problemi durante l’esecuzione di un aggiornamento. Tuttavia, quando esegui l’aggiornamento a AEM 6.5 Forms:

      * Assicurati che gli eventuali componenti personalizzati siano compatibili con le versioni di jQuery supportate.
      * Rimuovi le API non supportate dai componenti personalizzati. Per l&#39;elenco delle API rimosse, consulta la [guida all&#39;aggiornamento](https://jquery.com/upgrade-guide/3.0/). Ad esempio, viene rimosso il supporto per le API load(), .unload() ed .error(). Utilizza il metodo .on() al posto delle API di cui sopra. Ad esempio, modificare $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Se si esegue l&#39;aggiornamento da AEM 6.2 Forms o solo da versioni precedenti) Riconfigura analisi e report**

     In AEM 6.4 Forms, la variabile di traffico per la sorgente e l’evento di successo per le impression non sono disponibili. Pertanto, quando esegui l’aggiornamento da AEM 6.2 Forms o versioni precedenti, AEM Forms smette di inviare dati al server Adobe Analytics e i rapporti di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce la variabile di traffico per la versione di analisi dei moduli e l’evento di successo per la quantità di tempo trascorso su un campo. Quindi, riconfigura le analisi e i rapporti per il tuo ambiente AEM Forms. Per i passaggi dettagliati, vedi [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).

1. Verificare che il server sia stato aggiornato correttamente, che anche tutti i dati siano stati migrati correttamente e che possa funzionare normalmente.

   * **Verifica lo stato dei bundle:** Verifica che tutti i bundle siano in stato attivo.
   * **Verifica replica e replica inversa:** Pubblicare, compilare e inviare alcuni moduli migrati. Verifica anche i dati inviati.
   * **Verificare l&#39;accesso alle interfacce utente amministratore e sviluppatore:** Accedere all&#39;istanza di AEM da un account amministratore e verificare di disporre dell&#39;accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >In AEM 6.4 Forms, la struttura dell’archivio crx è cambiata. Se esegui l’aggiornamento da Forms 6.3 a AEM 6.5 Forms, utilizza i percorsi modificati per la personalizzazione che crei nuovamente. Per l&#39;elenco completo dei percorsi modificati, vedere [Ristrutturazione dell&#39;archivio Forms in AEM](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5).


## Distribuzione di AEM su JBoss EAP 8 (Windows)

### Panoramica

Questa guida fornisce istruzioni dettagliate per la distribuzione di Adobe Experience Manager (AEM) come file WAR OSGi standalone in JBoss Enterprise Application Platform (EAP) 8 in un ambiente Windows utilizzando JDK 21.

### Requisiti di sistema

Prima di iniziare il processo di distribuzione, assicurati che l’ambiente soddisfi i seguenti requisiti:

| Componente | Requisito |
|-----------|-------------|
| Sistema operativo | Windows Server 2016 o versione successiva (64 bit) |
| Java Development Kit | JDK 21 (Oracle o OpenJDK) |
| Server applicazioni | JBoss EAP 8.x |
| Distribuzione AEM | File WAR di AEM (ottenuto da Adobe) |

>[!NOTE]
>
> Verificare che la variabile di ambiente `JAVA_HOME` punti alla directory di installazione di JDK 21.

### Passaggio 1: installare JBoss EAP 8

#### Scarica EAP JBoss

1. Accedi al portale per sviluppatori Red Hat:\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. Scarica la distribuzione ZIP JBoss EAP 8 per Windows.

#### Estrai EAP JBoss

1. Estrarre il file ZIP scaricato nella directory di installazione preferita.

2. Prendere nota del percorso di questa directory come `<JBOSS_HOME>` da utilizzare in questa guida.

   **Esempio:**\
   ```C:\jboss-eap-8.0```

### Passaggio 2: preparare il file WAR di AEM

#### Ottenere AEM WAR

Acquisisci il file WAR di AEM da Adobe Software Distribution o dal tuo rappresentante Adobe.

#### Rinomina file WAR

Rinomina il file WAR in modo che rifletta il percorso di contesto URL desiderato:

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> Il nome file WAR determina il contesto URL dell&#39;applicazione. Ad esempio, `cq-quickstart.war` sarà accessibile in `/cq-quickstart`.


### Passaggio 3: configurare AEM WAR

Tutte le modifiche alla configurazione devono essere completate **prima** della distribuzione a JBoss.

#### Crea directory di lavoro

1. Creare una directory di lavoro temporanea:

   ```
   C:\aem\war-config
   ```

2. Copia il file `cq-quickstart.war` in questa directory.

#### Estrai contenuto WAR

1. Apri **Prompt dei comandi** e passa alla directory di lavoro:

   ```cmd
   cd C:\aem\war-config
   ```

2. Estrai il file WAR:

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   Viene creata una struttura di directory con `WEB-INF` e altri file dell&#39;applicazione.

### Passaggio 4: configurare il descrittore di distribuzione JBoss

#### Crea file struttura di distribuzione

1. Passare alla directory `WEB-INF` all&#39;interno del file WAR estratto:

   ```cmd
   cd WEB-INF
   ```

2. Creare un nuovo file denominato `jboss-deployment-structure.xml`.

3. Aggiungi il seguente contenuto XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure xmlns="urn:jboss:deployment-structure:1.2">
       <deployment>
           <dependencies>
               <module name="jdk.unsupported" />
           </dependencies>
       </deployment>
   </jboss-deployment-structure>
   ```

4. Salva e chiudi il file.

**Scopo:** questa configurazione fornisce l&#39;accesso ai moduli interni JDK richiesti da AEM.

### Passaggio 5: Configurare Le Impostazioni Di Caricamento Multipart

>[!NOTE]
>
> Il passaggio 5 è applicabile solo a **AEM Forms**. Se stai configurando **solo AEM**, puoi saltare questo passaggio.


#### Modifica web.xml

1. Apri `WEB-INF\web.xml` in un editor di testo.

2. Individuare la sezione `<servlet>` contenente la configurazione della modalità di esecuzione:

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. Sostituire il tag di chiusura `</servlet>` e la riga precedente con:

   ```xml
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <multipart-config>
       <max-file-size>1048576000</max-file-size>
       <max-request-size>1048576000</max-request-size>
       <file-size-threshold>0</file-size-threshold>
   </multipart-config>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

4. Salva e chiudi `web.xml`.

**Scopo:** queste impostazioni consentono caricamenti di file di grandi dimensioni (fino a 1 GB) per AEM Forms e Digital Asset Management.

### Passaggio 6: riconfezionare il file WAR

Dopo aver completato tutte le modifiche di configurazione, crea un nuovo pacchetto del file WAR.

1. Tornate alla directory di lavoro contenente il contenuto estratto:

   ```cmd
   cd C:\aem\war-config
   ```

2. Creare il nuovo file WAR:

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> Esegui questo passaggio una sola volta, dopo il completamento di tutte le configurazioni.

### Passaggio 7: distribuire e avviare AEM

#### Distribuire WAR in JBoss

1. Copia `cq-quickstart.war` ricompilato nella directory delle distribuzioni JBoss:

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **Esempio:**
   ```C:\jboss-eap-8.0\standalone\deployments```

#### Configurare le impostazioni JVM (facoltativo ma consigliato)

Prima di avviare JBoss, configura le impostazioni della memoria JVM:

1. Apri `<JBOSS_HOME>\bin\standalone.conf.bat` in un editor di testo.

1. Modificare o aggiungere la riga seguente per impostare la memoria heap:

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> Regola i valori di memoria in base alla capacità del server e ai requisiti AEM.

1. Salva e chiudi il file.

#### Avvia EAP JBoss

1. Apri **Prompt dei comandi** come **Amministratore**.

1. Passa alla directory bin JBoss:

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **Esempio:**
   ```cmd cd C:\jboss-eap-8.0\bin```

1. Avvia il server JBoss:

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **Parametri:**
   * `-b 0.0.0.0` - Associa il server a tutte le interfacce di rete
   * `-bmanagement 0.0.0.0` - Associa l&#39;interfaccia di gestione a tutte le interfacce di rete

#### Monitorare l’implementazione

Osserva l’output della console per i messaggi di distribuzione. La corretta distribuzione è indicata da:

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### Passaggio 8: accedere ad AEM

Una volta completata la distribuzione e avviato AEM:

**URL autore AEM:**
```http://<server-ip>:8080/cq-quickstart```

**Credenziali predefinite:**

* Nome utente: `admin`
* Password: `admin`

**Importante:** modificare la password predefinita immediatamente dopo il primo accesso.

### Risoluzione dei problemi

#### Problemi comuni

| Problema | Soluzione |
|-------|----------|
| Distribuzione non riuscita con ClassNotFoundException | Verificare che `jboss-deployment-structure.xml` sia configurato correttamente |
| OutOfMemoryError durante l&#39;avvio | Aumenta memoria heap in `standalone.conf.bat` |
| AEM non si avvia dopo la distribuzione | Controlla registri JBoss in `<JBOSS_HOME>\standalone\log\server.log` |
| Impossibile accedere ad AEM nel browser | Verificare che le impostazioni del firewall consentano la porta 8080 |

#### File di registro

* **Registro server JBoss:** `<JBOSS_HOME>\standalone\log\server.log`
* **Registro errori AEM:** disponibile tramite la console Web AEM dopo l&#39;avvio alle\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### Configurazione aggiuntiva

#### Configurazione delle modalità di esecuzione

Per modificare le modalità di esecuzione di AEM (creazione/pubblicazione), modificare il parametro `sling.run.modes` in `WEB-INF\web.xml` prima di ricompilare il file WAR:

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### Consigli di produzione

Per gli ambienti di produzione:

* Configurare i certificati SSL/TLS in JBoss
* Configurare gli agenti di replica di AEM
* Configurare il dispatcher per il bilanciamento del carico
* Abilita backup automatizzati
* Implementazione del monitoraggio e degli avvisi

### Documentazione correlata

* [Documentazione EAP 8 JBoss](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Documentazione di Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
* [Guida all&#39;installazione e alla distribuzione di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=it)

### Informazioni documento

| Campo | Valore |
|-------|-------|
| Ultimo aggiornamento | Febbraio 2026 |
| Versione di AEM | 6,5+ (LTS) |
| Versione JBoss | EAP 8.x |
| Versione JDK | 21 |
| Platform | Windows |


