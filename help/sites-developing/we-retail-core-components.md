---
title: Prova i Componenti core in We.Retail
description: Scopri come utilizzare i componenti core in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 62b6d299-f44e-4af3-b5e1-b0e92ca0598a
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 5%

---

# Prova i componenti core in We.Retail{#trying-out-core-components-in-we-retail}

I componenti core sono componenti moderni e flessibili, facilmente estensibili e semplici da integrare nei progetti. I componenti core sono stati progettati in base a diversi principi di progettazione principali, come HTL, facilità d’uso, configurabilità, controllo delle versioni ed estensibilità. Il sito `We.Retail` è basato sui componenti core.

## Provatelo {#trying-it-out}

1. Avvia Adobe Experience Manager (AEM) con il contenuto di esempio `We.Retail` e apri la [console Componenti](/help/sites-authoring/default-components-console.md).

   **Navigazione globale > Strumenti > Componenti**

1. Aprendo la barra nella console Componenti, puoi filtrare per un particolare gruppo di componenti. I Componenti core sono disponibili in

   * `.core-wcm`: Componenti core standard
   * `.core-wcm-form`: componenti core per l&#39;invio dei moduli

   Scegli `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Tutti i componenti core utilizzano il nome **v1** per indicare la prima versione di ciascun componente. Versioni regolari sono pianificate per il rilascio in futuro, che sono compatibili con le versioni di AEM e consentono un facile aggiornamento in modo da poter sfruttare le funzioni più recenti.
1. Fare clic su **Testo (v1)**.

   Vedi che il **tipo di risorsa** del componente è `/apps/core/wcm/components/text/v1/text`. I componenti core si trovano in `/apps/core/wcm/components` e dispongono di versioni per componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fai clic sulla scheda **Documentazione** per visualizzare la documentazione per gli sviluppatori del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Torna alla console Componenti. Filtra per il gruppo **`We.Retail`** e seleziona il componente **Testo**.
1. Verificare che il **Tipo risorsa** punti a un componente come previsto in `/apps/weretail`, ma il **Super Tipo risorsa** punti al componente di base `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Fai clic sulla scheda **Utilizzo live** per vedere su quali pagine viene utilizzato questo componente. Fai clic sulla prima pagina di **ringraziamento** per modificare la pagina.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Nella pagina di ringraziamento, seleziona il componente testo e fai clic sull’icona Annulla ereditarietà nel menu Modifica del componente.

   [`We.Retail` ha una struttura del sito globalizzata](/help/sites-developing/we-retail-globalized-site-structure.md) in cui il contenuto viene inviato dal sito della lingua primaria alle [Live Copy tramite un meccanismo denominato ereditarietà](/help/sites-administering/msm.md). Per questo motivo, è necessario annullare l’ereditarietà per consentire a un utente di modificare manualmente il testo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Fai clic su **Sì** per confermare l&#39;annullamento.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una volta annullata l’ereditarietà e selezionati i componenti di testo, sono disponibili molte altre opzioni. Fai clic su **Modifica**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Ora puoi vedere quali opzioni di modifica sono disponibili per il componente testo.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Dal menu **Informazioni pagina**, selezionare **Modifica modello**.
1. Nell&#39;Editor modelli della pagina fare clic sull&#39;icona **Policy** del componente Testo nel **Contenitore layout** della pagina.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. I Componenti core consentono all’autore di un modello di configurare quali proprietà sono disponibili per gli autori di pagine. Queste proprietà includono caratteristiche quali le origini Incolla consentite, le opzioni di formattazione e gli stili di paragrafo disponibili.

   Tali finestre di dialogo di progettazione sono disponibili per molti componenti core e funzionano in parallelo con l’Editor modelli. Una volta abilitate, sono disponibili per l’autore tramite gli editor dei componenti.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Consulta anche {#further-information}

Per informazioni dettagliate sui componenti core, consulta la guida all&#39;authoring [Componenti core](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/introduction) per una panoramica delle funzionalità. Per una panoramica tecnica, consulta la guida [Sviluppo di componenti core](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/overview).



Per ulteriori informazioni sui Componenti core, vedere il documento di authoring [Componenti core](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/introduction) per una panoramica delle funzionalità dei Componenti core e il documento per sviluppatori [Sviluppo di Componenti core](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/overview) per informazioni tecniche.

È inoltre possibile esaminare [modelli modificabili](/help/sites-developing/we-retail-editable-templates.md). Per informazioni dettagliate sui modelli modificabili, consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o il documento per sviluppatori Pagina [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md).
