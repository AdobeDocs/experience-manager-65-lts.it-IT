---
title: Gestione multisito e traduzione
description: Scopri come riutilizzare i contenuti all’interno del progetto e gestire siti web multilingue in Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Multi Site Manager, Language Copy
role: Admin
exl-id: 325089d0-9310-4219-b0e3-9645c3189d37
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 33%

---

# Gestione multisito e traduzione {#msm-and-translation}

Sono disponibili i seguenti strumenti di amministrazione per la gestione di siti web e pagine:

* Multi Site Manager (MSM) consente di utilizzare lo stesso contenuto del sito in più posizioni, consentendo al contempo l’utilizzo di varianti:

   * [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](/help/sites-administering/msm.md)

* La traduzione consente di automatizzare la traduzione di contenuti di pagina, risorse e contenuti generati dall’utente per creare e gestire siti web multilingue:

   * [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md)

* Queste due funzionalità possono essere combinate per gestire i siti Web che sono entrambi [Multinazionali e Multilingue](#multinational-and-multilingual-sites).

## Siti multinazionali e multilingue {#multinational-and-multilingual-sites}

Puoi creare contenuti per siti multinazionali e multilingue in modo efficiente tramite l’utilizzo combinato di Multi Site Manager e del flusso di lavoro di traduzione. Crea un sito master in una lingua, per un paese specifico, quindi utilizza tale contenuto come base per gli altri siti, utilizzando la traduzione, se necessario:

* [Tradurre](/help/sites-administering/translation.md) il sito master in lingue diverse.

* Utilizza [Multi Site Manager](/help/sites-administering/msm.md) per:

   * Riutilizzare i contenuti del sito master e delle traduzioni per creare siti per altri paesi e culture.
   * Assicurati di limitare l’utilizzo del gestore multisito ai contenuti in una sola lingua, ad esempio master inglese > filiali in lingua inglese nei siti del paese, master francese > filiali in lingua francese nei siti del paese.
   * Se necessario, scollega gli elementi delle Live Copy per aggiungere i dettagli di localizzazione.

Il diagramma seguente illustra l’intersezione dei concetti principali (ma non tutti i livelli/elementi coinvolti):

![Diagramma che mostra i concetti principali di MSM e traduzione](assets/chlimage_1-71a.png)

>[!NOTE]
>
>In questo scenario (e simili) MSM non gestisce le diverse versioni linguistiche in quanto tali.
>
>* [MSM](/help/sites-administering/msm.md) gestisce la distribuzione dei contenuti tradotti da un blueprint (ad esempio, un master globale) alle Live Copy (ad esempio, i siti locali), entro i limiti di una lingua.
>* Le capacità di integrazione delle [traduzioni](/help/sites-administering/translation.md) di AEM, in collaborazione con servizi di gestione della localizzazione di terze parti, gestiscono le lingue e traducono i contenuti in diverse lingue.
>
>Per casi di utilizzo più avanzati, MSM può essere utilizzato anche tra le lingue master.

>[!NOTE]
>
>Per tutti i casi d’uso si consiglia di leggere le seguenti best practice:
>
>* [Best practice per MSM](/help/sites-administering/msm-best-practices.md); in particolare:
>
>   * [Crea sito](/help/sites-administering/msm-best-practices.md#create-site)
>   * [Siti Web MSM e multilingue](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Best practice per la traduzione](/help/sites-administering/tc-bp.md)
