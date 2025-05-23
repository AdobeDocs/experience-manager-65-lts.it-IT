---
title: Architettura di AEM Forms Workspace
description: Informazioni concettuali e panoramica dell’architettura dell’area di lavoro di AEM Forms LiveCycle.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: d317274f-2c9a-4809-b43e-2efebc8fcb3f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Architettura di AEM Forms Workspace {#aem-forms-workspace-architecture}

AEM Forms Workspace è un’applicazione web ospitata su CRX™. Quando l’area di lavoro viene aperta in un browser, si accede a una risorsa CRX e l’applicazione viene riprodotta come pagina HTML nel browser.

L’applicazione accede al server AEM Forms sugli endpoint REST per eseguire le seguenti operazioni:

* Recupera le attività utente, i punti d&#39;inizio processo, la cronologia processo e le informazioni utente
* Eseguire azioni sulle attività
* Eseguire query sulle attività nel database
* Aggiornare le preferenze utente e altro ancora

Il server AEM Forms accede al database di AEM Forms tramite JDBC. Il database consente di salvare in modo permanente le attività, i processi e le relative istanze, gli utenti e le informazioni correlate.

L’area di lavoro di AEM Forms è progettata in componenti modulari JavaScript™ che possono essere personalizzati individualmente e riutilizzati in altre applicazioni web. I componenti sono basati su BackBone, una libreria JavaScript che dà struttura alle applicazioni web. Un articolo dettagliato che descrive l&#39;interazione dei componenti con BackBone è [qui](/help/forms/using/backbone-interaction.md). L&#39;organizzazione dei componenti nella struttura di cartelle di CRX è descritta in [questo](/help/forms/using/folder-structure.md) articolo.

Pacchetti consegnati per l’area di lavoro di AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: è un pacchetto CRX, ovvero può essere distribuito in CRX utilizzando Gestione pacchetti.
* `adobe-lc-workspace-<version>-src.zip`: è un archivio che contiene il codice completo dell&#39;area di lavoro AEM Forms e gli script per la creazione dei pacchetti di distribuzione: spedizione, debug e sviluppo.
