---
title: Utilizzare i flussi di lavoro
description: I flussi di lavoro in Adobe Experience Manager consentono di automatizzare una serie di passaggi eseguiti su una pagina o una risorsa.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Architect,Developer
exl-id: 55382f3d-7aa4-433f-ac0c-c4764c01a8c3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 74%

---

# Utilizzare i flussi di lavoro{#working-with-workflows}

I flussi di lavoro di AEM consentono di automatizzare una serie di passaggi eseguiti su (una o più) pagine e/o risorse.

Ad esempio, per la pubblicazione, un editor deve rivedere il contenuto prima che l’amministratore del sito attivi la pagina. Un flusso di lavoro che automatizza questo esempio avvisa ogni partecipante quando è il momento di eseguire il lavoro richiesto:

1. L’autore applica il flusso di lavoro alla pagina.
1. L’editor riceve un elemento di lavoro che indica che è necessario rivedere il contenuto della pagina. Al termine, sarà indicato che l’elemento di lavoro è stato completato.
1. L’amministratore del sito riceve quindi una richiesta di lavoro per l’attivazione della pagina. Al termine, sarà indicato che l’elemento di lavoro è stato completato.

In genere:

* Gli autori dei contenuti applicano i flussi di lavoro alle pagine e partecipano ai flussi di lavoro.
* I flussi di lavoro utilizzati sono specifici per i processi aziendali dell’organizzazione.

Le pagine seguenti trattano:

* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
* [Partecipazione ai flussi di lavoro](/help/sites-authoring/workflows-participating.md)
