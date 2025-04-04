---
title: Strategia di backup e ripristino per AEM Forms
description: Scopri come implementare una strategia per eseguire il backup dei dati e assicurarti che rimangano sincronizzati con i dati dei moduli di AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2f34b48a-0b95-4994-ac4f-616620a5b211
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---

# Strategia di backup e ripristino per AEM Forms{#backup-and-recovery-strategy-for-aem-forms}

Se l’implementazione di AEM Forms memorizza dati personalizzati aggiuntivi in un database diverso, è tua responsabilità implementare una strategia per eseguire il backup di tali dati e assicurarti che rimangano sincronizzati con i dati di AEM Forms. Inoltre, l&#39;applicazione deve essere progettata in modo da essere sufficientemente solida da gestire uno scenario in cui i database aggiuntivi non sono sincronizzati. Si consiglia vivamente di eseguire qualsiasi operazione di database nel contesto di una transazione per mantenere uno stato coerente.

Dopo aver identificato la modalità di utilizzo di AEM Forms, determinare quali file devono essere sottoposti a backup, la frequenza di esecuzione e la finestra di backup da rendere disponibile.

>[!NOTE]
>
>Come per qualsiasi altro aspetto dell&#39;implementazione di AEM Forms, la strategia di backup e ripristino deve essere sviluppata e testata in un ambiente di sviluppo o di staging prima di essere utilizzata in produzione per garantire che l&#39;intera soluzione funzioni come previsto senza perdita di dati.

Adobe Experience Manager (AEM) è parte integrante di AEM Forms. Pertanto, è necessario eseguire il backup di AEM e sincronizzarlo con il backup di AEM Forms come soluzione e servizi per la gestione della corrispondenza, come Forms Manager, che si basano sui dati memorizzati nella parte AEM di AEM forms.Per evitare perdite di dati, è necessario eseguire il backup dei dati specifici di AEM Forms in modo da garantire la correlazione tra GDS e AEM (archivio) e i riferimenti al database.Le directory radice di database, GDS, AEM e Content Storage devono essere ripristinate su un computer con lo stesso nome DNS dell&#39;originale.

## Tipi di backup {#types-of-backups}

La strategia di backup di AEM Forms prevede due tipi di backup:

**Immagine di sistema:** Backup di sistema completo che è possibile utilizzare per ripristinare il contenuto del computer se il disco rigido o l&#39;intero computer smette di funzionare. Il backup dell’immagine del sistema è necessario solo prima della distribuzione di produzione di AEM Forms. Le regole aziendali interne determinano quindi la frequenza con cui vengono richiesti i backup delle immagini di sistema.

**Dati specifici di AEM Forms:** I dati dell&#39;applicazione sono presenti nel database, nel GDS (Global Document Storage) e nell&#39;archivio di AEM e devono essere sottoposti a backup in tempo reale. GDS è una directory utilizzata per memorizzare i file di lunga durata utilizzati all&#39;interno di un processo. Tali file possono includere PDF, criteri o modelli di modulo.

>[!NOTE]
>
>Se è installato Content Services (obsoleto), eseguire anche il backup della directory principale di archiviazione dei contenuti. Vedere [Directory principale di archiviazione dei contenuti (solo Content Services)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

Il database viene utilizzato per memorizzare gli artefatti del modulo, le configurazioni del servizio, lo stato del processo e i riferimenti del database ai file GDS. Se nel database è stata abilitata l&#39;archiviazione dei documenti, anche i dati e i documenti persistenti in GDS vengono memorizzati nel database. È possibile eseguire il backup e il ripristino del database utilizzando i metodi seguenti:

* La modalità **Backup snapshot** indica che il sistema AEM Forms è in modalità di backup indefinita o per un numero di minuti specificato, dopo il quale la modalità di backup non è più abilitata. Per attivare o disattivare la modalità di backup delle copie istantanee, è possibile utilizzare una delle opzioni seguenti. Dopo uno scenario di ripristino, la modalità di backup delle copie istantanee non deve essere abilitata.

   * Utilizzare la pagina Impostazioni di backup nella console di amministrazione. Per attivare la modalità snapshot, selezionare la casella di controllo Esegui in modalità di backup sicuro. Deselezionare la casella di controllo per uscire dalla modalità snapshot.
   * Utilizzare lo script LCBackupMode (vedere [Eseguire il backup del database, di GDS e delle directory principali dell&#39;archiviazione dei contenuti](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Per uscire dalla modalità di backup dello snapshot, nell&#39;argomento dello script impostare il parametro `continuousCoverage` su `false` o utilizzare l&#39;opzione `leaveContinuousCoverage`.
   * Utilizzare l&#39;API di backup/ripristino fornita. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **La modalità di backup continuo** indica che il sistema è sempre in modalità di backup, con una nuova sessione in modalità di backup avviata non appena viene rilasciata la sessione precedente. Alla modalità di backup continuo non è associato alcun timeout. Quando si chiama lo script o le API LCBackupMode per uscire dalla modalità di backup continuo, viene avviata una nuova sessione di tale modalità. Questa modalità è utile per supportare backup continui, ma consente comunque di eliminare dalla directory GDS i documenti vecchi e non necessari. La modalità di backup continuo non è supportata dalla pagina Backup e ripristino. Dopo uno scenario di ripristino, la modalità di backup continua a essere abilitata. È possibile uscire dalla modalità di backup continuo (modalità di backup continuo) utilizzando lo script LCBackupMode con l&#39;opzione `leaveContinuousCoverage`.

>[!NOTE]
>
>Se si abbandona immediatamente la modalità di backup continuo, viene avviata una nuova sessione in modalità di backup. Per disabilitare completamente la modalità di backup continuo, utilizzare l&#39;opzione `leaveContinuousCoverage` nello script, che sovrascrive la sessione di backup continuo esistente. In modalità di backup delle copie istantanee, è possibile lasciare la modalità di backup come si fa di solito.

Per evitare la perdita di dati, è necessario eseguire il backup dei dati specifici dei moduli AEM in modo da garantire la correlazione tra i documenti di directory radice di archiviazione dei contenuti e GDS e i riferimenti al database.

>[!NOTE]
>
>Quando il GDS viene memorizzato nel file system e non nel database, eseguire il backup del database prima del backup del GDS.

## Considerazioni speciali per il backup e il ripristino {#special-considerations-for-backup-and-recovery}

Se è necessario ripristinare AEM Forms in un ambiente diverso a causa delle modifiche seguenti, attenersi alle linee guida riportate di seguito.

* Modifica dell’indirizzo IP, del nome host o della porta del server AEM Forms
* Modifica delle lettere di unità o del percorso della directory
* Passare a un altro nome, porta o host di database

In genere, tali scenari di ripristino sono causati da un guasto hardware del server che ospita l&#39;application server, il server di database o il server Forms. Oltre alle configurazioni specifiche di AEM Forms descritte in questa sezione, se il nome host o l’indirizzo IP di un server AEM Forms cambia, è necessario apportare le modifiche necessarie anche ad altre parti della distribuzione di AEM Forms, come i load balancer e i firewall.

### Cosa non può essere modificato {#what-cannot-be-changed}

Anche se è possibile modificare il server di database e molti altri parametri, non è possibile modificare il tipo di server applicazioni o il tipo di database quando si recupera AEM Forms da un backup. Se, ad esempio, si ripristina un backup di AEM Forms, non è possibile modificare il server applicazioni da JBoss a WebLogic o database da Oracle a DB2. Inoltre, i moduli AEM recuperati devono utilizzare gli stessi percorsi del file system, ad esempio la directory dei font.

### Riavvio dopo un ripristino {#restarting-after-a-recovery}

Prima di riavviare Forms Server dopo un ripristino, eseguire le operazioni seguenti:

1. Avviare il sistema in modalità di manutenzione.
1. Effettua le seguenti operazioni per garantire che Gestione moduli sia sincronizzato con AEM Forms in modalità manutenzione:

   1. Vai a https://&lt;*server*>:&lt;*porta*>/lc/fm e accedi utilizzando le credenziali amministratore/password.
   1. Fai clic sul nome dell’utente (in questo caso Amministratore privilegiato) nell’angolo in alto a destra.
   1. Fare clic su **Opzioni amministratore**.
   1. Fai clic su **Inizio** per sincronizzare le risorse dal repository.

1. In un ambiente cluster, il nodo principale (rispetto ad AEM) deve trovarsi prima dei nodi secondari.
1. Verificare che non vengano avviati processi da origini interne o esterne, ad esempio gli iniziatori di processi Web, SOAP o EJB, fino alla convalida del normale funzionamento del sistema.

Se il database principale di AEM Forms viene spostato o modificato, consultare le guide all&#39;installazione relative al server applicazioni per informazioni sull&#39;aggiornamento delle informazioni di connessione al database per le origini dati IDP_DS e EDC_DS di AEM Forms.

>[!NOTE]
> 
> Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

### Modifica del nome host o dell’indirizzo IP di AEM Forms {#changing-the-aem-forms-hostname-or-ip-address}

In un cluster, se si utilizza il caching TCP anziché UDP, è necessario aggiornare la configurazione del localizzatore di cache. Consulta &quot;Configuring the caching locators (caching using TCP only)&quot; nella guida alla configurazione relativa al server applicazioni.

### Modifica dei percorsi del file system del nodo di AEM Forms {#changing-the-aem-forms-node-file-system-paths}

Se si modificano i percorsi dei file system per un nodo standalone, è necessario aggiornare i riferimenti appropriati nelle preferenze, in altre configurazioni di sistema, in applicazioni personalizzate e in applicazioni AEM Form distribuite. Per un cluster, invece, tutti i nodi devono utilizzare la stessa configurazione del percorso del file system. Impostare la directory radice Global Document Storage (GDS) e assicurarsi che punti a una copia del GDS ripristinato sincronizzata con il database ripristinato. L&#39;impostazione del percorso GDS è importante perché GDS può contenere dati destinati a persistere durante il riavvio del server applicazioni.

In un ambiente cluster, la configurazione del percorso del file system dell&#39;archivio deve essere la stessa per tutti i nodi del cluster prima del backup e dopo il ripristino.

Utilizzare lo script `LCSetGDS` nella cartella `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` per impostare il percorso GDS dopo aver modificato i percorsi del file system. Per ulteriori dettagli, vedere il file `ReadMe.txt` nella stessa cartella. Se non è possibile utilizzare il percorso della directory GDS precedente, è necessario utilizzare lo script `LCSetGDS` per impostare il nuovo percorso del GDS prima di avviare AEM Forms.

>[!NOTE]
>
>Questa circostanza è l&#39;unica in base alla quale utilizzare questo script per modificare la posizione di GDS. Per modificare la posizione di GDS durante l&#39;esecuzione di AEM Forms, utilizzare la console di amministrazione. (Vedi [Configurare le impostazioni generali di AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Dopo aver impostato il percorso GDS, avviare Forms Server in modalità di manutenzione e utilizzare la console di amministrazione per aggiornare i percorsi del file system rimanenti per il nuovo nodo. Dopo aver verificato che tutte le configurazioni necessarie siano state aggiornate, riavvia e verifica AEM Forms.
