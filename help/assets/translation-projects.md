---
title: Creare progetti di traduzione
description: Scopri come creare progetti di traduzione in [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Admin
feature: Translation
solution: Experience Manager, Experience Manager Assets
exl-id: e6b78580-a96e-4560-8f25-b62bb04b060e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 15%

---

# Creare progetti di traduzione {#creating-translation-projects}

Per creare una copia per lingua, attivare uno dei seguenti flussi di lavoro per la copia della lingua disponibili nella barra Riferimenti nell&#39;interfaccia utente [!DNL Experience Manager].

* **Crea e traduci**: in questo flusso di lavoro, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. Inoltre, a seconda delle opzioni scelte, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato.

* **Aggiorna copie per lingua**: esegui questo flusso di lavoro per tradurre un gruppo aggiuntivo di risorse e includerlo in una copia per lingua per una lingua specifica. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già le risorse tradotte in precedenza.

>[!PREREQUISITES]
>
>* Gli utenti che creano progetti di traduzione sono membri del gruppo `projects-administrators`.
>* Il fornitore di servizi di traduzione supporta la traduzione dei file binari.

## Creare e tradurre il flusso di lavoro {#create-and-translate-workflow}

Puoi utilizzare il flusso di lavoro Crea e traduci per generare per la prima volta copie per una determinata lingua. Il flusso di lavoro fornisce le seguenti opzioni:

* Crea solo struttura.
* Crea un progetto di traduzione.
* Aggiungi al progetto di traduzione esistente.

### Crea solo struttura {#create-structure-only}

Utilizza l’opzione **[!UICONTROL Crea solo struttura]** per creare una gerarchia di cartelle di destinazione all’interno della directory principale lingua di destinazione, in modo che corrisponda alla gerarchia della cartella di origine all’interno della directory principale lingua di origine. In questo caso, le risorse di origine vengono copiate nella cartella di destinazione. Tuttavia, non viene generato alcun progetto di traduzione.

1. Nell&#39;interfaccia [!DNL Assets] selezionare la cartella di origine per la quale si desidera creare una struttura nella directory principale lingua di destinazione.

1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**.

   ![Copie per lingua](assets/translation-language-copies.png)

1. Fai clic su **[!UICONTROL Crea e traduci]**. Dall&#39;elenco **[!UICONTROL Lingue di destinazione]**, selezionare la lingua per la quale si desidera creare una struttura di cartelle.

1. Dall’elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea solo struttura]**.

1. Fai clic su **[!UICONTROL Crea]**. La nuova struttura per la lingua di destinazione è elencata in **[!UICONTROL Copie per lingua]**.

   ![copie per lingua](assets/lang-copy2.png)

1. Fare clic sulla struttura dall&#39;elenco, quindi fare clic su **[!UICONTROL Mostra in Assets]** per passare alla struttura di cartelle nella lingua di destinazione.

   ![risorse da visualizzare](assets/reveal-in-assets.png)

### Crea un progetto di traduzione {#create-a-new-translation-project}

Se utilizzi questa opzione, le risorse da tradurre vengono copiate nella directory principale della lingua in cui desideri tradurre. A seconda delle opzioni scelte, viene creato un progetto di traduzione per le risorse nella console Progetti. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o eseguito automaticamente non appena viene creato.

1. Nell&#39;interfaccia utente di [!DNL Assets], selezionare la cartella di origine per la quale si desidera creare una copia in lingua.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Fai clic su **[!UICONTROL Crea e traduci]** in basso.

1. Dall&#39;elenco **[!UICONTROL Lingue di destinazione]**, selezionare le lingue per le quali si desidera creare una struttura di cartelle.

1. Dall&#39;elenco **[!UICONTROL Progetto]**, selezionare **[!UICONTROL Crea un nuovo progetto di traduzione]**.

1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.

1. Fai clic su **[!UICONTROL Crea]**. [!DNL Assets] dalla cartella di origine vengono copiati nelle cartelle di destinazione per le impostazioni internazionali selezionate al passaggio 4.

   ![copie per lingua](assets/lang-copy2.png)

1. Per passare alla cartella, selezionare la copia per lingua e fare clic su **[!UICONTROL Mostra in Assets]**.

   ![risorse da visualizzare](assets/reveal-in-assets.png)

1. Passa alla console Progetti. La cartella di traduzione viene copiata nella console Progetti.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Apri la cartella per visualizzare il progetto di traduzione.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Fai clic sul progetto per aprire la pagina dei dettagli.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Per visualizzare lo stato del processo di traduzione, fai clic sui puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Per ulteriori dettagli sugli stati dei processi, vedi [Monitoraggio dello stato di un processo di traduzione](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Passa all&#39;interfaccia utente [!DNL Assets] e apri la pagina [!UICONTROL Proprietà] per ciascuna delle risorse tradotte per visualizzare i metadati tradotti.

   ![visualizza i metadati tradotti nella pagina Proprietà risorsa](assets/translated-metadata-asset-properties.png)

   *Figura: metadati tradotti nella pagina delle proprietà della risorsa.*

   >[!NOTE]
   >
   >Questa funzione è disponibile sia per le risorse che per le cartelle. Quando viene selezionata una risorsa invece di una cartella, l’intera gerarchia di cartelle fino alla directory principale della lingua viene copiata per creare una copia per lingua della risorsa.

### Aggiungi al progetto di conversione corrente {#add-to-existing-translation-project}

Se utilizzi questa opzione, il flusso di lavoro di traduzione viene eseguito per le risorse aggiunte alla cartella di origine dopo l’esecuzione di un flusso di lavoro di traduzione precedente. Solo le risorse appena aggiunte vengono copiate nella cartella di destinazione che contiene le risorse tradotte in precedenza. In questo caso non viene creato alcun nuovo progetto di traduzione.

1. Nell&#39;interfaccia utente [!DNL Assets], passa alla cartella di origine contenente le risorse non tradotte.
1. Seleziona una risorsa da tradurre e apri il **[!UICONTROL riquadro Riferimento]**. Nella sezione **[!UICONTROL Copie per lingua]** viene visualizzato il numero di copie di traduzione attualmente disponibili.
1. Fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]**. Viene visualizzato un elenco delle copie di traduzione disponibili.
1. Fai clic su **[!UICONTROL Crea e traduci]** in basso.

1. Dall&#39;elenco **[!UICONTROL Lingue di destinazione]**, selezionare le lingue per le quali si desidera creare una struttura di cartelle.

1. Dall’elenco **[!UICONTROL Progetto]**, seleziona **[!UICONTROL Aggiungi al progetto di traduzione esistente]** per eseguire il flusso di lavoro di traduzione nella cartella.

   >[!NOTE]
   >
   >Se si sceglie l&#39;opzione **[!UICONTROL Aggiungi al progetto di traduzione esistente]**, il progetto di traduzione verrà aggiunto a un progetto preesistente solo se le impostazioni del progetto corrispondono esattamente a quelle del progetto preesistente. In caso contrario, viene creato un nuovo progetto.

1. Dall&#39;elenco **[!UICONTROL Progetto di traduzione esistente]**, seleziona un progetto per aggiungere la risorsa per la traduzione.

1. Fai clic su **[!UICONTROL Crea]**. Le risorse da tradurre vengono aggiunte alla cartella di destinazione. La cartella aggiornata è elencata nella sezione **[!UICONTROL Copie per lingua]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Passa alla console Progetti e apri il progetto di traduzione esistente aggiunto a.
1. Fai clic sul progetto di traduzione per visualizzare la pagina dei dettagli del progetto.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Fai clic sui puntini di sospensione nella parte inferiore del riquadro **Processo di traduzione** per visualizzare le risorse nel flusso di lavoro di traduzione. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

   >[!NOTE]
   >
   >Se elimini la voce per tag o metadati, nessun tag o metadati viene tradotto per nessuna delle risorse.

   >[!NOTE]
   >
   >Se la risorsa aggiunta al processo di traduzione include risorse secondarie, selezionale e rimuovile affinché la traduzione possa procedere senza errori.

1. Per avviare la traduzione delle risorse, fai clic sulla freccia nella sezione **[!UICONTROL Processo di traduzione]** e seleziona **[!UICONTROL Inizio]** dall&#39;elenco.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un messaggio notifica l’inizio del processo di traduzione.

1. Per visualizzare lo stato del processo di traduzione, fai clic sui puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Per ulteriori dettagli, vedi [Monitoraggio dello stato di un processo di traduzione](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Al termine della traduzione, lo stato diventa Pronto per la revisione. Passa all&#39;interfaccia utente [!DNL Assets] e apri la pagina Proprietà di ciascuna delle risorse tradotte per visualizzare i metadati tradotti.

## Aggiorna copie per lingua {#update-language-copies}

Esegui questo flusso di lavoro per tradurre qualsiasi set aggiuntivo di risorse e includerlo in una copia per lingua specifica. In questo caso, le risorse tradotte vengono aggiunte alla cartella di destinazione che contiene già le risorse tradotte in precedenza. A seconda della scelta di opzioni, viene creato un progetto di traduzione o viene aggiornato un progetto di traduzione esistente per le nuove risorse. Il flusso di lavoro Aggiorna copie per lingua include le seguenti opzioni:

* Crea un progetto di traduzione
* Aggiungi al progetto di conversione corrente

### Crea un progetto di traduzione {#create-a-new-translation-project-1}

Se utilizzi questa opzione, viene creato un progetto di traduzione per il set di risorse per il quale desideri aggiornare una copia per lingua.

1. Dall&#39;interfaccia utente [!DNL Assets], seleziona la cartella di origine in cui hai aggiunto una risorsa.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare l&#39;elenco delle copie per lingua.
1. Seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**, quindi fai clic sulla cartella di destinazione che corrisponde alle impostazioni internazionali appropriate.

   ![seleziona copia per lingua](assets/lang-copy1.png)

1. Fai clic su **[!UICONTROL Aggiorna copie per lingua]** in basso.

1. Dall&#39;elenco **[!UICONTROL Progetto]**, scegli **[!UICONTROL Crea un nuovo progetto di traduzione]**.

1. Nel campo **[!UICONTROL Titolo progetto]**, inserisci un titolo.

1. Fare clic su **[!UICONTROL Inizio]**.
1. Passa alla console Progetti. La cartella di traduzione viene copiata nella console Progetti.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Apri la cartella per visualizzare il progetto di traduzione.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Fai clic sul progetto per aprire la pagina dei dettagli.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Per avviare la traduzione delle risorse, fai clic sulla freccia nella sezione **[!UICONTROL Processo di traduzione]** e seleziona **[!UICONTROL Inizio]** dall&#39;elenco.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un messaggio notifica l’inizio del processo di traduzione.

1. Per visualizzare lo stato del processo di traduzione, fai clic sui puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Per ulteriori dettagli sugli stati dei processi, vedi [Monitoraggio dello stato di un processo di traduzione](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Passa all&#39;interfaccia utente [!DNL Assets] e apri la pagina Proprietà di ciascuna delle risorse tradotte per visualizzare i metadati tradotti.

### Aggiungi al progetto di conversione corrente {#add-to-existing-translation-project-1}

Se si utilizza questa opzione, il set di risorse viene aggiunto a un progetto di traduzione esistente per aggiornare la copia per lingua scelta.

1. Dall&#39;interfaccia utente [!DNL Assets], selezionare la cartella di origine in cui è stata aggiunta una cartella di risorse.
1. Apri il riquadro **[!UICONTROL Riferimenti]** e fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare l&#39;elenco delle copie per lingua.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Per selezionare tutte le copie della lingua, seleziona la casella di controllo che precede **[!UICONTROL Copie per lingua]**. Deseleziona le altre copie, ad eccezione della copia (o copie) per lingua corrispondente alle impostazioni internazionali verso cui vuoi tradurre.

   ![seleziona copia per lingua](assets/lang-copy1.png)

1. Fai clic su **[!UICONTROL Aggiorna copie per lingua]** in basso.

1. Dall&#39;elenco **[!UICONTROL Progetto]** scegliere **[!UICONTROL Aggiungi al progetto di traduzione esistente]**.

1. Dall&#39;elenco **[!UICONTROL Progetto di traduzione esistente]**, seleziona un progetto per aggiungere la risorsa per la traduzione.

1. Fare clic su **[!UICONTROL Inizio]**.
1. Vedere i passaggi 9-14 di [Aggiungi al progetto di traduzione esistente](translation-projects.md#add-to-existing-translation-project) per completare il resto della procedura.

## Creare copie per lingua temporanee {#creating-temporary-language-copies}

Quando esegui un flusso di lavoro di traduzione per aggiornare una copia per lingua con le versioni modificate delle risorse originali, la copia per lingua esistente viene mantenuta finché non approvi le risorse tradotte. [!DNL Adobe Experience Manager Assets] archivia le risorse appena tradotte in una posizione temporanea e aggiorna la copia per lingua esistente dopo l&#39;approvazione esplicita delle risorse. Se rifiuti le risorse, la copia per lingua rimane invariata.

1. Fai clic sulla cartella principale di origine in **[!UICONTROL Copie per lingua]** per la quale hai già creato una copia per lingua, quindi fai clic su **[!UICONTROL Mostra in Assets]** per aprire la cartella in [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Dall&#39;interfaccia [!DNL Assets], seleziona una risorsa già tradotta e fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti per aprire la risorsa in modalità di modifica.
1. Modifica la risorsa, quindi salva le modifiche.
1. Eseguire i passaggi da 2 a 14 della procedura [Aggiungi al progetto di traduzione esistente](#add-to-existing-translation-project) per aggiornare la copia per lingua.
1. Fai clic sui puntini di sospensione nella parte inferiore del riquadro **[!UICONTROL Processo di traduzione]**. Dall&#39;elenco delle risorse nella pagina **[!UICONTROL Processo di traduzione]**, puoi visualizzare chiaramente il percorso temporaneo in cui è memorizzata la versione tradotta della risorsa.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Seleziona la casella di controllo accanto a **[!UICONTROL Titolo]**.
1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Accetta traduzione]** ![Accetta traduzione](assets/do-not-localize/thumb-up.png), quindi fai clic su **[!UICONTROL Accetta]** nella finestra di dialogo per sovrascrivere la risorsa tradotta nella cartella di destinazione con la versione tradotta della risorsa modificata.

   >[!NOTE]
   >
   >Per abilitare il flusso di lavoro di traduzione per aggiornare le risorse di destinazione, accetta sia la risorsa che i metadati.

   Fai clic su **[!UICONTROL Rifiuta traduzione]** ![Rifiuta traduzione](assets/do-not-localize/thumb-down.png) per mantenere la versione tradotta in origine della risorsa nella directory principale delle impostazioni locali di destinazione e rifiutare la versione modificata.

1. Per visualizzare i metadati tradotti, passa alla console [!DNL Assets] e apri la pagina [!UICONTROL Proprietà] per ciascuna delle risorse tradotte.

## Suggerimenti e limitazioni {#tips-limitations}

* Se avvii un flusso di lavoro di traduzione per risorse complesse, ad esempio file PDF e [!DNL Adobe InDesign], le relative risorse secondarie o rappresentazioni (se presenti) non vengono inviate per la traduzione.
* Se utilizzi la traduzione automatica, i binari delle risorse non vengono tradotti.
