---
title: Aggiornamento a Adobe Experience Manager 6.5
description: Scopri le nozioni di base sull’aggiornamento di un’installazione precedente di Adobe Experience Manager (AEM) ad AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 956da2542a958ee6548ede63a7e564f5a4705552
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Aggiornamento a Adobe Experience Manager (AEM) 6.5 {#upgrading-to-aem}

Questa sezione descrive come aggiornare un’installazione di AEM ad AEM 6.5:

* [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md)
* [Valutazione della complessità dell’aggiornamento con il rilevatore pattern](/help/sites-deploying/pattern-detector.md)
* [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md)
* [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Esecuzione di un aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md)
* [Controlli post-aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md)
* [Migrazione dei contenuti differita](/help/sites-deploying/lazy-content-migration.md)

Per un riferimento più semplice alle istanze di AEM coinvolte in queste procedure, in questi articoli vengono utilizzati i termini seguenti:

* L&#39;istanza *source* è l&#39;istanza di AEM da cui si sta eseguendo l&#39;aggiornamento.
* L&#39;istanza *target* è quella a cui si sta eseguendo l&#39;aggiornamento.

## Cosa È Cambiato? {#what-has-changed}

Di seguito sono riportate le principali modifiche da apportare alle ultime versioni di AEM:

AEM 6.0 ha introdotto il nuovo archivio Jackrabbit Oak. I Persistence Manager sono stati sostituiti da [Micro Kernel](/help/sites-deploying/platform.md#contentbody_title_4). A partire dalla versione 6.1, CRX2 non è più supportato. Per migrare gli archivi CRX2 dalle istanze 5.6.1, è necessario eseguire uno strumento di migrazione denominato crx2oak. Per ulteriori informazioni, vedere [Utilizzo dello strumento di migrazione CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Se utilizzi Assets Insights e stai eseguendo l’aggiornamento da una versione precedente a AEM 6.2, è necessario migrare le risorse e generare gli ID tramite un bean JMX. Per i test interni di Adobe, le risorse 125.000 in un ambiente TarMK sono state migrate in un’ora, ma i risultati possono variare.

6.3 ha introdotto un nuovo formato per `SegmentNodeStore`, che è la base dell&#39;implementazione di TarMK. Se esegui l’aggiornamento da una versione precedente a AEM 6.3, è necessaria una migrazione dell’archivio come parte dell’aggiornamento, che comporta tempi di inattività del sistema.

Adobe Engineering stima che siano circa 20 minuti. La reindicizzazione non è necessaria. Inoltre, è stata rilasciata una nuova versione dello strumento crx2oak per l’utilizzo con il nuovo formato di archivio.

**Questa migrazione non è necessaria per l&#39;aggiornamento da AEM 6.3 ad AEM 6.5.**

Le attività di manutenzione pre-aggiornamento sono state ottimizzate per supportare l’automazione.

Le opzioni di utilizzo della riga di comando dello strumento crx2oak sono state modificate per semplificare l’automazione e supportare più percorsi di aggiornamento.

I controlli post-aggiornamento sono stati resi anche più semplici da automatizzare.

La raccolta periodica di oggetti inattivi di revisioni e la raccolta di oggetti inattivi dell’archivio dati sono ora attività di manutenzione ordinaria che devono essere eseguite periodicamente. Con l’introduzione di AEM 6.3, Adobe supporta e consiglia Online Revision Cleanup. Per informazioni su come configurare queste attività, vedere [Pulizia revisioni](/help/sites-deploying/revision-cleanup.md).

AEM ha recentemente introdotto il [rilevatore pattern](/help/sites-deploying/pattern-detector.md) per la valutazione della complessità dell&#39;aggiornamento quando si inizia la pianificazione per l&#39;aggiornamento. La versione 6.5 è inoltre incentrata sulla [compatibilità con le versioni precedenti](/help/sites-deploying/backward-compatibility.md) delle funzionalità. Infine, vengono aggiunte anche le best practice per [aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md).

Per ulteriori dettagli sulle altre modifiche apportate alle versioni recenti di AEM, consulta le note complete sulla versione:

* [Note sulla versione più recente del Service Pack di Adobe Experience Manager 6.5](/help/release-notes/release-notes.md)

## Panoramica dell’aggiornamento {#upgrade-overview}

L’aggiornamento di AEM è un processo con più passaggi, a volte con più mesi. La seguente struttura fornisce una panoramica di ciò che è incluso in un progetto di aggiornamento e del contenuto incluso in questa documentazione:

![schermata_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Flusso di aggiornamento {#upgrade-overview-1}

Il diagramma seguente acquisisce il flusso complessivo consigliato evidenziando l’approccio di aggiornamento. Nota il riferimento alle nuove funzioni introdotte da Adobe. L&#39;aggiornamento deve iniziare con il rilevatore pattern (vedi [Valutazione della complessità dell&#39;aggiornamento con il rilevatore pattern](/help/sites-deploying/pattern-detector.md)), che deve consentire di decidere il percorso da seguire per la compatibilità con AEM 6.4 in base ai pattern nel report generato.

Nella versione 6.5 era stato posto un obiettivo significativo per mantenere tutte le nuove funzioni compatibili con le versioni precedenti, ma nei casi in cui riscontri ancora alcuni problemi di compatibilità con le versioni precedenti, la modalità di compatibilità consente di posticipare temporaneamente lo sviluppo per mantenere il codice personalizzato conforme alla versione 6.5. Questo approccio consente di evitare sforzi di sviluppo subito dopo l&#39;aggiornamento (vedi [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Infine, nel tuo ciclo di sviluppo 6.5, le funzionalità introdotte in Aggiornamenti sostenibili (vedi [Aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md)) ti aiutano a seguire le best practice per rendere gli aggiornamenti futuri ancora più efficienti e fluidi.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
