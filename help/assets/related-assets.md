---
title: Risorse correlate
description: Scopri come correlare le risorse digitali che condividono alcuni attributi comuni. Crea anche relazioni derivate dall’origine tra risorse digitali.
contentOwner: AG
role: User
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
exl-id: 7b07a5ce-c438-4e5f-a14c-bf96b42c2a78
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 3%

---

# Risorse correlate {#related-assets}

[!DNL Adobe Experience Manager Assets] consente di correlare manualmente le risorse in base alle esigenze dell&#39;organizzazione utilizzando la funzionalità risorse correlate. Ad esempio, puoi correlare un file di licenza con una risorsa o un’immagine o un video su un argomento simile. Puoi correlare risorse che condividono alcuni attributi comuni. È inoltre possibile utilizzare la funzione per creare relazioni di origine/derivate tra le risorse. Se ad esempio si dispone di un file PDF generato da un file INDD, è possibile correlare il file PDF al relativo file INDD di origine.

Grazie a questa funzione, è possibile condividere un file PDF a bassa risoluzione o un file JPG con fornitori o agenzie e rendere disponibile il file INDD ad alta risoluzione solo su richiesta.

>[!NOTE]
>
>Solo gli utenti con autorizzazioni di modifica per le risorse possono correlare e scollegare le risorse.

## Riferire le risorse {#relating-assets}

1. Dall&#39;interfaccia [!DNL Experience Manager], apri la pagina **[!UICONTROL Proprietà]** per una risorsa da correlare.

   ![apri la pagina Proprietà di una risorsa per correlarla](assets/asset-properties-relate-assets.png)

   *Figura: [!DNL Assets] [!UICONTROL Proprietà] pagina per correlare le risorse.*

   In alternativa, seleziona la risorsa dalla vista a elenco.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Puoi anche selezionare la risorsa da una raccolta.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Per correlare un&#39;altra risorsa alla risorsa selezionata, fare clic su **[!UICONTROL Correlare]** ![correlare le risorse](assets/do-not-localize/link-relate.png) nella barra degli strumenti.
1. Effettua una delle seguenti operazioni:

   * Per correlare il file di origine della risorsa, selezionare **[!UICONTROL Source]** dall&#39;elenco.
   * Per correlare un file derivato, selezionare **[!UICONTROL Derivato]** dall&#39;elenco.
   * Per creare una relazione bidirezionale tra le risorse, seleziona **[!UICONTROL Altri]** dall&#39;elenco.

1. Dalla schermata **[!UICONTROL Seleziona risorsa]**, individua il percorso della risorsa da correlare e selezionala.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Fai clic su **[!UICONTROL Conferma]**.
1. Fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. A seconda della relazione scelta al passaggio 3, la risorsa correlata viene elencata in una categoria appropriata nella sezione **[!UICONTROL Correlati]**. Se ad esempio la risorsa correlata è il file di origine della risorsa corrente, verrà elencata in **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Per rimuovere la correlazione di una risorsa, fare clic su **[!UICONTROL Annulla correlazione]** ![annulla correlazione tra risorse](assets/do-not-localize/link-unrelate-icon.png) nella barra degli strumenti.

1. Selezionare le risorse da rimuovere dalla finestra di dialogo **[!UICONTROL Rimuovi relazioni]** e fare clic su **[!UICONTROL Annulla correlazione]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Le risorse per le quali hai rimosso le relazioni vengono eliminate dall&#39;elenco delle risorse correlate nella sezione **[!UICONTROL Correlate]**.

## Tradurre le risorse correlate {#translating-related-assets}

La creazione di relazioni origine/derivate tra risorse utilizzando la funzione risorse correlate è utile anche nei flussi di lavoro di traduzione. Quando esegui un flusso di lavoro di traduzione su una risorsa derivata, [!DNL Experience Manager Assets] recupera automaticamente qualsiasi risorsa a cui il file di origine fa riferimento e la include per la traduzione. In questo modo, la risorsa a cui fa riferimento la risorsa sorgente viene tradotta insieme alle risorse sorgente e derivate. Ad esempio, considera uno scenario in cui la copia in lingua inglese include una risorsa derivata e il relativo file di origine, come illustrato.

![chlimage_1-281](assets/chlimage_1-281.png)

Se il file di origine è correlato a un&#39;altra risorsa, [!DNL Experience Manager Assets] recupera la risorsa di riferimento e la include per la traduzione.

![la pagina Proprietà risorsa mostra il file di origine della risorsa correlata da includere per la traduzione](assets/asset-properties-source-asset.png)

*Figura: risorsa Source delle risorse correlate da includere per la traduzione.*

1. Tradurre le risorse nella cartella di origine in una lingua di destinazione seguendo i passaggi descritti in [Creare un progetto di traduzione](translation-projects.md#create-a-new-translation-project). Ad esempio, in questo caso, traduci le risorse in francese.

1. Dalla pagina [!UICONTROL Progetti], apri la cartella di traduzione.

1. Fai clic sul riquadro del progetto per aprire la pagina dei dettagli.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Fai clic sui puntini di sospensione sotto la scheda Lavoro di traduzione per visualizzare lo stato della traduzione.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Seleziona la risorsa, quindi fai clic su **[!UICONTROL Mostra in Assets]** nella barra degli strumenti per visualizzare lo stato di traduzione della risorsa.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Per verificare se le risorse correlate all’origine sono state tradotte, fai clic sulla risorsa di origine.

1. Selezionare la risorsa correlata all&#39;origine, quindi fare clic su **[!UICONTROL Mostra in Assets]**. Viene visualizzata la risorsa correlata tradotta.
