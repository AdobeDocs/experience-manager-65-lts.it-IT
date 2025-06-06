---
title: Creazione di progetti di traduzione per frammenti di contenuto
description: Scopri come tradurre i frammenti di contenuto in Adobe Experience Manager.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
feature: Content Fragments
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: cad7253d-95fb-47eb-b1c9-2d22a9e34481
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 5%

---

# Creazione di progetti di traduzione per frammenti di contenuto {#creating-translation-projects-for-content-fragments}

Oltre alle risorse, Adobe Experience Manager (AEM) Assets supporta flussi di lavoro di copia per lingua per [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) (incluse le varianti). Non è necessaria alcuna ottimizzazione aggiuntiva per eseguire flussi di lavoro di copia per lingua sui frammenti di contenuto. In ogni flusso di lavoro, l’intero frammento di contenuto viene inviato per la traduzione.

I tipi di flussi di lavoro che è possibile eseguire sui frammenti di contenuto sono esattamente simili ai tipi di flusso di lavoro eseguiti per le risorse. Inoltre, le opzioni disponibili all’interno di ciascun tipo di flusso di lavoro corrispondono a quelle disponibili nei corrispondenti tipi di flussi di lavoro per le risorse.

Sui frammenti di contenuto è possibile eseguire i seguenti tipi di flussi di lavoro per la copia in lingua:

**Crea e traduci**

In questo flusso di lavoro, i frammenti di contenuto da tradurre vengono copiati nella directory principale della lingua nella quale desideri tradurre. Inoltre, a seconda delle opzioni scelte, viene creato un progetto di traduzione per i frammenti di contenuto nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato.

**Aggiorna copie per lingua**

Quando il frammento di contenuto sorgente viene aggiornato o modificato, il frammento di contenuto corrispondente specifico per lingua/lingua richiede la riconversione. Il flusso di lavoro di aggiornamento delle copie per lingua traduce un ulteriore gruppo di frammenti di contenuto e lo include in una copia in lingua per una specifica lingua. In questo caso, i frammenti di contenuto tradotti vengono aggiunti alla cartella di destinazione che contiene già frammenti di contenuto tradotti in precedenza.

## Creare e tradurre il flusso di lavoro {#create-and-translate-workflow}

Il flusso di lavoro Crea e traduci include le seguenti opzioni. Le fasi procedurali associate a ciascuna opzione sono simili a quelle associate all’opzione corrispondente per le risorse.

* Crea solo struttura: per i passaggi della procedura, vedere [Crea struttura solo per risorse](translation-projects.md#create-structure-only).
* Crea un progetto di traduzione: per i passaggi della procedura, consulta [Creare un progetto di traduzione per le risorse](translation-projects.md#create-a-new-translation-project).
* Aggiungi al progetto di traduzione esistente: per i passaggi della procedura, consulta [Aggiungi al progetto di traduzione esistente per le risorse](translation-projects.md#add-to-existing-translation-project).

## Flusso di lavoro Aggiorna copie per lingua {#update-language-copies-workflow}

Il flusso di lavoro Aggiorna copie per lingua include le seguenti opzioni. Le fasi procedurali associate a ciascuna opzione sono simili a quelle associate all’opzione corrispondente per le risorse.

* Crea un progetto di traduzione: per i passaggi della procedura, consulta [Creare un progetto di traduzione per le risorse](translation-projects.md#create-a-new-translation-project) (flusso di lavoro di aggiornamento).
* Aggiungi al progetto di traduzione esistente: per i passaggi della procedura, consulta [Aggiungi al progetto di traduzione esistente per le risorse](translation-projects.md#add-to-existing-translation-project) (flusso di lavoro di aggiornamento).

Puoi anche creare copie temporanee per i frammenti in una lingua diversa, nello stesso modo in cui crei copie temporanee per le risorse. Per informazioni dettagliate, consulta [Creazione di copie temporanee della lingua per le risorse](translation-projects.md#creating-temporary-language-copies).

## Traduzione di frammenti multimediali diversi {#translating-mixed-media-fragments}

AEM consente di tradurre frammenti di contenuto che includono vari tipi di risorse multimediali e raccolte. Se traduci un frammento di contenuto che include risorse in linea, le copie tradotte di tali risorse vengono memorizzate nella directory principale della lingua di destinazione.

Se il frammento di contenuto include una raccolta, le risorse all’interno della raccolta vengono tradotte insieme al frammento di contenuto. Le copie tradotte delle risorse vengono memorizzate nella directory principale della lingua di destinazione appropriata in una posizione corrispondente alla posizione fisica delle risorse di origine nella directory principale della lingua di origine.

Per tradurre frammenti di contenuto che includono file multimediali diversi, modifica innanzitutto il framework di traduzione predefinito per abilitare la traduzione delle risorse e delle raccolte in linea associate ai frammenti di contenuto.

1. Fai clic sul logo AEM e passa a **[!UICONTROL Strumenti > Distribuzione > Cloud Services]**.
1. Individua **[!UICONTROL Integrazione traduzione]** in **[!UICONTROL Adobe Marketing Cloud]** e fai clic su **[!UICONTROL Mostra configurazioni]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. Dall&#39;elenco delle configurazioni disponibili, fare clic su **[!UICONTROL Configurazione predefinita (configurazione integrazione di traduzione)]** per aprire la pagina **[!UICONTROL Configurazione predefinita]**.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti per visualizzare la finestra di dialogo **[!UICONTROL Configurazione traduzione]**.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. Passa alla scheda **[!UICONTROL Assets]** e scegli **[!UICONTROL Inline Media Assets e le raccolte associate]** dall&#39;elenco **[!UICONTROL Traduci frammento di contenuto Assets]**. Fare clic su **[!UICONTROL OK]** per salvare le modifiche.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. Dalla cartella principale inglese, apri un frammento di contenuto.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. Fai clic sull&#39;icona **[!UICONTROL Inserisci risorsa]**.

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. Inserisci una risorsa nel frammento di contenuto.

   ![inserisci risorsa nel frammento di contenuto](assets/column-view.png)

1. Fare clic sull&#39;icona **[!UICONTROL Associa contenuto]**.

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. Fare clic su **[!UICONTROL Associa contenuto]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. Seleziona una raccolta e includila nel frammento di contenuto. Fai clic su **[!UICONTROL Salva]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. Seleziona il frammento di contenuto e fai clic sull&#39;icona **[!UICONTROL GlobalNav]**.
1. Seleziona **[!UICONTROL Riferimenti]** dal menu per visualizzare il riquadro **[!UICONTROL Riferimenti]**.

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. Fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare le copie per lingua.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. Fai clic su **[!UICONTROL Crea e traduci]** dalla parte inferiore del pannello per visualizzare la finestra di dialogo **[!UICONTROL Crea e traduci]**.

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. Selezionare la lingua di destinazione dall&#39;elenco **[!UICONTROL Lingue di destinazione]**.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. Selezionare il tipo di progetto di traduzione dall&#39;elenco **[!UICONTROL Progetto]**.

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. Specificare il titolo del progetto nella casella **[!UICONTROL Titolo progetto]**, quindi fare clic su **Crea**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. Passa alla console **[!UICONTROL Progetti]** e apri la cartella del progetto di traduzione creato.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. Fai clic sul riquadro del progetto per aprire la pagina dei dettagli del progetto.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. Dal riquadro Lavoro di traduzione, verifica il numero di risorse da tradurre.
1. Avvia il processo di traduzione dal riquadro **[!UICONTROL Processo di traduzione]**.

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. Fai clic sui puntini di sospensione nella parte inferiore del riquadro Lavoro di traduzione per visualizzare lo stato del lavoro di traduzione.

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. Fai clic sul frammento di contenuto per verificare il percorso delle risorse associate tradotte.

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. Esamina la copia per lingua della raccolta nella console Raccolte.

   ![chlimage_1-465](assets/chlimage_1-465.png)

   Tieni presente che solo il contenuto della raccolta è tradotto. La raccolta stessa non è tradotta.

1. Passa al percorso della risorsa associata tradotta. Tieni presente che la risorsa tradotta viene memorizzata nella directory principale della lingua di destinazione.

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. Passa alle risorse all’interno della raccolta che vengono tradotte insieme al frammento di contenuto. Tieni presente che le copie tradotte delle risorse vengono memorizzate nella directory principale della lingua di destinazione appropriata.

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >Le procedure per aggiungere un frammento di contenuto a un progetto esistente o per eseguire flussi di lavoro di aggiornamento sono simili alle procedure corrispondenti per le risorse. Per informazioni su queste procedure, vedere le procedure descritte per le risorse.
