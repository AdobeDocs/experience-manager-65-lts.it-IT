---
title: Impostazioni AEM Forms generali
description: Scopri come configurare le impostazioni della pagina Configurazioni core nella console di amministrazione per migliorare le prestazioni del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 54e7132d-3009-4a83-9f03-55bb2c41ae90
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 0%

---

# Impostazioni AEM Forms generali {#general-aem-forms-settings}

La pagina Configurazioni core della console di amministrazione fornisce le impostazioni che possono contribuire a migliorare le prestazioni del sistema. Dopo aver configurato o aggiornato queste impostazioni, riavviare il server applicazioni.

>[!NOTE]
>
> * Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.
> * Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

Per informazioni sull&#39;attivazione della modalità di backup sicuro, vedere [Attivazione e disattivazione della modalità di backup sicuro](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>I file nella directory temporanea e i documenti di lunga durata nella directory principale GDS (Global Document Storage) possono contenere informazioni utente riservate, ad esempio informazioni che richiedono credenziali speciali quando si accede utilizzando le API o le interfacce utente. È quindi importante che questa directory sia protetta correttamente utilizzando tutti i metodi disponibili per il sistema operativo. È consigliabile che solo l&#39;account del sistema operativo utilizzato per eseguire l&#39;Application Server disponga dell&#39;accesso in lettura e scrittura a questa directory.


1. Nella console di amministrazione, selezionare **[!UICONTROL Impostazioni > Impostazioni sistema di base > Configurazioni]**.
1. Nella pagina Configurazioni core, modificare le opzioni in base alle esigenze e selezionare **[!UICONTROL OK]**. Per informazioni dettagliate sulle opzioni, vedere [Opzioni di configurazione principali](configure-general-aem-forms-settings.md#core-configurations-options).


## Opzioni configurazioni core {#core-configurations-options}

**Posizione della directory temporanea** Percorso della directory in cui AEM Forms creerà i file temporanei del prodotto. Se il valore di questa impostazione è vuoto, per impostazione predefinita la posizione viene impostata sulla directory temporanea di sistema. Verificare che la directory temporanea sia una cartella scrivibile.

>[!NOTE]
>
>Verificare che la directory temporanea si trovi nel file system locale. AEM forms non supporta una directory temporanea in una posizione remota.

**Directory radice di archiviazione documenti globale** *ndash; La directory radice di archiviazione documenti globale (GDS) viene utilizzata per i seguenti scopi:

* Archiviazione di documenti di lunga durata. I documenti di lunga durata non hanno un tempo di scadenza e persistono finché non vengono rimossi (ad esempio, i file PDF utilizzati in un processo di workflow). I documenti di lunga durata sono una parte critica dello stato generale del sistema. Se alcuni o tutti questi documenti vengono persi o danneggiati, il server Forms potrebbe diventare instabile. Pertanto, è importante che questa directory sia memorizzata su un dispositivo RAID.
* Memorizzazione dei documenti temporanei necessari durante l&#39;elaborazione.

>[!NOTE]
>
>È inoltre possibile abilitare l&#39;archiviazione dei documenti nel database di AEM Forms. Tuttavia, le prestazioni del sistema sono migliori quando si utilizza GDS.

* Trasferimento di documenti tra nodi in un cluster. Se si esegue AEM Forms in un ambiente cluster, questa directory deve essere accessibile da tutti i nodi del cluster.
* Ricezione dei parametri in entrata dalle chiamate API remote.

Se non si specifica una directory radice GDS, la directory predefinita è una directory del server applicazioni:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modifica del valore della directory principale GDS deve essere eseguita con particolare attenzione. La directory GDS viene utilizzata per memorizzare sia i file di lunga durata utilizzati all’interno di un processo che i componenti critici di AEM Forms. La modifica della posizione della directory GDS rappresenta una modifica importante del sistema. Una configurazione errata della posizione della directory GDS renderà AEM Forms inoperativo e potrebbe richiedere una reinstallazione completa di AEM Forms. Se si specifica una nuova posizione per la directory GDS, è necessario arrestare l&#39;Application Server e migrare i dati prima di riavviare il server. L&#39;amministratore di sistema deve spostare tutti i file dalla posizione precedente alla nuova posizione, mantenendo la struttura di directory interna.

>[!NOTE]
>
>Non specificare la stessa directory per la directory temporanea e la directory GDS.

Per ulteriori informazioni sulla directory GDS, vedere [Preparazione all&#39;installazione di AEM Forms (server singolo)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Posizione della directory Adobe Server Fonts** *ndash; digitare il percorso della directory che contiene i caratteri del server Adobe. Questi tipi di carattere vengono installati con AEM Forms. Il percorso predefinito per questi tipi di carattere è la directory [root]/font di aem-forms. Se questa directory non è accessibile, potete copiare i font altrove e utilizzare questa impostazione per specificare la nuova posizione.

**Posizione della directory Caratteri cliente** *ndash; digitare il percorso di una directory contenente i caratteri aggiuntivi che si desidera utilizzare.

***nota **: i tipi di carattere vengono selezionati dalla cache dei tipi di carattere del sistema Windows ed è necessario riavviare il sistema per aggiornare la cache. Dopo aver specificato la directory dei caratteri del cliente, assicurarsi di riavviare il sistema in cui è installato AEM Forms.*

**Posizione della directory System Fonts** *ndash; digitare il percorso della directory dei font fornita dal sistema operativo. È possibile aggiungere più directory, separate da un punto e virgola **;**.

**Percorso del file di configurazione dei servizi dati** *ndash; Specifica il percorso del file services-config.xml. Per impostazione predefinita, questo file è incorporato nel file adobe-core-appserver.ear e non è accessibile all’utente. Una copia del file services-config.xml predefinito si trova nella directory principale di [aem-forms]\sdk\misc\DataServices\Server-Configuration. Se il file è stato modificato e spostato, digitare la nuova posizione in questo campo.

Il file di configurazione dei servizi dati consente di personalizzare le impostazioni dei servizi dati, ad esempio il tipo di autenticazione e l&#39;output di debug.

Questa impostazione è vuota per impostazione predefinita.

**Dimensione massima predefinita in linea del documento (byte)** *ndash; numero massimo di byte conservati in memoria per il passaggio di documenti tra vari componenti di AEM Forms. Utilizzare questa impostazione per ottimizzare le prestazioni. I documenti inferiori a questo numero vengono memorizzati in memoria e memorizzati nel database. I documenti che superano questo limite massimo vengono archiviati sul disco rigido.

Questa impostazione è obbligatoria. Il valore predefinito è 65536 byte.

**Timeout eliminazione documento predefinito (secondi)** *ndash; la quantità massima di tempo, in secondi, durante la quale un documento passato tra i vari componenti di AEM Form viene considerato attivo. Trascorso questo tempo, i file utilizzati per memorizzare il documento saranno rimossi. Utilizzare questa impostazione per controllare l&#39;utilizzo dello spazio su disco.

Questa impostazione è obbligatoria. Il valore predefinito è 600 secondi.

**Intervallo di sweep del documento (secondi)** *ndash; la quantità di tempo, in secondi, tra i tentativi di eliminare i file che non sono più necessari e sono stati utilizzati per passare i dati del documento tra i servizi.

Questa impostazione è obbligatoria. Il valore predefinito è 30 secondi.

**Abilita FIPS** *ndash; selezionare questa opzione per abilitare la modalità FIPS. Il Federal Information Processing Standard (FIPS) 140-2 è uno standard di crittografia definito dal governo degli Stati Uniti. Quando viene eseguito in modalità FIPS, AEM forms limita la protezione dei dati agli algoritmi approvati FIPS 140-2 utilizzando il modulo di crittografia RSA BSAFE Crypto-C 2.1.

La modalità FIPS non supporta gli algoritmi di crittografia utilizzati nelle versioni di Adobe Acrobat® precedenti alla 7.0. Se la modalità FIPS è attivata e si utilizza il servizio Crittografia per crittografare il PDF utilizzando una password con un livello di compatibilità impostato su Acrobat 5, il tentativo di crittografia non riuscirà e verrà restituito un errore.

In generale, quando FIPS è abilitato, il servizio Assembler non applica la crittografia password a nessun documento. Se si tenta di eseguire questa operazione, viene generata un&#39;eccezione FIPSModeException che indica che &quot;la crittografia della password non è consentita in modalità FIPS&quot;. Inoltre, l&#39;elemento PDFsFromBookmarks del documento Description XML (DDX) non è supportato in modalità FIPS quando il documento di base è crittografato con password.

>[!NOTE]
>
>Il software AEM Forms non convalida il codice per garantire la compatibilità FIPS. Fornisce una modalità operativa FIPS in modo che gli algoritmi approvati FIPS vengano utilizzati per i servizi di crittografia dalle librerie approvate FIPS (RSA).

**Abilita WSDL** *ndash; selezionare questa opzione per abilitare la generazione WSDL (Web Service Definition Language) per tutti i servizi che fanno parte di AEM Forms.

Abilita questa opzione negli ambienti di sviluppo, in cui gli sviluppatori utilizzano la generazione WSDL per creare le applicazioni client. Puoi scegliere di disabilitare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

**Abilitare l&#39;archiviazione dei documenti nel database** *ndash; Selezionare questa opzione per memorizzare i documenti di lunga durata nel database di AEM Forms. L&#39;attivazione di questa opzione non elimina la necessità di una directory GDS. Tuttavia, la scelta di questa opzione semplifica i backup di AEM Forms. Se si utilizza solo il GDS, un backup comporta l&#39;attivazione della modalità di backup del sistema AEM FormsAEM Forms e il completamento dei backup del database e del GDS. Se si seleziona l&#39;opzione del database, il backup comporta il completamento del backup del database per una nuova installazione o il completamento del backup del database e del backup unico del GDS per un aggiornamento. Potrebbe essere necessaria una gestione aggiuntiva del database per eliminare processi e dati rispetto a una configurazione che utilizza solo GDS. Consultate Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti.

**Abilita statistica chiamata DSC** *ndash; quando questa opzione è selezionata, AEM forms tiene traccia delle statistiche di chiamata, ad esempio il numero di chiamate, il tempo impiegato per la chiamata e il numero di errori nelle chiamate. Queste informazioni vengono memorizzate in un bean JMX in modo da poter utilizzare Java™ JConsole o un software di terze parti per esaminare le statistiche. Se non desideri visualizzare queste statistiche, deseleziona questa opzione per migliorare le prestazioni di AEM Forms.

**Abilita RDS** *ndash; se si seleziona questa opzione, verrà abilitato il servlet di Servizi di sviluppo remoto (RDS) in AEM Forms. Quando questa opzione è abilitata, gli strumenti lato client possono interagire con Data Services per eseguire operazioni quali la distribuzione o l’annullamento della distribuzione di modelli per creare destinazioni ed endpoint o per individuare i modelli distribuiti negli endpoint. Per impostazione predefinita, questa opzione non è selezionata.

**Consenti richiesta RDS non protetta** *ndash; se questa opzione è selezionata, le richieste RDS non devono utilizzare https. Per impostazione predefinita, questa opzione non è selezionata e tutte le comunicazioni a Data Services devono essere richieste https.

**Consenti caricamento di documenti non protetti da applicazioni Flex** *ndash; Il servlet di caricamento file utilizzato per caricare documenti da applicazioni Adobe Flex® in AEM Forms richiede che gli utenti siano autenticati e autorizzati prima di poter caricare documenti. All&#39;utente deve essere assegnato il ruolo di Utente dell&#39;applicazione di caricamento documento o un altro ruolo che includa l&#39;autorizzazione di caricamento documento. In questo modo si evita che utenti non autorizzati possano caricare documenti sul server AEM Forms. Selezionare questa opzione se si desidera disattivare questa funzionalità di protezione in un ambiente di sviluppo o per garantire la compatibilità con le versioni precedenti di AEM Forms. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, consulta &quot;Richiamare AEM Forms utilizzando AEM Forms Remoting&quot; in Programmazione con AEM forms.

**Consenti caricamento di documenti non protetti da applicazioni Java SDK** *ndash; i caricamenti HTTP DocumentManager devono essere protetti. Per impostazione predefinita, i caricamenti HTTP richiedono che gli utenti siano autenticati e autorizzati prima di poter caricare i documenti. All&#39;utente deve essere assegnato il ruolo Utente servizi o un altro ruolo contenente l&#39;autorizzazione Richiamo servizio. In questo modo si evita che utenti non autorizzati possano caricare documenti su Forms Server. Selezionare questa opzione se si desidera disattivare questa funzionalità di protezione in un ambiente di sviluppo, per garantire la compatibilità con le versioni precedenti di AEM Form o in base alla configurazione del firewall. Per impostazione predefinita, questa opzione non è selezionata. Per informazioni dettagliate, consulta &quot;Richiamare AEM Forms utilizzando l’API Java&quot; in Programmazione con AEM Forms.
