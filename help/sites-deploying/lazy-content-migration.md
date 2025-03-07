---
title: Migrazione dei contenuti differita
description: Scopri la migrazione dei contenuti Lazy in Adobe Experience Manager 6.4.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: 78c5486c-ed84-4ec8-b0b0-42d4e8611098
source-git-commit: 09d2e75729060135f9eff1fc9f0126b0f940310b
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 2%

---

# Migrazione dei contenuti differita {#lazy-content-migration}

Per motivi di compatibilità con le versioni precedenti, il contenuto e la configurazione in **/etc** e **/content** a partire da Adobe Experience Manager (AEM) 6.3 non verranno toccati o trasformati immediatamente con l&#39;aggiornamento. Questo viene fatto per garantire che le dipendenze delle applicazioni del cliente da tali strutture rimangano intatte. La funzionalità relativa a queste strutture di contenuto è ancora la stessa anche se il contenuto in un’istanza predefinita di AEM 6.5 sarebbe ospitato in un’altra posizione.

Anche se non tutte queste posizioni possono essere trasformate automaticamente, alcune `CodeUpgradeTasks` posticipate sono anche denominate Migrazione dei contenuti lenti. Questo consente ai clienti di attivare tali trasformazioni automatiche riavviando l’istanza con questa proprietà di sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Questo causa l&#39;esecuzione di `CodeUpgradeTasks` durante la migrazione.

Anche se l’obiettivo è un’esecuzione efficiente, questo processo di aggiornamento è sincrono e quindi comporta un tempo di inattività a seconda della quantità di contenuto da elaborare. Adobe consiglia di valutare i tempi di esecuzione in un ambiente stage prima di un sistema di produzione per pianificare un intervallo di manutenzione appropriato.

Poiché questo in genere richiede anche la regolazione dell’applicazione, questa attività deve essere eseguita insieme alla distribuzione dell’applicazione corrispondente.

Di seguito è riportato l&#39;elenco completo di `CodeUpgradeTasks` introdotti in 6.5:

| **Nome** | **Rilevante** **per le versioni di AEM precedenti** | **Migrazione** **Tipo** | **Dettagli** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6,0 | Immediato | Rileva tutti i `LiveRelationShips` da `VersionStorage` che sono stati eliminati e aggiunge la proprietà di esclusione all&#39;elemento padre |
| `Cq61CloudServicesContentUpgrade` | &lt; 6,1 | Immediato | Ristruttura i servizi cloud per la sicurezza per impostazione predefinita |
| `Cq62ConfContentUpgrade` | &lt; 6,2 | Immediato | Rimuove il collegamento basato su proprietà da **/content** a **/conf** (sostituito dal meccanismo OSGi), genera la configurazione OSGi corrispondente |
| `Cq62FormsContentUpgrade` | &lt; 6,2 | Immediato | A causa della gestione di merge_preserve, la regola di negazione sicura per impostazione predefinita sostituisce le autorizzazioni specificate, rendendo necessario il riordinamento al momento dell’aggiornamento |
| `CQ62Html5SmartFileUpgrade` | &lt; 6,2 | Immediato | Rileva i componenti utilizzando il widget Html5SmartFile, cerca gli utilizzi del componente nel contenuto e ripristina la persistenza, spostando efficacemente il binario di un livello inferiore e non memorizzandolo a livello di componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6,2 | Immediato | Sposta i vecchi progetti di stile da **/etc/projects** a **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6,2 | Immediato | Introduce un livello contenitore nella gerarchia (Aree) e regola i riferimenti. |
| `Cq62TargetContentUpgrade` | &lt; 6,2 | Immediato | Imposta i nomi delle posizioni fisse per i componenti di destinazione. |
| `Cq62WorkflowContentUpgrade` | &lt; 6,2 | Immediato | Trasformazione complessa di modelli di flusso di lavoro precedenti alla versione 6.2 di strutture, istanze, notifiche, con successiva unione dal percorso di backup da **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6,3 | Immediato | Sposta le risorse, gli schemi di metadati personalizzati e i profili di elaborazione da **/apps** a **/conf** e traduce i moduli di schema metadati e profili metadati da coral2 a coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6,3 | Immediato | Sposta le risorse e i facet di ricerca personalizzati da **/apps** a **/conf** e traduce i moduli schema metadati e profili metadati da coral2 a coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6,3 | Immediato | Aggiorna Posta in arrivoElementi per l&#39;ordinamento degli elementi della casella in entrata (regolazione dei metadati per un ordinamento efficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6,3 | Immediato | Regola la proprietà metadataSchema nella cartella sostituendo i percorsi relativi a **/conf** al posto di **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6,3 | Immediato | Regolazione della struttura di navigazione |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6,3 | Immediato | Sposta le configurazioni personalizzate per i dashboard di monitoraggio da **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6,3 | Immediato | Traduce la proprietà processingProfile (utilizzata fino alla versione 6.1) in Assets per corrispondere alla struttura della versione 6.3 e successive. Inoltre regola i percorsi relativi del profilo a **/conf** al posto di **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6,3 | Immediato | Attività di aggiornamento che rimuove le voci di menu obsolete di CRXDE Lite e Console Web in caso di aggiornamento. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6,3 | Ritardato | Spostando le configurazioni cloud SRP, le configurazioni delle parole chiave della community, si puliscono **/etc/social** e **/etc/enablement** (è necessario regolare riferimenti e dati durante l&#39;esecuzione della migrazione lenta: nessuna parte dell&#39;applicazione deve più dipendere da questa struttura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6,4 | Ritardato | Pulisce **/etc/cloudsettings** (contenente la configurazione ContextHub). La configurazione viene migrata automaticamente al primo accesso. Nel caso in cui la migrazione dei contenuti lazy venga avviata insieme all&#39;aggiornamento, questi contenuti in **/etc/cloudsettings** devono essere conservati tramite pacchetto prima dell&#39;aggiornamento e reinstallati per consentire l&#39;avvio della trasformazione implicita, insieme a una successiva disinstallazione del pacchetto dopo il completamento. |
| `CQ64UsersTitleFixTask` | &lt; 6,4 | Ritardato | Regola la struttura del titolo legacy al titolo nel nodo del profilo utente. |
| `CQ64CommerceMigrationTask` | &lt; 6,4 | Ritardato | Migra il contenuto commerce da **/etc/commerce** a **/var/commerce**. Durante la migrazione il contenuto viene spostato e i riferimenti al contenuto spostato vengono aggiornati per riflettere la nuova posizione. |
| `CQ65DMMigrationTask` | &lt; 6,5 | Ritardato | Migra le impostazioni del catalogo legacy e le impostazioni dei servizi cloud Dynamic Media da **/etc** a **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Ritardato | Pulisci clientlibs legacy esistenti in **/etc/clientlibs** |
