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
exl-id: ebc34847-dc3d-41ed-b0d6-f004c3debcd9
source-git-commit: 57bf39aa914bddca05d526b46b581579965069d6
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Aggiornamento a Adobe Experience Manager (AEM) 6.5 LTS {#upgrading-to-aem}

>[!NOTE]
>L’aggiornamento ad AEM 6.5 LTS è disponibile per tutti i Service Pack 6.5 supportati.

>[!NOTE]
>
>Da un punto di vista tecnico, il processo di aggiornamento da AEM 6.5 LTS a AEM 6.5 LTS Service Pack è progettato per essere un [aggiornamento sul posto senza soluzione di continuità](/help/sites-deploying/in-place-upgrade.md). Questo processo generalmente non richiede alcuna modifica del codice da parte dei clienti, a meno che non sia specificamente indicato nelle note sulla versione.

Questa sezione descrive come aggiornare un’installazione AEM a AEM 6.5 LTS:

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
-->

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

Foundation Layer ora supporta Java 17 e Java 21, incorporando i bundle open-source più recenti di Apache Sling, Felix e Jackrabbit Oak. Inoltre, è stato modificato il pacchetto di AEM 6.5 LTS uber-jar. Inoltre, alcune funzioni legacy sono state rimosse da AEM 6.5 LTS. Per ulteriori informazioni, consultare le [note sulla versione](/help/release-notes/release-notes.md#whats-new-what-s-new) e [elenco dei bundle obsoleti disinstallati dopo l&#39;aggiornamento](/help/sites-deploying/obsolete-bundles.md)

AEM 6.5 LTS è incentrato sulla compatibilità con le versioni precedenti delle funzioni e viene fornito con uno strumento di analisi. Consulta [Valutazione della complessità dell&#39;aggiornamento con AEM Analyzer](/help/sites-deploying/aem-analyzer.md) per la valutazione della complessità all&#39;avvio della [pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md).
