---
title: Gestione delle campagne
description: La gestione delle campagne offre agli esperti di marketing digitale l’opportunità di distribuire contenuti personalizzati e creare così esperienze dedicate per i visitatori. Consente di orchestrare campagne di marketing su web, e-mail e servizi mobili, coinvolgendo in tal modo i visitatori.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
exl-id: 86fe233e-b3fb-432e-861e-8134df2744e4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Gestione delle campagne{#campaign-management}

La gestione delle campagne offre agli esperti di marketing digitale l’opportunità di distribuire contenuti personalizzati e creare così esperienze dedicate per i visitatori.

Consente di orchestrare campagne di marketing su web, e-mail e servizi mobili, coinvolgendo in tal modo i visitatori. Puoi creare contenuti, segmentare i visitatori, trasmettere e promuovere contenuti mirati per profili di utenti specifici e gestire campagne su più canali.

Questo documento descrive i vari elementi che compongono le campagne. Informazioni più dettagliate sono disponibili nei seguenti documenti:

* [Teaser e strategie](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [E-mail marketing](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Pagine di destinazione](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Offerte Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Utilizzo del Marketing Campaign Manager](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Segmentazione](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configurazione della campagna](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La gestione delle campagne è composta da vari elementi:

* **Marchi**
In Adobe Experience Manager (AEM), i brand sono l&#39;unità di livello principale e costituiscono una raccolta di **Campagne**.

* **Campagne**
Una campagna è una raccolta di singole **esperienze**.

* **Esperienze**
Il contenuto mirato forma le varie esperienze, presentate al visitatore ai **punti di contatto**. Sono disponibili diversi tipi di esperienza:

   * **Teaser**

     [Le pagine/paragrafi teaser](#teasers) vengono utilizzati per indirizzare specifici visitatori **Segmenti** a contenuti incentrati sui loro interessi.

     Le pagine teaser possono:

      * presenta una serie di opzioni tra cui il visitatore può scegliere
      * mostra un solo paragrafo teaser basato sul segmento visitatore specifico. Ad esempio, il paragrafo del teaser mostrato può dipendere dall’età del visitatore.

     In genere, una pagina teaser è un’azione temporanea che dura per un periodo di tempo specifico, fino a quando non viene sostituita dalla pagina teaser successiva.

   * **Newsletter**

     [Le comunicazioni tramite posta elettronica](#emailmarketing) vengono utilizzate per coinvolgere gli utenti e incoraggiarli a visitare il sito Web. In genere assumono la forma di una newsletter, inviata ai tuoi **Lead** (raggruppati in **Elenchi**). **Nota:** Adobe non prevede di migliorare ulteriormente questa funzionalità. Si consiglia di [utilizzare Adobe Campaign e l&#39;integrazione con AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Questo consente l’integrazione con Adobe Target (precedentemente Test&amp;Target), che offre agli esperti di marketing uno strumento di ottimizzazione per la conversione da siti web con le funzionalità necessarie per rendere i contenuti online e le offerte sempre più rilevanti per i clienti con conseguenti maggiori conversioni. Adobe Target fornisce un’interfaccia intuitiva per la progettazione e l’esecuzione di test, la creazione di segmenti di pubblico e il targeting dei contenuti, il tutto da una singola applicazione.

* **Punti di contatto**

  Questi sono i punti di contatto tra il visitatore e la campagna. I punti di contatto sono collegati alle esperienze create.

  Ad esempio, per i teaser si tratta della pagina del contenuto in cui si trova il paragrafo teaser, mentre per una newsletter si tratta della mailing list.

* **Lead**

  Le informazioni raccolte sui visitatori e su come contattarli costituiscono la base per i lead. **Nota:** Adobe non prevede di migliorare ulteriormente questa funzionalità.

  Si consiglia di [utilizzare Adobe Campaign e l&#39;integrazione con AEM](/help/sites-administering/campaign.md).

* **Elenchi**

  I lead sono raggruppati in elenchi in modo da poter intraprendere azioni collettive su di essi. Nota: **Nota:** Adobe non prevede di migliorare ulteriormente questa funzionalità.

  Si consiglia di [utilizzare Adobe Campaign e l&#39;integrazione con AEM.](/help/sites-administering/campaign.md)

* **Segmenti**

  I visitatori del sito hanno interessi e obiettivi diversi quando arrivano su un sito. L’analisi di questo dato in base a fattori quali l’attività sul sito web, le informazioni sul profilo registrate e l’attività su altri siti web, ti aiuta a definire i segmenti. Il contenuto può quindi essere mirato in base alle esigenze e agli interessi del visitatore, in base ai segmenti di corrispondenza.

* **MCM**

  Marketing Campaign Manager (MCM) è una console che consente di accedere a tutte le funzionalità necessarie per creare e controllare campagne, marchi, esperienze, punti di contatto, lead, elenchi, segmenti e rapporti.

  È possibile accedervi da varie posizioni (etichettate come **Campagne**) o con, ad esempio, l&#39;URL:

  `http://localhost:4502/libs/mcm/content/admin.html`
