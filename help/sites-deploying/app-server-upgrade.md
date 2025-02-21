---
title: Passaggi per l'aggiornamento delle installazioni di Application Server
description: Scopri come aggiornare le istanze di AEM distribuite tramite Application Server.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 28701105452c347c5470fdb582d783e7aef1adb0
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Passaggi per l&#39;aggiornamento delle installazioni di Application Server {#upgrade-steps-for-application-server-installations}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento per la guerra AEM 6.5 LTS su WLP (WebSphere Liberty).

## Passaggi di pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Consulta [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) per ulteriori informazioni. Inoltre, assicurati che il tuo sistema soddisfi i requisiti per AEM 6.5 LTS. Analizzatore può aiutarti a stimare la complessità dell&#39;aggiornamento e a pianificare l&#39;aggiornamento (consulta [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md) per ulteriori informazioni).

### Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta**: assicurati di aver installato IBM Sumeru JRE 17 sul tuo server WLP.

### Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

1. Esegui un backup dell’istanza prima di avviare qualsiasi attività di aggiornamento.
1. Identificare se è necessario eseguire un aggiornamento sul posto o un aggiornamento secondario a seconda della versione del server WLP in uso. Se il server WLP corrente supporta il Servlet 6, è possibile eseguire l&#39;aggiornamento sul posto e continuare con questa documentazione. In caso contrario, è necessario eseguire un&#39;operazione di livello inferiore. Per il livello secondario, seguire la documentazione di migrazione dei contenuti con aggiornamento Oak - [Collegamento da aggiungere]
1. Arresta l’istanza di AEM. In genere può essere eseguita utilizzando questo comando:

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. Rimuovere i file e le cartelle non più necessari. Gli elementi da rimuovere in modo specifico sono:

   * `cq-quickstart-65.war` dalla cartella `dropins` e dalla cartella espansa si trovano in genere rispettivamente in `<path-to-aem-server>/dropins/cq-quickstart-65.war` e `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`
   * La cartella `launchpad/startup`. È possibile eliminarlo eseguendo il comando seguente nel terminale, supponendo che ci si trovi nella cartella del server:

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * Il file `base.jar`. Per eseguire questa operazione, eseguire i comandi seguenti:

     ```shell
     find crx-quickstart/launchpad -type f -name 
     "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
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
1. Esamina i parametri di avvio per il server AEM e assicurati di aggiornarli in base ai requisiti di sistema. Per ulteriori informazioni, vedere [Installazione autonoma personalizzata](/help/sites-deploying/custom-standalone-install.md)
1. Installa Java 17 e accertati che sia installato correttamente eseguendo:

   ```shell
   java -version
   ```

1. Scarica il nuovo LTS war 6.5 da Software Distribution e copialo nella cartella dei dropin che si trova in: `/<path-to-aem-server>/dropins/`
1. Avvia istanza di AEM: in genere può essere eseguita utilizzando questo comando:

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. Se sono presenti modifiche personalizzate in `sling.properties`, seguire le istruzioni seguenti:

   1. Arrestare l&#39;istanza di AEM eseguendo `<path-to-wlp-directory>/bin/server stop server_name`
   1. Applica le `sling.properties` modifiche personalizzate al file `sling.properties` appena generato (facendo riferimento al file di backup creato al passaggio 6)
   1. Avvia l’istanza di AEM. In genere è possibile eseguirlo eseguendo: `<path-to-wlp-directory>/bin/server start server_name`

## Distribuisci codebase aggiornata {#deploy-upgraded-codebase}

Al termine del processo di aggiornamento sul posto, deve essere distribuita la base di codice aggiornata. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM si trovano nella pagina [Aggiorna codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

## Eseguire Controlli E Risoluzione Dei Problemi Dopo L&#39;Aggiornamento {#perform-post-upgrade-checks-and-troubleshooting}

Per ulteriori informazioni, vedere [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).