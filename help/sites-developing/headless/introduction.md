---
title: Sviluppo headless per siti AEM 6.5
description: Scopri come le potenti funzionalità headless di AEM 6.5, come i modelli di contenuto, i frammenti di contenuto e l’API GraphQL, collaborano per gestire le esperienze a livello centrale e distribuirle tra i canali.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: 4eb42d3a-f869-4831-9aaf-58e7272bd1fe
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 32%

---

# Sviluppo headless per siti AEM 6.5 {#headless-development}

Scopri come le potenti funzionalità headless di AEM 6.5, come i modelli di contenuto, i frammenti di contenuto e l’API GraphQL, collaborano per gestire le esperienze a livello centrale e distribuirle tra i canali.

## Panoramica {#overview}

L’implementazione headless diventa sempre più importante per offrire esperienze al pubblico, ovunque si trovi e indipendentemente dal canale.

L’implementazione headless ignora la gestione di pagine e componenti come avviene nelle soluzioni complete e ibride e si concentra sulla creazione di frammenti di contenuto riutilizzabili e indipendenti dal canale, che possono essere distribuiti in modalità cross-channel. Si tratta di un modello di sviluppo moderno e dinamico per l’implementazione di esperienze web.

![Modelli di implementazione di AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Confronto tra headful e headless {#headful-headless}

Questo documento si concentra sul modello completo di implementazione headless di AEM. Tuttavia, headful e headless non devono essere necessariamente una scelta binaria in AEM. Le funzioni headless consentono di gestire e distribuire i contenuti a diversi endpoint, consentendo agli autori dei contenuti di modificare le applicazioni a pagina singola. Tutto questo direttametne in AEM.

>[!TIP]
>
>Per saperne di più, consulta il documento [Headful e headless in AEM](/help/sites-developing/headful-headless.md).

## AEM 6.5 e headless {#aem-headless}

AEM 6.5 è uno strumento flessibile per il modello di implementazione headless che offre tre potenti servizi:

1. Modelli di contenuto
   * I modelli di contenuto sono rappresentazioni strutturate di contenuti.
   * Questi vengono definiti dagli architetti di informazioni nell’editor di modelli per frammenti di contenuto di AEM.
   * I modelli di contenuto fungono da base per i frammenti di contenuto.
1. Frammenti di contenuto
   * I frammenti di contenuto sono istanze di modelli di contenuto.
   * Vengono creati dagli autori di contenuti tramite l’editor di frammenti di contenuto di AEM.
   * Vengono memorizzati in AEM Assets e gestiti nell’interfaccia utente di amministrazione di Assets.
1. API per la distribuzione dei contenuti
   * L’API GraphQL di AEM supporta la distribuzione di frammenti di contenuto.
   * L’API REST di AEM Assets supporta le operazioni CRUD relative ai frammenti di contenuto.
   * La distribuzione diretta dei contenuti è possibile anche con l&#39;esportazione JSON del componente core Frammento di contenuto [.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it)

## Primi passi con AEM headless {#first-steps}

Sono disponibili diverse risorse per iniziare a utilizzare le funzioni headless di AEM. Sono destinati a casi d’uso diversi, ma forniscono tutti una panoramica delle funzioni headless di AEM.

| Risorsa | Descrizione | Tipo | Pubblico | Tempo stimato |
|---|---|---|---|---|
| [Percorso per sviluppatori headless](/help/journey-headless/developer/overview.md) | **Se sei un utente senza esperienza di AEM e tecnologie headless**, fai clic qui per un&#39;introduzione completa ad AEM e alle sue funzionalità headless, dalla teoria headless fino alla pubblicazione del primo progetto headless. | Guida | Sviluppatori **senza esperienza di AEM e headless** | 1 ora |
| [Guida introduttiva headless](/help/sites-developing/headless/getting-started/introduction.md) | **Se sei un utente esperto di AEM** che necessita di un riepilogo delle principali funzioni headless di AEM, consulta questa breve panoramica. | Guida rapida | Sviluppatori e amministratori **con esperienza di AEM** | 20 minuti |
| [Guida introduttiva all&#39;esercitazione pratica su AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=it) | **Se preferisci un approccio pratico e hai familiarità con AEM**, questo tutorial si concentra direttamente sulla creazione di un semplice progetto headless. | Tutorial | Sviluppatori | 2 ore |
| [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it) | Questa raccolta di risorse viene fornita sia per gli sviluppatori **new** che per quelli **esperti**. | Raccolta di risorse | Sviluppatori | |
