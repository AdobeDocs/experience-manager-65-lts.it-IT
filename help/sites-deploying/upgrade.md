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
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---

# Aggiornamento a Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>L’aggiornamento ad AEM 6.5 LTS è supportato dagli ultimi 6 Service Pack.

Questa sezione descrive come aggiornare un’installazione di AEM ad AEM 6.5:

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  This was drafted before: * [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

<!--
* [Upgrade Procedure](/help/sites-deploying/upgrade-procedure.md)
* [Upgrading Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Pre-Upgrade Maintenance Tasks](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Performing an In-Place Upgrade](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Sustainable Upgrades](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)

-->

Per un riferimento più semplice alle istanze di AEM coinvolte in queste procedure, in questi articoli vengono utilizzati i termini seguenti:

* L&#39;istanza *source* è l&#39;istanza di AEM da cui si sta eseguendo l&#39;aggiornamento.
* L&#39;istanza *target* è quella a cui si sta eseguendo l&#39;aggiornamento.

## Cosa È Cambiato? {#what-has-changed}

### Aggiornamenti {#updates}

Di seguito sono riportate le principali modifiche da apportare alle ultime versioni di AEM:

1. Il livello Foundation è stato aggiornato per supportare Java 17 (che comprende livelli open source di bundle da Apache Sling, Apache Felix e Apache Jackrabbit Oak)

1. Il pacchetto jar AEM 6.5 LTS ora supporta le API Jarkarta Servlet specifiche 5 e il pacchetto war può essere distribuito nei contenitori servlet che implementano le specifiche API Jakarta Servlet 5/6

1. La confezione di AEM 6.5 LTS uber-jar è cambiata. Per ulteriori informazioni, fare riferimento a [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

### Funzioni/artefatti legacy rimossi {#removed-legacy-features-artifacts}

Le seguenti soluzioni legacy sono state rimosse da AEM 6.5 LTS. Per ulteriori informazioni, fare riferimento a TBD: link to release notes and [List of Obsolete Bundles Uninstallation After the Upgrade](/help/sites-deploying/obsolete-bundles.md) (TBD: collegamento alle note sulla versione e  elenco dei bundle obsoleti disinstallati dopo l&#39;aggiornamento)

1. Social network
1. Commerce
1. Screens
1. We-retail
1. Integrazione di ricerca e promozione

**Artefatti rimossi**

1. CRX-explorer
1. Crx2oak
1. Google guava (rimosso a causa di vulnerabilità di sicurezza)
1. Abdera-parser (rimosso a causa di vulnerabilità di sicurezza)
1. jdom (`org.apache.servicemix.bundles.jdom`) (rimosso a causa di vulnerabilità di sicurezza)
1. `com.github.jknack.handlebars` (rimosso a causa di vulnerabilità di sicurezza)

AEM 6.5 LTS è incentrato sulla compatibilità con le versioni precedenti delle funzioni e viene fornito con uno strumento di analisi. Consulta [Valutazione della complessità dell&#39;aggiornamento con AEM Analyzer](/help/sites-deploying/pattern-detector.md) per la valutazione della complessità quando inizi a pianificare l&#39;aggiornamento. Per ulteriori dettagli sulle altre modifiche, consulta le note sulla versione complete qui. TBD: collegamento alle note sulla versione di AEM 6.5 LTS