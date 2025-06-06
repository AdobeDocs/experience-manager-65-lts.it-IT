---
title: Visualizzazione dei dati di analisi delle pagine per misurare l’efficacia del contenuto delle pagine
description: Utilizzare i dati di analisi delle pagine per misurare l’efficacia del contenuto delle pagine
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Architect,Developer
exl-id: debcc73f-c2bb-4e3a-8ebf-c7590264d289
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 4%

---

# Visualizzazione dei dati di analisi delle pagine{#seeing-page-analytics-data}

Utilizza i dati di analisi della pagina per misurare l’efficacia del contenuto della pagina.

## Analytics visibile dalla console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

I dati di analisi delle pagine vengono visualizzati in [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view) della console Sites. Quando le pagine vengono visualizzate in formato elenco, per impostazione predefinita sono disponibili le seguenti colonne:

* Visualizzazioni pagina
* Visitatori univoci
* Tempo sulla pagina

Ogni colonna mostra un valore per il periodo di reporting corrente e indica anche se il valore è aumentato o diminuito rispetto al periodo di reporting precedente. I dati visualizzati vengono aggiornati ogni 12 ore.

>[!NOTE]
>
>Per modificare il periodo di aggiornamento, [configurare l&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Apri la console **Sites**, ad esempio [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. Nell&#39;angolo superiore destro della barra degli strumenti fare clic sull&#39;icona per selezionare **Vista elenco** (l&#39;icona visualizzata dipenderà dalla [vista corrente](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Di nuovo, all&#39;estrema destra della barra degli strumenti (angolo superiore destro), fai clic sull&#39;icona e seleziona **Visualizza impostazioni**. Viene visualizzata la finestra di dialogo **Configura colonne**. Apporta le modifiche necessarie e conferma con **Aggiorna**.

   ![aa-04](assets/aa-04.png)

### Selezione del periodo di reporting {#selecting-the-reporting-period}

Seleziona il periodo di reporting per il quale i dati di Analytics vengono visualizzati nella console Sites:

* Dati degli ultimi 30 giorni
* Dati degli ultimi 90 giorni
* Dati di quest&#39;anno

Il periodo di reporting corrente viene visualizzato sulla barra degli strumenti della console Sites (a destra della barra degli strumenti superiore). Utilizza l’elenco a discesa per selezionare il periodo di reporting richiesto.
![aa-05](assets/aa-05.png)

### Configurazione delle colonne di dati disponibili {#configuring-available-data-columns}

I membri del gruppo di utenti amministratori di Analytics possono configurare la console Sites per consentire agli autori di visualizzare colonne aggiuntive di Analytics.

>[!NOTE]
>
>Quando una struttura ad albero di pagine contiene elementi secondari associati a diverse configurazioni cloud di Adobe Analytics, non è possibile configurare le colonne di dati disponibili per le pagine.

1. In Vista a elenco, utilizza i selettori di visualizzazione (a destra della barra degli strumenti), seleziona **Impostazioni visualizzazione** e quindi **Aggiungi dati di analisi personalizzati**.

   ![aa-15](assets/aa-15.png)

1. Selezionare le metriche da esporre agli autori nella console Sites, quindi fare clic su **Aggiungi**.

   Le colonne visualizzate vengono recuperate da Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Apertura di Content Insights da Sites {#opening-content-insights-from-sites}

Apri [Content Insight](/help/sites-authoring/content-insights.md) dalla console Sites per ulteriori informazioni sull&#39;efficacia della pagina.

1. Nella console Sites, seleziona la pagina per la quale desideri visualizzare Content Insights.
1. Sulla barra degli strumenti, fai clic sull’icona Analytics e Recommendations.

   ![Icona Analytics and Recommendations](do-not-localize/chlimage_1-16a.png)

## Analytics visibile dall’Editor pagina (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Questo viene mostrato se [Activity Map è stato configurato](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) per il tuo sito Web.

>[!NOTE]
>
>I dati per Activity Map provengono da Adobe Analytics.

Quando il tuo sito Web è stato [configurato per Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), puoi utilizzare l&#39;Activity Map[&#128279;](/help/sites-authoring/author-environment-tools.md#page-modes) in modalità  per visualizzare i dati rilevanti. Ad esempio:

![aa-07](assets/aa-07.png)

### Accesso a Activity Map {#accessing-the-activity-map}

Dopo aver selezionato la modalità [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes), ti verrà richiesto di immettere le credenziali Adobe Analytics.

![aa-03](assets/aa-03.png)

Viene visualizzata la barra degli strumenti mobile di **Analytics**. Qui è possibile:

* modificare il formato della barra degli strumenti utilizzando le doppie frecce (**>>**)
* Attiva/disattiva dettagli pagina (icona a forma di occhio)
* Configurare le impostazioni di Activity Map (icona a forma di codice)
* Seleziona l’analisi da mostrare (vari selettori a discesa)
* Chiudi Activity Map e la barra degli strumenti (x)

![aa-09](assets/aa-09.png)

### Selezione di Analytics da visualizzare {#selecting-the-analytics-to-show}

Puoi selezionare i dati analitici da visualizzare e come visualizzarli, utilizzando i vari criteri:

* **Standard**/**Live**

* tipo di evento
* gruppo utenti
* **Bolle**/**Sfumatura**/**Utenti e perdenti**/**Scostamento**

* periodo da visualizzare

![aa-13](assets/aa-13.png)

### Configurazione di Activity Map {#configuring-the-activity-map}

Utilizza l&#39;icona **Mostra impostazioni** per aprire la finestra di dialogo **Impostazioni Activity Map**.

![aa-04-1](assets/aa-04-1.png)

La finestra di dialogo **Impostazioni Activity Map** fornisce una serie di opzioni in tre schede:

![aa-06](assets/aa-06.png)

* Generale

   * Suite per report
   * Nome pagina
   * Lingua
   * Sovrapposizioni etichetta con
   * Dimensione font etichetta
   * Colore sfumatura
   * Colore bolla
   * Sfumatura colore basata su
   * Trasparenza sfumatura

* Standard

   * Visualizzazione (tipo e numero di collegamenti)
   * Nascondi sovrapposizioni per collegamenti che non hanno ricevuto hit

* Live

   * Visualizza in alto (guadagni o perdenti)
   * Escludi % inferiore
   * Aggiornamento automatico (dati e periodo)
