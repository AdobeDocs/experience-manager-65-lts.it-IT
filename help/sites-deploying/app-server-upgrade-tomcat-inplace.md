---
title: Passaggi per l'aggiornamento delle installazioni di Application Server (Tomcat)
description: Scopri come aggiornare le istanze di AEM distribuite tramite Tomcat.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b3c4e946a3f235fa0e3a0945f1ad692ee195e3ef
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Passaggi per l&#39;aggiornamento delle installazioni di Application Server (Tomcat - Aggiornamento sul posto) {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento (aggiornamento locale) da AEM 6.5 LTS a AEM 6.5 LTS Servicepack su Tomcat. Per l&#39;aggiornamento da AEM 6.5 a 6.5 LTS, [fai riferimento qui](/help/sites-deploying/app-server-upgrade-tomcat.md).

## Passaggi di pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Consulta [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) per ulteriori informazioni. Inoltre, assicurati che il tuo sistema soddisfi i [requisiti per AEM 6.5 LTS Servicepack](/help/sites-deploying/technical-requirements.md) e consulta [considerazioni sulla pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md).


### Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta**: verificare di aver installato Oracle® JRE 17/21 sul server Tomcat.
* **Server Tomcat**: le versioni supportate del server Tomcat per AEM 6.5 LTS e i relativi ServicePack sono **10.0.x** e **10.1.x**.

### Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

Tutti gli esempi in questa procedura utilizzano Tomcat come server applicazioni e implicano che è già stata distribuita una versione funzionante di AEM 6.5 LTS. La procedura consente di documentare gli aggiornamenti eseguiti dalla versione **6.5** LTS di AEM alla versione **6.5 LTS** Servicepack.

1. Se AEM 6.5 LTS è già distribuito, verificare che i bundle funzionino correttamente accedendo a: *`https://<serveraddress:port>/system/console/bundles`*
1. Quindi, arrestare AEM 6.5 LTS. Questa operazione può essere eseguita da Tomcat App Manager all&#39;indirizzo: *`https://<serveraddress:port>/manager/html`*
1. Assicurati di aver completato le [attività di pre-aggiornamento](#pre-upgrade-steps) come il backup del server AEM 6.5 LTS prima di eseguire qualsiasi attività di aggiornamento
1. Arrestare il server AEM 6.5 LTS Tomcat. Nella maggior parte delle situazioni è possibile eseguire lo script `./catalina.sh` eseguendo il comando dal terminale:

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. Rimuovere i file e le cartelle non più necessari. Gli elementi da rimuovere in modo specifico sono:

   * Il file **cq-quickstart-65.war** e la cartella `cq-quickstart-65` della cartella `webapps` si trovano in genere in `<path-to-aem-server>/webapps`
   * La cartella `launchpad/startup`. È possibile eliminarlo eseguendo il comando seguente nel terminale, supponendo che ci si trovi nella cartella del server:

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * Il file `base.jar`. Per eseguire questa operazione, eseguire i comandi seguenti:

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * Il file `BootstrapCommandFile_timestamp.txt`:

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * Rimuovere il file `sling.options` eseguendo:

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * Rimuovi il file `sling.bootstrap.txt`:

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. Creare un backup del file `sling.properties` (in genere presente in `<path-to-aem-server>/bin/crx-quickstart/launchpad/`) ed eliminarlo
1. Copia il file .war del servicepack AEM 6.5 LTS nella cartella `<path-to-aem-server>/webapps`
1. Avvia il server AEM 6.5 LTS Tomcat eseguendo:

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Monitora i registri di errore all’avvio di AEM per verificare che non vi siano errori e che AEM funzioni senza problemi
1. Una volta avviato AEM 6.5 LTS, verificare che i bundle funzionino correttamente accedendo a: *`https://<serveraddress:port>/cq/system/console/bundles`*

## Eseguire Controlli E Risoluzione Dei Problemi Dopo L&#39;Aggiornamento {#perform-post-upgrade-checks-and-troubleshooting}

Per ulteriori informazioni, vedere [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
