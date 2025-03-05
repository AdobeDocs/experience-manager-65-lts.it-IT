---
title: Attività di manutenzione pre-aggiornamento
description: Scopri le attività di pre-aggiornamento consigliate per AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b7304709729915dbcc27533caf88b61cd5657a2c
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# Attività di manutenzione pre-aggiornamento{#pre-upgrade-maintenance-tasks}

Prima di iniziare l’aggiornamento, è importante seguire queste attività di manutenzione per garantire che il sistema sia pronto e possa essere ripristinato nel caso in cui si verifichino dei problemi:

* [Definizioni indice](#index-definitions)
* [Garantire spazio su disco sufficiente](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Backup completo di AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Genera il file quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurare il flusso di lavoro e la rimozione del registro di controllo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Installare, configurare ed eseguire le attività di pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Rimuovi aggiornamenti dalla directory /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Arresta tutte le istanze di standby a freddo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Disabilita processi pianificati personalizzati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Esegui pulizia revisioni offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Esegui raccolta oggetti inattivi archivio dati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Aggiorna lo schema del database se necessario](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Ruota file di registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Definizioni indice {#index-definitions}

Assicurati di aver installato le definizioni dell’indice richieste rilasciate con i Service Pack di AEM 6.5 forniti almeno fino a AEM Service Pack 22. (Per ulteriori informazioni, consultare le [note sulla versione del servicepack AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/release-notes/release-notes)).

## Garantire spazio su disco sufficiente {#ensure-sufficient-disk-space}

Durante l&#39;esecuzione dell&#39;aggiornamento, verificare che lo spazio su disco sia sufficiente.

## Backup completo di AEM {#fully-back-up-aem}

Prima di iniziare l’aggiornamento, è necessario eseguire il backup completo di AEM. Assicurati di eseguire il backup dell’archivio, dell’installazione dell’applicazione, dell’archivio dati e delle istanze Mongo, se applicabile. Per ulteriori informazioni sul backup e il ripristino di un&#39;istanza di AEM, vedere [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

## Genera il file quickstart.properties {#generate-quickstart-properties}

All&#39;avvio di AEM dal file jar, viene generato un file `quickstart.properties` in `crx-quickstart/conf`. Se AEM è stato avviato solo in passato con lo script di avvio, questo file non è presente e l’aggiornamento non riesce. Verifica l’esistenza di questo file e, se non è presente, riavvia AEM dal file jar.

## Configurare il flusso di lavoro e la rimozione del registro di controllo {#configure-wf-audit-purging}

Le attività `WorkflowPurgeTask` e `com.day.cq.audit.impl.AuditLogMaintenanceTask` richiedono configurazioni OSGi separate e non possono funzionare senza di esse. In caso di errore durante l’esecuzione delle attività di pre-aggiornamento, la causa più probabile è la mancanza di configurazioni. Di conseguenza, se non desideri eseguirle, accertati di aggiungere configurazioni OSGi per queste attività o rimuoverle completamente dall’elenco delle attività di ottimizzazione pre-aggiornamento. La documentazione relativa alla configurazione delle attività di eliminazione del flusso di lavoro è disponibile all&#39;indirizzo [Amministrazione delle istanze del flusso di lavoro](/help/sites-administering/workflows-administering.md), mentre la configurazione delle attività di manutenzione del registro di controllo è disponibile all&#39;indirizzo [Gestione del registro di controllo in AEM 6](/help/sites-administering/operations-audit-log.md).


## Installare, configurare ed eseguire le attività di pre-aggiornamento {#install-configure-run-pre-upgrade-tasks}

Le attività di manutenzione pre-aggiornamento che prima dovevano essere eseguite manualmente vengono ottimizzate e automatizzate. L&#39;ottimizzazione della manutenzione pre-aggiornamento consente di attivare in modo unificato queste attività e di esaminarne i risultati su richiesta.

### Come usarlo {#how-to-use-it}

Il componente OSGI `PreUpgradeTasksMBean` è preconfigurato con un elenco di attività di manutenzione pre-aggiornamento che possono essere eseguite tutte contemporaneamente. Puoi configurare le attività seguendo la procedura seguente:

1. Vai alla console Web navigando su *https://serveraddress:serverport/system/console/configMgr*

1. Cerca &quot;**preupgrade detasks**&quot;, quindi fai clic sul primo componente corrispondente. Il nome completo del componente è `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modificare l&#39;elenco delle attività di manutenzione che devono essere eseguite come illustrato di seguito:

   ![1487758925984](assets/1487758925984.png)

Di seguito è riportata una descrizione della modalità di esecuzione per cui ogni attività di manutenzione è progettata.

| Attività | Note |
|---|---|
| WorkflowPurgeTask | Prima di eseguire, è necessario configurare Adobe Granite Workflow Purge Configuration OSGi. |
| GenerateBundlesListFileTask |   |
| RevisionCleanupTask |   |
| com.day.cq.audit.impl.AuditLogMaintenanceTask | Prima di eseguire, è necessario configurare la configurazione OSGi dell’utilità di pianificazione per la rimozione del registro di controllo. |

### Configurazione predefinita dei controlli di integrità pre-aggiornamento {#default-configuration-of-the-pre-upgrade-health-checks}

Il componente OSGI `PreUpgradeTasksMBeanImpl` è preconfigurato con un elenco di tag di verifica stato pre-aggiornamento da eseguire quando viene chiamato il metodo `runAllPreUpgradeHealthChecks`:

* **system** - tag utilizzato dai controlli di integrità della manutenzione granite

* **pre-aggiornamento** - un tag personalizzato che può essere aggiunto a tutti i controlli di integrità che puoi impostare per l&#39;esecuzione prima di un aggiornamento

**Metodi MBean**

È possibile accedere alla funzionalità bean gestito utilizzando [Console JMX](/help/sites-administering/jmx-console.md).

Per accedere a MBean:

1. Passaggio alla console JMX all&#39;indirizzo *https://serveraddress:serverport/system/console/jmx*
1. Cerca **PreUpgradeTasks** e fai clic sul risultato

1. Seleziona un metodo dalla sezione **Operazioni** e seleziona **Richiama** nella finestra seguente.

Di seguito è riportato un elenco di tutti i metodi disponibili esposti da `PreUpgradeTasksMBeanImpl`:

| Nome metodo | Tipo | Descrizione |
|---|---|---|
| runAllPreUpgradeTasks() | AZIONE | Esegue tutte le attività di manutenzione pre-aggiornamento nell’elenco. |
| runPreUpgradeTask(preUpgradeTaskName) | AZIONE | Esegue l&#39;attività di manutenzione pre-aggiornamento con il nome specificato come parametro. |
| getPreUpgradeTaskLastRunTime(preUpgradeTaskName) | AZIONE | Visualizza il tempo di esecuzione esatto dell&#39;attività di manutenzione pre-aggiornamento con il nome specificato come parametro. |
| getPreUpgradeTaskLastRunState(preUpgradeTaskName) | AZIONE | Visualizza l&#39;ultimo stato di esecuzione dell&#39;attività di manutenzione pre-aggiornamento con il nome specificato come parametro. |
| runAllPreUpgradeHealthChecks(shutDownOnSuccess) | AZIONE | Esegue tutti i controlli di integrità pre-aggiornamento e ne salva lo stato in un file denominato preUpgradeHCStatus.properties nel percorso della home di sling. Se shutDownOnSuccess è impostato su true, l&#39;istanza di AEM viene chiusa, ma solo se tutti i controlli di integrità precedenti all&#39;aggiornamento hanno lo stato OK. Il file delle proprietà viene utilizzato come precondizione per qualsiasi aggiornamento futuro e il processo di aggiornamento viene interrotto se l&#39;esecuzione del controllo di integrità pre-aggiornamento non è riuscita. Se si desidera ignorare il risultato dei controlli di integrità precedenti all&#39;aggiornamento e avviare comunque l&#39;aggiornamento, è possibile eliminare il file. |
| detectUsageOfUnavailableAPI(aemVersion) | AZIONE | Elenca tutti i pacchetti importati che non sono più soddisfatti quando si esegue l’aggiornamento alla versione di AEM specificata. La versione AEM di destinazione deve essere fornita come parametro. |

>[!NOTE]
>
>I metodi MBean possono essere richiamati tramite:
>
>* Console JMX
>* Qualsiasi applicazione esterna che si connette a JMX
>* cURL
>

## Rimuovi aggiornamenti dalla directory /install {#remove-updates-install-directory}

>[!NOTE]
>
>Rimuovi solo i pacchetti dalla directory crx-quickstart/install DOPO aver chiuso l&#39;istanza di AEM. Questo passaggio è uno degli ultimi prima di avviare la procedura di aggiornamento sul posto.

Rimuovere i Service Pack, i Feature Pack o gli hotfix distribuiti tramite la directory `crx-quickstart/install` nel file system locale. In questo modo si evita l’installazione involontaria dei vecchi hotfix e service pack oltre alla nuova versione di AEM al termine dell’aggiornamento.

## Arresta tutte le istanze di standby a freddo {#stop-tarmk-coldstandby-instance}

Se si utilizza lo standby a freddo TarMK, interrompere le istanze di standby a freddo. In questo modo è possibile tornare online in caso di problemi durante l&#39;aggiornamento. Al termine dell’aggiornamento, è necessario ricompilare le istanze in standby a freddo dalle istanze primarie aggiornate.

## Disabilita processi pianificati personalizzati {#disable-custom-scheduled-jobs}

Disattiva tutti i processi pianificati OSGi inclusi nel codice dell’applicazione.

## Esegui pulizia revisioni offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Questo passaggio è necessario solo per le installazioni TarMK

Se utilizzi TarMK, esegui Offline Revision Cleanup prima dell’aggiornamento. In questo modo il passaggio di migrazione dell’archivio e le successive attività di aggiornamento vengono eseguiti molto più rapidamente e si garantisce che la pulizia delle revisioni online possa essere eseguita correttamente al termine dell’aggiornamento. Per informazioni sull&#39;esecuzione della pulizia delle revisioni non in linea, vedere [Esecuzione della pulizia delle revisioni non in linea](/help/sites-deploying/revision-cleanup.md#revision-cleanuprevision-cleanup).

## Esegui raccolta oggetti inattivi archivio dati {#execute-datastore-garbage-collection}

Dopo aver eseguito la pulizia delle revisioni sulle istanze di CRX3, è necessario eseguire la raccolta oggetti inattivi del datastore per rimuovere eventuali BLOB senza riferimenti nell’archivio dati. Per istruzioni, consulta la documentazione su [Data Store Garbage Collection](/help/sites-administering/data-store-garbage-collection.md).

## Ruota file di registro {#rotate-log-files}

Adobe consiglia di archiviare i file di registro correnti prima di iniziare l’aggiornamento. In questo modo è più facile monitorare e analizzare i file di registro durante e dopo l’aggiornamento per identificare e risolvere eventuali problemi.
