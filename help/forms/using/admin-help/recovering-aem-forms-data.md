---
title: Recupero dei dati dei moduli di AEM
description: Questo documento descrive i passaggi necessari per recuperare i dati dei moduli di AEM.
contentOwner: admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 6345edda-cdc6-4e13-ade6-2dd6de9d9616
source-git-commit: f7adcbe7700d0ea9cbd18eb0b59bcd76f56e8cc5
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# Recupero dei dati dei moduli di AEM {#recovering-the-aem-forms-data}

Questa sezione descrive i passaggi necessari per recuperare i dati dei moduli di AEM. Vedere anche [Considerazioni speciali per il backup e il ripristino](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>È necessario ripristinare il database, il GDS, il repository di AEM e le directory principali di archiviazione del contenuto in un computer con lo stesso nome DNS dell&#39;originale.

AEM forms deve essere ripristinato in modo affidabile dai seguenti errori:

**Errore disco:** Per ripristinare il contenuto del database è necessario il supporto di backup più recente.

**Danneggiamento dei dati:** I file system non registrano le transazioni passate e i sistemi potrebbero accidentalmente sovrascrivere i dati di processo richiesti.

**Errore utente:** il recupero è limitato ai dati resi disponibili dal database. Se i dati sono stati memorizzati e sono disponibili, il ripristino è semplificato.

**Interruzione dell&#39;alimentazione, arresto anomalo del sistema:** Le API del file system spesso non sono progettate o utilizzate in modo affidabile per evitare errori di sistema imprevisti. Se si verifica un&#39;interruzione dell&#39;alimentazione o un arresto anomalo del sistema, è più probabile che il contenuto del documento memorizzato nel database sia aggiornato rispetto al contenuto memorizzato in un file system.

Se si utilizza la modalità di backup continuo, è ancora attiva la modalità di backup dopo il ripristino. Se si utilizza la modalità di backup delle copie istantanee, non è attiva la modalità di backup dopo il ripristino.

Quando si esegue il ripristino da un backup in un nuovo sistema, le seguenti configurazioni possono essere diverse. Questa differenza non dovrebbe influire sul corretto ripristino dell’applicazione AEM Forms:

* Indirizzo IP
* Configurazione del sistema fisico (CPU, disco, memoria)
* Posizione GDS

>[!NOTE]
>
>Il backup della directory radice di archiviazione dei contenuti deve essere ripristinato nella posizione della directory impostata durante la configurazione di Content Services.

Se un singolo nodo di un cluster multinodo non riesce e i nodi rimanenti del cluster funzionano correttamente, eseguire la procedura di ripristino del cluster a nodo singolo.

## Recuperare i dati dei moduli di AEM {#recover-the-aem-forms-data}

1. Arrestare il server applicazioni e i servizi di AEM Forms se in esecuzione.
1. Se necessario, ricreare il sistema fisico da un&#39;immagine di sistema. Ad esempio, questo passaggio potrebbe non essere necessario se il motivo del ripristino è un server di database difettoso.
1. Applica patch o aggiornamenti ai moduli di AEM che sono stati applicati dopo la creazione dell’immagine. Queste informazioni sono state registrate nella procedura di backup. Per AEM forms è necessario eseguire l&#39;operazione patch allo stesso livello di patch utilizzato al momento del backup.
1. (Server applicazioni WebSphere®) Se si sta eseguendo il ripristino in una nuova istanza dell&#39;Application Server WebSphere®, eseguire il comando restoreConfig.bat/sh.
1. Recuperare il database di AEM Forms eseguendo prima un&#39;operazione di ripristino del database utilizzando i file di backup del database e quindi applicando i redo log delle transazioni al database ripristinato. (Vedere [database di AEM forms](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Per ulteriori informazioni, vedere uno degli articoli della Knowledge Base riportati di seguito.

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [Backup e ripristino Oracle per AEM Forms](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [Backup e ripristino MySQL per AEM forms](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. Recuperare la directory GDS eliminando prima il contenuto della directory GDS nell&#39;installazione esistente di AEM Forms e quindi copiando il contenuto della directory GDS dal GDS di cui è stato eseguito il backup. Se si è modificato il percorso della directory GDS, vedere [Modifica del percorso GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Rinominare la directory di backup GDS da ripristinare come illustrato negli esempi seguenti:

   >[!NOTE]
   >
   >Se la directory /restore esiste già, eseguirne il backup e quindi eliminarla prima di rinominare la directory /backup che contiene i dati più recenti.

   * (JBoss®) Rinominare `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` in:

     `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Rinominare `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` in:

     `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere®) Rinominare `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` in:

     `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Ripristinare la directory principale di archiviazione dei contenuti eliminando prima il contenuto della directory principale di archiviazione dei contenuti nell’installazione esistente di AEM Forms e quindi recuperando il contenuto seguendo le attività per gli ambienti autonomi o cluster:

   >[!NOTE]
   >
   >Il backup della directory radice di archiviazione dei contenuti deve essere ripristinato nella posizione della directory radice di archiviazione dei contenuti impostata durante la configurazione di Content Services (obsoleto).

   **Standalone:** Durante il processo di ripristino, ripristinare tutte le directory di cui è stato eseguito il backup. Quando queste directory vengono ripristinate, se è presente la directory /backup-lucene-indexes, rinominarla in /lucene-indexes. In caso contrario, la directory degli indici di tipo Lucene dovrebbe già esistere e non è richiesta alcuna azione.

   **Cluster:** Durante il processo di ripristino, ripristinare tutte le directory di cui è stato eseguito il backup. Per ripristinare la directory principale dell&#39;indice, effettuare le seguenti operazioni su ciascun nodo del cluster:

   * Elimina tutto il contenuto nella directory radice indice.
   * Se la directory /backup-lucene-indexes è presente, copiare il contenuto della directory radice dell&#39;archiviazione dei contenuti */backup-lucene-indexes nella directory radice dell&#39;indice ed eliminare la directory radice dell&#39;archiviazione dei contenuti*/backup-lucene-indexes.**
   * Se la directory /lucene-indexes è presente, copiare il contenuto della directory radice di archiviazione del contenuto *Directory radice di archiviazione del contenuto*/indice del lucene nella directory radice dell&#39;indice.

1. Ripristina/ripristina l’archivio CRX.

   * **Autonomo**

     *Ripristina istanze di authoring e pubblicazione*: se si verifica un problema, è possibile ripristinare l&#39;ultimo stato di backup del repository eseguendo i passaggi descritti in [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

     Il ripristino completo del nodo Author verifica anche il ripristino dei dati di Forms Manager e AEM Forms Workspace.

   * **Cluster**

     Per il ripristino in un ambiente cluster, vedere [Strategia di backup e ripristino in un ambiente cluster](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Eliminare tutti i file temporanei di AEM Form creati nella directory java.io.temp o nella directory temporanea di Adobe.
1. Avviare AEM Forms (vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Modifica della posizione GDS durante il ripristino {#changing-the-gds-location-during-recovery}

Se il GDS viene ripristinato in una posizione diversa da quella originale, eseguire lo script LCSetGDS per impostare il GDS nella nuova posizione. Script nella cartella `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline`. Lo script accetta due parametri, `defaultGDS` e `newGDS`. Per istruzioni su come eseguire lo script, vedere il file `ReadMe.txt` nella stessa cartella.

>[!NOTE]
>
>Se è stata abilitata l&#39;archiviazione dei documenti nel database, non è necessario modificare la posizione di GDS.

>[!NOTE]
>
>Questa circostanza è l&#39;unica in base alla quale utilizzare questo script per modificare la posizione di GDS. Per modificare la posizione di GDS durante l&#39;esecuzione di AEM Forms, utilizzare la console di amministrazione. (Vedi [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>La distribuzione dei componenti non riuscirà in Windows se la directory GDS si trova nella directory principale dell&#39;unità (ad esempio, D:\). Per GDS, è necessario assicurarsi che la directory non si trovi nella radice dell&#39;unità, ma in una sottodirectory. Ad esempio, la directory dovrebbe essere D:\GDS e non semplicemente D:\.

## Ripristino di GDS in un ambiente cluster {#recovering-the-gds-to-a-clustered-environment}

Per modificare la posizione GDS in un ambiente cluster, arrestare l&#39;intero cluster ed eseguire lo script LCSetGDS su un singolo nodo del cluster. (Vedere [Modifica del percorso GDS durante il ripristino](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Avviare solo tale nodo. Quando il nodo è completamente avviato, gli altri nodi del cluster possono essere avviati in modo sicuro e punteranno correttamente al nuovo GDS.

>[!NOTE]
>
>Se non è possibile assicurarsi di avviare completamente un nodo prima di avviare altri nodi, è necessario eseguire lo script LCSetGDS su ogni nodo del cluster prima di avviare il cluster.
