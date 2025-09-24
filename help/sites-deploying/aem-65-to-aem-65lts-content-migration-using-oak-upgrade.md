---
title: Migrazione dei contenuti da AEM 6.5 ad AEM 6.5 LTS tramite l’aggiornamento ad Oak
description: Scopri come migrare i contenuti da AEM 6.5 a AEM 6.5 LTS utilizzando lo strumento oak-upgrade
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
source-git-commit: 69033442fda82d9efdd1ba2f55a45173c8ffc6ec
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Migrazione dei contenuti da AEM 6.5 ad AEM 6.5 LTS tramite l’aggiornamento ad Oak {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

Questo documento fornisce una guida completa per l&#39;aggiornamento di Adobe Experience Manager dalla versione **6.5** alla versione **6.5 LTS**, concentrandosi sulla migrazione dell&#39;archivio dei contenuti tramite lo strumento oak-upgrade, una potente utility per il trasferimento dei contenuti tra archivi diversi con precisione e controllo.

## Prerequisiti {#prerequisites}

Prima di avviare la migrazione, verifica che siano soddisfatti i seguenti requisiti:

1. Compatibilità Java: AEM 6.5 LTS deve essere installato e configurato per l’esecuzione con Java™ 17. Una volta configurata, avvia l’istanza di AEM e verifica che tutti i bundle siano attivi e funzionanti senza problemi
1. Risorse di sistema: garantire spazio su disco e memoria sufficienti per gestire entrambi gli archivi durante il processo di migrazione
1. Strumento di aggiornamento Oak: scarica il file jar `oak-upgrade` dall&#39;[archivio Maven ufficiale](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade). Assicurati che la versione corrisponda a quella oak-core utilizzata in AEM 6.5 LTS. Lo strumento di aggiornamento di Oak viene eseguito su Oracle® Java™ 11 o versione successiva

## Processo di migrazione passo dopo passo {#step-by-step-migration-process}

### Interruzione di AEM 6.5 e AEM 6.5 LTS {#stopping-aem65-and-aem65lts}

Prima di avviare la migrazione, arresta le istanze AEM 6.5 e AEM 6.5 LTS. In questo modo l’archivio sarà in uno stato stabile e non si verificheranno scritture aggiuntive durante la migrazione.

### Backup dell’istanza di AEM 6.5 {#backing-up-the-aem65-instance}

Esegui un backup completo dell’istanza di AEM 6.5 se non lo hai già fatto.

### Utilizzo dello strumento di aggiornamento di Oak per la migrazione dei contenuti {#using-the-oak-upgrade-tool-for-content-migration}

Lo strumento Oak-Upgrade viene eseguito tramite la riga di comando, come illustrato di seguito:

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

Di seguito sono riportati i comandi e le opzioni essenziali:

**Opzioni chiave**

* `--include-paths`: specificare le sottostrutture da includere nella migrazione. Per informazioni sull&#39;utilizzo del comando, vedere questo esempio:

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`: escludi percorsi specifici dalla migrazione. Presta attenzione quando utilizzi questa opzione: se il percorso esiste sul sistema di destinazione, verrà rimosso. Per informazioni sull&#39;utilizzo del comando, vedere questo esempio:

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`: per impostazione predefinita, oak-upgrade migra solo i riferimenti ai file binari, lasciando i file effettivi nell&#39;archivio BLOB/dati originale. Di conseguenza, il nuovo archivio si basa ancora sull’archivio di origine per i file binari. Per eseguire la migrazione dei dati binari insieme al contenuto dell&#39;archivio, utilizzare il parametro `--copy-binaries` per copiare tutti i dati binari nel nuovo archivio, come illustrato di seguito:

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### Migrazione dei checkpoint {#migratiing-checkpoints}

Durante la migrazione di un vecchio archivio SegmentMK (precedente ad Oak 1.6) a un nuovo SegmentMK (versione Oak successiva o uguale a 1.6), viene eseguita anche la migrazione dei punti di controllo. Questo consente di evitare la reindicizzazione quando Oak viene eseguito per la prima volta sul nuovo archivio. Tuttavia, la migrazione dei punti di controllo non verrà eseguita nei casi seguenti:

1. Sono specificati percorsi di inclusione, esclusione o unione personalizzati oppure
1. I binari vengono copiati dai riferimenti, non viene specificato alcun datastore di origine e due punti di controllo diversi contengono un binario diverso nello stesso percorso.

Nel secondo caso, oak-upgrade genera l’avviso e le interruzioni seguenti:

```
Checkpoints won't be copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

Il modo più semplice per risolvere il problema è specificare l&#39;archivio dati di origine nelle opzioni della riga di comando (ad esempio `--src-datastore` o `--src-s3datastore`).

Anche l’avviso può essere ignorato, ma in questo caso l’archivio verrà reindicizzato completamente al primo avvio. Può essere un processo lungo, soprattutto per la grande istanza. L’archivio non sarà utilizzabile fino al completamento del processo di reindicizzazione. Utilizzare l&#39;opzione `--skip-checkpoints` per eliminare l&#39;avviso.

È inoltre possibile reindicizzare offline l&#39;archivio prima di avviare AEM utilizzando [reindicizzazione offline](/help/sites-deploying/offline-reindexing.md) per evitare la reindicizzazione completa al primo avvio.

Per ulteriori informazioni sullo strumento oak-upgrade e sull&#39;utilizzo avanzato, consulta la [documentazione ufficiale](https://jackrabbit.apache.org/oak/docs/migration.html).
