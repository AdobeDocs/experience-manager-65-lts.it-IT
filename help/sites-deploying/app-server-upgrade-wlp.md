---
title: Passaggi per l'aggiornamento delle installazioni di Application Server (WLP)
description: Scopri come aggiornare le istanze di AEM distribuite tramite WebSphere Liberty.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 2a5d9026-49bc-4766-bcbe-38d834c14f72
source-git-commit: e5acea11254a6c4dbd24ff2a6d8ae3578b6690da
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Passaggi per l&#39;aggiornamento delle installazioni di Application Server (WLP) {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento per AEM 6.5 LTS su WLP (WebSphere® Liberty).

## Passaggi di pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Consulta [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) per ulteriori informazioni. Inoltre, assicurati che il tuo sistema soddisfi i [requisiti per AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

Controlla [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md) e come [AEM Analyzer](/help/sites-deploying/aem-analyzer.md) può aiutarti a stimare la complessità dell&#39;aggiornamento di AEM.

### Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta**: assicurati di aver installato IBM® Sumeru JRE 17/21 sul tuo server WLP.

### Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

1. Assicurati di aver completato i [passaggi precedenti all&#39;aggiornamento](#pre-upgrade-steps) come il backup del server AEM 6.5 prima di eseguire qualsiasi attività di aggiornamento
1. A seconda delle esigenze, scegli uno dei seguenti percorsi di aggiornamento:
   1. **Aggiornamento sul posto**: se il server WLP corrente supporta il Servlet 6, è possibile eseguire un aggiornamento sul posto e continuare con il passaggio 3.
   1. **Sidegrade**: se preferisci una nuova configurazione o se il server WLP non supporta il Servlet 6, configura una nuova istanza WLP con AEM 6.5 LTS e migra il contenuto seguendo la [guida AEM 6.5 in AEM 6.5 LTS Content Migration Using Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md) e passa alla [sezione Deploy Upgraded Codebase](#deploy-upgraded-codebase)

1. Arresta l’istanza di AEM. In genere può essere eseguita utilizzando questo comando:

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. Rimuovere i file e le cartelle non più necessari. Gli elementi da rimuovere in modo specifico sono:

   * La cartella **cq-quickstart-65.war** dalla cartella `dropins` e la cartella `expanded` si trovano rispettivamente in `<path-to-aem-server>/dropins/cq-quickstart-65.war` e `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`
   * La cartella `launchpad/startup`. È possibile eliminarlo eseguendo il comando seguente nel terminale, supponendo che ci si trovi nella cartella del server:

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * Il file `base.jar`. Per eseguire questa operazione, eseguire i comandi seguenti:

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * Il file `BootstrapCommandFile_timestamp.txt`:

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * Rimuovere il file `sling.options` eseguendo:

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * Rimuovi il file `sling.bootstrap.txt`:

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. Creare un backup del file `sling.properties` (in genere presente in `crx-quickstart/conf/`) ed eliminarlo
1. Cambia la versione del servlet in **6.0** nel file `server.xml`
1. Installa Java 17/Java 21 e assicurati che sia installato correttamente eseguendo:

   ```shell
   java -version
   ```

1. Esamina i parametri di avvio per il server AEM e assicurati di aggiornarli in base alle tue esigenze. Per ulteriori informazioni, vedere [Java 17/Java 21 Considerazioni](/help/sites-deploying/custom-standalone-install.md#java-considerations).
1. Scarica il nuovo file .war 6.5 LTS e copialo nella cartella dei dropin che si trova in: `/<path-to-aem-server>/dropins/`
1. Avvia istanza di AEM: in genere può essere eseguita utilizzando questo comando:

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. Se sono presenti modifiche personalizzate in `sling.properties`, seguire le istruzioni seguenti:

   1. Arrestare l&#39;istanza di AEM eseguendo `<path-to-wlp-directory>/bin/server stop server_name`
   1. Applica le `sling.properties` modifiche personalizzate al file `sling.properties` appena generato (facendo riferimento al file di backup creato al passaggio 5)
   1. Avvia l’istanza di AEM. In genere è possibile eseguirlo eseguendo: `<path-to-wlp-directory>/bin/server start server_name`

## Distribuisci codebase aggiornata {#deploy-upgraded-codebase}

Una volta completato il processo di aggiornamento, la base di codice aggiornata deve essere distribuita. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM sono disponibili nella [pagina Aggiorna codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

## Eseguire Controlli E Risoluzione Dei Problemi Dopo L&#39;Aggiornamento {#perform-post-upgrade-checks-and-troubleshooting}

Consulta [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
