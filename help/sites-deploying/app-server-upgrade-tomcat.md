---
title: Passaggi per l'aggiornamento delle installazioni di Application Server (Tomcat)
description: Scopri come aggiornare le istanze di AEM distribuite tramite Tomcat.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 7f8de16f-9e9a-4d37-9978-d26c496b911c
source-git-commit: b9b5492b1bf5f717dec6a48ffbe808bf75cbce6a
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Passaggi per l&#39;aggiornamento delle installazioni di Application Server (Tomcat) {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento per AEM 6.5 LTS su Tomcat.

## Passaggi di pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Consulta [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) per ulteriori informazioni. Inoltre, assicurati che il tuo sistema soddisfi i [requisiti per AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md) e consulta le [considerazioni sulla pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md) e in che modo [Analyzer](/help/sites-deploying/aem-analyzer.md) può aiutarti a stimare la complessità.


### Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta**: verificare di aver installato Oracle® JRE 17/21 sul server Tomcat.
* **Server Tomcat**: le versioni supportate del server Tomcat per AEM 6.5 LTS sono **10.0.x** e **10.1.x**.

### Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

Tutti gli esempi in questa procedura utilizzano Tomcat come server applicazioni e indicano che è già stata distribuita una versione funzionante di AEM. La procedura consente di documentare gli aggiornamenti eseguiti dalla versione **6.5** di AEM alla versione **6.5 LTS**.

1. Se AEM 6.5 è già distribuito, verificare che i bundle funzionino correttamente accedendo a: *`https://<serveraddress:port>/system/console/bundles`*
1. Quindi, interrompi AEM 6.5. Questa operazione può essere eseguita da Tomcat App Manager all&#39;indirizzo: *`https://<serveraddress:port>/manager/html`*
1. Assicurati di aver completato le [attività di pre-aggiornamento](#pre-upgrade-steps) come il backup del server AEM 6.5 prima di eseguire qualsiasi attività di aggiornamento
1. Installa Java 17/Java 21 e accertati che sia installato correttamente eseguendo il comando:

   ```
   java –version
   ```

1. Configurare un server Tomcat compatibile con AEM 6.5 LTS
1. Rivedi i parametri di avvio per il server AEM e assicurati di aggiornare i parametri in base ai requisiti di sistema. Consulta [Java 17/Java 21 Considerazioni](/help/sites-deploying/custom-standalone-install.md#java-considerations) per ulteriori informazioni
1. Distribuisci la guerra 6.5 LTS appena scaricata sul server Tomcat utilizzando Java 17/Java 21 e avvia il server AEM 6.5 LTS Tomcat eseguendo:

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Quando AEM è in esecuzione, assicurati che tutti i bundle siano in esecuzione accedendo a: *`https://<serveraddress:port>/cq/system/console/bundles`*
1. Arrestare il server AEM 6.5 LTS Tomcat. Nella maggior parte delle situazioni è possibile eseguire lo script `./catalina.sh` eseguendo il comando dal terminale:

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. È ora possibile migrare i contenuti da AEM 6.5 a AEM 6.5 LTS seguendo la procedura descritta di seguito: [Migrazione dei contenuti da AEM 6.5 a AEM 6.5 LTS tramite Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. Dopo la migrazione del contenuto, applicare le modifiche personalizzate richieste nel file `sling.properties`
1. Avvia il server AEM 6.5 LTS Tomcat eseguendo:

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Monitora i registri di errore all’avvio di AEM per verificare che non vi siano errori e che AEM funzioni senza problemi
1. Una volta avviato AEM 6.5 LTS, verificare che i bundle funzionino correttamente accedendo a: *`https://<serveraddress:port>/cq/system/console/bundles`*

## Distribuisci codebase aggiornata {#deploy-upgraded-codebase}

Una volta completato il processo di aggiornamento, la base di codice aggiornata deve essere distribuita. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM sono disponibili nella [pagina Aggiorna codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

## Eseguire Controlli E Risoluzione Dei Problemi Dopo L&#39;Aggiornamento {#perform-post-upgrade-checks-and-troubleshooting}

Per ulteriori informazioni, vedere [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
