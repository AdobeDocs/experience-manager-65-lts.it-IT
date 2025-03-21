---
title: Introduzione alla generazione di rapporti sui processi
description: Introduzione e funzionalità chiave di AEM Forms su JEE Process Reporting
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 755df7e2-3603-4c0d-ad07-ec6f27de8c64
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Introduzione alla generazione di rapporti sui processi{#introduction-to-process-reporting}

![report di processo](assets/process-reporting.png)

Process Reporting è uno strumento basato su browser che consente di creare e visualizzare report sui processi e le attività di AEM Forms.

Report processi fornisce una serie di report predefiniti che consentono di filtrare e visualizzare informazioni sui processi a esecuzione prolungata, sulla durata del processo e sul volume del flusso di lavoro.

Process Reporting fornisce inoltre un&#39;interfaccia per l&#39;esecuzione di query ad hoc e per l&#39;integrazione di visualizzazioni report personalizzate nell&#39;interfaccia utente di Process Reporting.

Per l&#39;elenco dei browser supportati, vedere [Piattaforme supportate da AEM Forms](/help/sites-deploying/technical-requirements.md)

Process Reporting è basato su moduli che:

* Leggi dati processo da AEM Forms Database
* Pubblicare i dati del processo in un repository Process Reporting incorporato
* Fornisce un&#39;interfaccia utente basata su browser per visualizzare i rapporti

## Funzionalità principali {#key-capabilities}

### Reporting sempre attivo {#always-on-reporting}

![gestione del sito](assets/site-management.png)

Visualizzare l&#39;elenco dei processi con tempi di esecuzione lunghi, elaborare grafici della durata ed eseguire query personalizzate utilizzando i filtri.

Process Reporting offre inoltre la possibilità di esportare il report ed eseguire query sui dati in formato CSV.

### Rapporti ad hoc {#adhoc-reports}

![stampa e colori](assets/print-&-colour.png)

Utilizza i filtri per ottenere una visualizzazione specifica dei dati.

È possibile cercare i processi o le attività in base all&#39;ID, alla durata, alle date di inizio e di fine, all&#39;iniziatore del processo e così via.

Puoi combinare più filtri per creare rapporti specifici.

Puoi quindi salvare i filtri del rapporto in modo che vengano eseguiti in una data o in un’ora successiva.

### Cronologia processi/attività {#process-task-history}

![gestione file](assets/file-management.png)

I server AEM Forms eseguono numerosi processi in parallelo. Questi processi continuano a passare da uno stato all’altro. Pubblicando i dati di Forms nel repository di Process Reporting a intervalli regolari, Process Reporting conserva le informazioni di transizione sui processi in esecuzione in AEM Forms.

### Controllo accesso {#access-control-br}

![senza titolo](assets/untitled.png)

Process Reporting fornisce un accesso basato su autorizzazioni all&#39;interfaccia utente.

Ciò significa che solo gli utenti con autorizzazioni di reporting hanno accesso all’interfaccia utente di Process Reporting.
