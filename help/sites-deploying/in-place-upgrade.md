---
title: Esecuzione di un aggiornamento sul posto
description: Scopri come eseguire un aggiornamento sul posto per AEM 6.5 LTS.
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c7351625-b29e-45a7-b966-e7c0f56d4f22
source-git-commit: db9bf14ec9fefcbafb7b6d749de966e97c54abda
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Esecuzione di un aggiornamento sul posto {#performing-an-in-place-upgrade}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento sul posto per AEM 6.5 LTS. Se si dispone di un&#39;installazione distribuita in un server applicazioni, vedere [Passaggi per l&#39;aggiornamento delle installazioni del server applicazioni](/help/sites-deploying/app-server-upgrade.md).

## Passaggi di pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Consulta [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) per ulteriori informazioni. Inoltre, assicurati che il tuo sistema soddisfi i [requisiti per AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md) e consulta le [considerazioni sulla pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md) e come [Analyzer](/help/sites-deploying/pattern-detector.md) può aiutarti a stimare la complessità.

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta:** Verifica che Oracle Java™ 17 sia installato nel sistema.

## Preparazione del file jar Quickstart di AEM {#prep-quickstart-file}

1. Scarica il nuovo file jar AEM 6.5 LTS

1. [Determinare il comando di avvio dell&#39;aggiornamento corretto](#determining-the-correct-upgrade-start-command)

1. Arresta l’istanza se è in esecuzione

1. Utilizza il nuovo file jar AEM 6.5 LTS per sostituire il vecchio all&#39;esterno della cartella `crx-quickstart`

1. Esegui una copia di backup del file `sling.properties` (in genere presente in `crx-quickstart/conf/`), quindi eliminalo

1. Decomprimi il nuovo file jar quickstart eseguendo:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

1. Il comando unpack genererà un nuovo file `sling.properties` nella cartella `crx-quickstart/conf/`. Ora puoi applicare le modifiche personalizzate al file `sling.properties` appena generato.

<!-- Alexandru: drafting temporarily

## Content Repository Migration {#content-repository-migration}

This migration is not required if you are upgrading from AEM 6.3. For versions older than 6.3, Adobe provides a tool that can be used to migrate the repository to the new version of the Oak Segment Tar present in AEM 6.3. It is provided as part of the quickstart package and is mandatory for any upgrades that will be using TarMK. Upgrades for environments that are using MongoMK do not require repository migration. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool to simplify the upgrade and make it more robust.

>[!NOTE]
>
>If you are performing TarMK repository content migration using the CRX2Oak Quickstart extension, you might remove the **samplecontent** runmode by adding the following to the migration command line:
>
>* `--promote-runmode nosamplecontent`
>

To determine the command that you should run, use the following command:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>Source Repository</strong></td>
   <td><strong>Target Repository</strong></td>
   <td><strong>Profile</strong></td>
   <td><strong>Additional Flags</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 or TarMK with <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK or crx2 with <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>TarMK with no datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No migration is needed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Where:**

* `mongo-host` is the MongoDB server IP (for example, 127.0.0.1)

* `mongo-port` is the MongoDB server port (for example: 27017)

* `mongo-database-name` represents the name of the database (for example: aem-author)

**You may also require additional switches for the following scenarios:**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, add the `--disable-mmap` parameter to the command.

For additional instructions on using the crx2oak tool, see Using the [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). The crx2oak helper JAR can be manually upgraded if needed, by manually replacing it with newer versions after unpacking the quickstart. Its location in the AEM installation folder is: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. The newest version of the CRX2Oak migration tool is available for download from the Adobe Repository at: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

If the migration has completed successfully, the tool will exit with an exit code of zero. Additionally, check for WARN and ERROR messages in the `upgrade.log` file, located under `crx-quickstart/logs` in the AEM installation directory, as these could indicate non-fatal errors that occurred during the migration.

Check the configuration files beneath `crx-quickstart/install` folder. If a migration was necessary these will be updated to reflect the target repository.

**A note on datastores:**

While `FileDataStore` is the new default for AEM 6.3 installations, using an external datastore is not required. While using an external datastore is recommended as a best practice for production deployments, it is not a prerequisite to upgrade. Due to the complexity already present in upgrading AEM, Adobe recommends performing the upgrade without doing a datastore migration. If desired, a datastore migration can be executed afterwards as a separate effort.

## Troubleshooting Migration Issues {#troubleshooting-migration-issues}

Skip this section if you are upgrading from 6.3. While the provided crx2oak profiles should meet the needs of most customers, there are times when additional parameters will be necessary. If you run into an error during your migration, it is possible that there are aspects of your environment that require additional configuration options to be provided. If so, you will likely encounter the following error:

**Checkpoints are not copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

For some reason, the migration process needs access to binaries in the datastore and is unable to find it. To specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**For S3 datastores:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**For File datastores:**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

-->

## Esecuzione Dell&#39;Aggiornamento {#performing-the-upgrade}

**Se si utilizza S3:**

1. Rimuovi eventuali file jar al di sotto di `crx-quickstart/install` associati a una versione precedente del connettore S3.

1. Scarica la versione più recente del connettore S3 1.60.2 da [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) <!-- Alexandru: this is a stub link for now -->

1. Estrarre il connettore S3 (versione 1.60.2) e copiare il contenuto delle cartelle seguenti in `crx-quickstart/install`, come segue:

   1. Copia `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/1` in `crx-quickstart/install/1`
   1. Copia `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/15` in `crx-quickstart/install/15`

Ora, avvia l&#39;istanza di AEM utilizzando il nuovo comando determinato utilizzando le informazioni nella sezione [Determinazione del comando di avvio dell&#39;aggiornamento corretto](#determining-the-correct-upgrade-start-command).

### Determinazione del comando di avvio dell&#39;aggiornamento corretto {#determining-the-correct-upgrade-start-command}

>[!NOTE]
>
>Il supporto per alcuni degli argomenti di Java 8/11 è stato rimosso in Java 17. Vedere [documenti di Oracle Java™ 17](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html) e [considerazioni sugli argomenti di Java&amp;trade per AEM 6.5 LTS](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations).

Per eseguire l’aggiornamento, è importante avviare AEM utilizzando il file jar per visualizzare l’istanza.

L’avvio di AEM dallo script di avvio non avvierà l’aggiornamento. La maggior parte dei clienti avvia AEM utilizzando lo script di avvio e ha personalizzato questo script di avvio in modo da includere gli switch per le configurazioni dell’ambiente, ad esempio le impostazioni di memoria, i certificati di sicurezza e così via. Per questo motivo, Adobe consiglia di seguire questa procedura per determinare il comando di aggiornamento corretto:

1. In un’istanza di AEM in esecuzione, esegui quanto segue dalla riga di comando:

   ```shell
   ps -ef | grep java
   ```

1. Cerca il processo AEM. Avrà un aspetto simile a:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modificare il comando sostituendo il percorso del file jar esistente ( `crx-quickstart/app/aem-quickstart*.jar` in questo caso) con il nuovo file jar AEM 6.5 LTS di pari livello della cartella `crx-quickstart`. Utilizzando il comando precedente come esempio, il comando sarà:

   ```shell
   /usr/bin/java -server -Xmx4096m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar <AEM-6.5-LTS.jar> -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   In questo modo, per l’aggiornamento verranno applicate tutte le impostazioni di memoria appropriate, le modalità di esecuzione personalizzate e altri parametri ambientali. Al termine dell’aggiornamento, l’istanza può essere avviata dallo script di avvio alle avviazioni future.

## Distribuisci codebase aggiornata {#deploy-upgraded-codebase}

Al termine del processo di aggiornamento sul posto, deve essere distribuita la base di codice aggiornata. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM sono disponibili nella [pagina Aggiorna codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

## Eseguire controlli post-aggiornamento e risoluzione dei problemi {#perform-post-upgrade-check-troubleshooting}

Consulta [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
