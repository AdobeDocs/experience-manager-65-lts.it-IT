---
title: Profili per l’elaborazione di metadati, immagini e video
description: Un profilo è un insieme di regole relative alle opzioni da applicare alle risorse caricate in una cartella. Specifica il profilo di metadati e il profilo di codifica video da applicare alle risorse video caricate. Per le risorse di immagini, puoi anche specificare il profilo di imaging da applicare alle risorse di immagini per ritagliarle correttamente.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
docset: aem65
role: User, Admin
feature: Workflow,Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
exl-id: aa257d33-302c-4a01-be48-e4ff56700bfa
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# Profili per l’elaborazione di metadati, immagini e video{#profiles-for-processing-metadata-images-and-videos}

Un profilo è la ricetta per le opzioni da applicare alle risorse caricate in una cartella. Ad esempio, puoi specificare il profilo di metadati e il profilo di codifica video da applicare alle risorse video caricate. Oppure, quale profilo di imaging applicare alle risorse di immagini per ritagliarle correttamente.

Tali regole possono includere l’aggiunta di metadati, il ritaglio intelligente delle immagini o la definizione di profili di codifica video. In Adobe Experience Manager, puoi creare tre tipi di profili, descritti in dettaglio ai seguenti collegamenti:

* [Profili metadati](/help/assets/metadata-config.md#metadata-profiles)
* [Profili immagine](/help/assets/image-profiles.md)
* [Profili video](/help/assets/video-profiles.md)

Per creare, modificare ed eliminare metadati, immagini o profili video sono necessari i diritti di amministratore.

Dopo aver creato i metadati, l’immagine o il profilo video, li assegni a una o più cartelle da utilizzare come destinazione per le risorse appena caricate.

Un concetto importante relativo all’utilizzo dei profili in Experience Manager Assets è che vengono assegnati alle cartelle. All’interno di un profilo sono presenti impostazioni sotto forma di profili di metadati, insieme a profili video o profili immagine. Queste impostazioni elaborano il contenuto di una cartella insieme alle relative sottocartelle. Pertanto, il modo in cui si denominano file e cartelle, si organizzano le sottocartelle e si gestiscono i file all’interno di queste cartelle ha un impatto significativo sul modo in cui tali risorse vengono elaborate da un profilo.
Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate, nonché una buona prassi in materia di metadati, puoi sfruttare al massimo la raccolta di risorse digitali e garantire che i file giusti vengano elaborati dal profilo corretto.

>[!NOTE]
>
>Assets che passi da una cartella a un’altra non viene rielaborato. Si supponga, ad esempio, di avere la cartella 1 a cui è assegnato il profilo A e la cartella 2 a cui è assegnato il profilo B. Se sposti le risorse dalla cartella 1 alla cartella 2, le risorse spostate mantengono l’elaborazione originale dalla cartella 1.
>
>Lo stesso vale anche quando si spostano risorse tra due cartelle a cui è assegnato lo stesso profilo.

## Rielaborazione delle risorse in una cartella {#reprocessing-assets}

>[!NOTE]
>
>Si applica a *Dynamic Media - Modalità Scene7* solo in Experience Manager 6.4.6.0 o versione successiva.

È possibile rielaborare le risorse in una cartella che dispone già di un profilo di elaborazione esistente che è stato successivamente modificato.

Si supponga, ad esempio, di aver creato un profilo Immagine e di averlo assegnato a una cartella. Il profilo Immagine veniva applicato automaticamente alle risorse di immagini caricate nella cartella. Tuttavia, in seguito decidi di aggiungere al profilo una nuova proporzione di ritaglio avanzato. Ora, invece di selezionare e ricaricare nuovamente le risorse nella cartella, è sufficiente eseguire il flusso di lavoro *Rielaborazione elemento multimediale dinamico* <!-- *Scene7: Reprocess Assets* -->.

Puoi eseguire il flusso di lavoro di rielaborazione su una risorsa per la quale la prima elaborazione non è riuscita. Di conseguenza, anche se non hai modificato un profilo di elaborazione o applicato un profilo di elaborazione, puoi comunque eseguire il flusso di lavoro di rielaborazione su una cartella di risorse in qualsiasi momento.

Se necessario, puoi modificare la dimensione batch del flusso di lavoro di rielaborazione da un valore predefinito di 50 risorse a un massimo di 1000 risorse. Quando si esegue il flusso di lavoro _Scene7: Rielabora Assets_ in una cartella, le risorse vengono raggruppate in batch e quindi inviate al server Dynamic Media per l&#39;elaborazione. Dopo l’elaborazione, i metadati di ciascuna risorsa nell’intero set di batch vengono aggiornati in Experience Manager. Se la dimensione del batch è grande, potrebbe verificarsi un ritardo nell’elaborazione. In alternativa, se la dimensione del batch è troppo piccola, potrebbero verificarsi troppi round trip al server Dynamic Media.

Vedere [Regolare la dimensione del batch del flusso di lavoro di rielaborazione](#adjusting-load).

>[!NOTE]
>
>Se esegui una migrazione in blocco di risorse da Dynamic Media Classic ad Experience Manager, devi abilitare l’agente di replica di migrazione sul server Dynamic Media. Al termine della migrazione, assicurati di disabilitare l’agente.
>
>L’agente di pubblicazione della migrazione deve essere disabilitato sul server Dynamic Media in modo che il flusso di lavoro Rielabora funzioni come previsto.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job, and so on, until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**Per rielaborare le risorse in una cartella:**

1. In Experience Manager, dalla pagina di Assets, accedi a una cartella di risorse a cui è assegnato un profilo di elaborazione e per la quale desideri applicare il flusso di lavoro **[!UICONTROL Rielaborazione elemento multimediale dinamico]**,

   Le cartelle a cui è già stato assegnato un profilo di elaborazione sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella in Vista a schede.

1. Seleziona una cartella.

   * Il flusso di lavoro considera tutti i file nella cartella selezionata in modo ricorsivo.
   * Se nella cartella principale selezionata sono presenti una o più sottocartelle con risorse, il flusso di lavoro rielabora ogni risorsa nella gerarchia delle cartelle.
   * Come best practice, evita di eseguire questo flusso di lavoro su una gerarchia di cartelle con più di 1000 risorse.

1. Selezionare **[!UICONTROL Timeline]** dall&#39;elenco a discesa nell&#39;angolo superiore sinistro della pagina.
1. Nell&#39;angolo inferiore sinistro della pagina, a destra del campo Commento, selezionare l&#39;icona del carato ( **^** ).

   ![Rielabora flusso di lavoro risorse 1](/help/assets/assets/reprocess-assets1.png)

1. Seleziona **[!UICONTROL Avvia flusso di lavoro]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Avvia flusso di lavoro]**, scegliere **[!UICONTROL Rielaborazione elemento multimediale dinamico]**.
1. (Facoltativo) Nel campo di testo **Inserisci il titolo del flusso di lavoro**, immetti un nome per il flusso di lavoro. Se necessario, puoi utilizzare il nome per fare riferimento all’istanza del flusso di lavoro.

   ![Rielabora risorse 2](/help/assets/assets/reprocess-assets2.png)

1. Seleziona **[!UICONTROL Inizio]**, quindi seleziona **[!UICONTROL Conferma]**.

   Per monitorare il flusso di lavoro o controllarne l&#39;avanzamento, dalla pagina della console principale di Experience Manager, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]**. Nella pagina Istanze flusso di lavoro, seleziona un flusso di lavoro. Sulla barra dei menu, selezionare **[!UICONTROL Cronologia elementi aperti]**. È inoltre possibile terminare, sospendere o rinominare un flusso di lavoro selezionato dalla stessa pagina Istanze flusso di lavoro.

### Regolare la dimensione batch del flusso di lavoro di rielaborazione {#adjusting-load}

(Facoltativo) La dimensione predefinita del batch nel flusso di lavoro di rielaborazione è di 50 risorse per processo. Questa dimensione ottimale del batch è determinata dalla dimensione media delle risorse e dai tipi MIME di risorse su cui viene eseguita la rielaborazione. Un valore più alto indica che in un singolo processo di rielaborazione sono presenti molti file. Pertanto, il banner di elaborazione rimane sulle risorse di Experience Manager per un periodo di tempo più lungo. Tuttavia, se la dimensione media del file è piccola - 1 MB o inferiore - Adobe consiglia di aumentare il valore a diversi 100, ma mai più di 1000. Se la dimensione media del file è grande, ad esempio centinaia di megabyte, Adobe consiglia di ridurre la dimensione del batch fino a 10.

**Per modificare facoltativamente la dimensione del batch del flusso di lavoro di rielaborazione:**

1. In Experience Manager, seleziona **[!UICONTROL Adobe Experience Manager]** per accedere alla console di navigazione globale, quindi seleziona l&#39;icona **[!UICONTROL Strumenti]** (martello) > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli di flusso di lavoro, in Vista a schede o Vista a elenco, selezionare **[!UICONTROL Rielaborazione elemento multimediale dinamico]**.

   ![Pagina Modelli di flusso di lavoro con il flusso di lavoro Rielaborazione elementi multimediali dinamici selezionato in Vista schede](/help/assets/assets-dm/reprocess-assets7.png)

1. Sulla barra degli strumenti, selezionare **[!UICONTROL Modifica]**. Una nuova scheda del browser apre la pagina del modello di flusso di lavoro Rielaborazione elementi multimediali dinamici.
1. Nella pagina del flusso di lavoro di rielaborazione Dynamic Media, nell&#39;angolo superiore destro, selezionare **[!UICONTROL Modifica]** per &quot;sbloccare&quot; il flusso di lavoro.
1. Nel flusso di lavoro, seleziona il componente Caricamento batch Scene7 per aprire la barra degli strumenti, quindi seleziona **[!UICONTROL Configura]** nella barra degli strumenti.

   ![Componente caricamento batch Scene7](/help/assets/assets-dm/reprocess-assets8.png)

1. Nella finestra di dialogo **[!UICONTROL Caricamento batch in Scene7 - Proprietà passaggio]**, imposta quanto segue:
   * Nei campi di testo **[!UICONTROL Titolo]** e **[!UICONTROL Descrizione]** immettere un nuovo titolo e una nuova descrizione per il processo, se necessario.
   * Seleziona **[!UICONTROL Avanzamento gestore]** se il gestore avanza al passaggio successivo.
   * Nel campo **[!UICONTROL Timeout]** immettere il timeout del processo esterno (secondi).
   * Nel campo **[!UICONTROL Periodo]** immettere un intervallo di polling (secondi) per verificare il completamento del processo esterno.
   * Nel campo **[!UICONTROL Batch]**, immettere il numero massimo di risorse (50-1000) da elaborare in un processo di caricamento batch di elaborazione batch del server Dynamic Media.
   * Seleziona **[!UICONTROL Avanza per timeout]** se desideri avanzare una volta raggiunto il timeout. Annulla la selezione se desideri passare alla casella in entrata una volta raggiunto il timeout.

   ![Finestra di dialogo Proprietà](/help/assets/assets-dm/reprocess-assets3.png)

1. Nell&#39;angolo superiore destro della finestra di dialogo **[!UICONTROL Caricamento batch in Scene7 - Proprietà passaggio]**, seleziona **[!UICONTROL Fine]**.

1. Nell&#39;angolo superiore destro della pagina del modello di flusso di lavoro Rielabora elemento multimediale dinamico, selezionare **[!UICONTROL Sincronizza]**. Quando viene visualizzato **[!UICONTROL Sincronizzato]**, il modello runtime del flusso di lavoro è stato sincronizzato correttamente ed è pronto per rielaborare le risorse in una cartella.

   ![Sincronizza modello flusso di lavoro](/help/assets/assets-dm/reprocess-assets1.png)

1. Chiudi la scheda del browser che mostra il modello di flusso di lavoro Rielaborazione elementi multimediali dinamici.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.-->
