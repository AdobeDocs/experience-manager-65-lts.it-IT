---
title: Best practice per l’elaborazione dei formati di file supportati
description: Best practice per elaborare i vari tipi di file supportati utilizzando  [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
solution: Experience Manager, Experience Manager Assets
exl-id: 28765aeb-1303-40da-bde0-df1b4c625d37
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Best practice per il formato dei file Assets {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] supporta molte librerie di formati di file proprietarie e di terze parti per soddisfare i diversi requisiti di supporto dei file degli utenti. Le librerie Adobe supportate includono, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Inoltre, [!DNL Experience Manager Assets] supporta librerie di terze parti, tra cui [!DNL ImageMagick], [!DNL TwelveMonkeys] e così via.

Per i formati di file supportati, vedere [Formati supportati da Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Se utilizzi [!DNL Experience Manager] su Adobe Managed Services (AMS), contatta l&#39;Assistenza clienti Adobe se intendi elaborare molti file PSD o PSB di grandi dimensioni. Collabora con il rappresentante dell’Assistenza clienti di Adobe per implementare queste best practice per l’implementazione di AMS e scegliere i migliori strumenti e modelli possibili per i formati proprietari di Adobe. [!DNL Experience Manager] potrebbe non elaborare file PSB ad alta risoluzione con più di 30000 x 23000 pixel.

## Libreria [!DNL Adobe Camera Raw] {#adobe-camera-raw-library}

Per prestazioni ottimali, Adobe consiglia di utilizzare la libreria [!DNL Adobe Camera Raw] per i file RAW e DNG.

La libreria [!DNL Adobe Camera Raw] supporta il profilo colore CMYK come input. Tuttavia, genera l&#39;output in RGB colorspace e supporta l&#39;output solo in formato JPEG. Non mantiene lo spazio colore del file di origine (ad esempio, CMYK) nelle miniature.

Per ulteriori informazioni, vedere [Supporto Camera Raw](/help/assets/camera-raw.md).

## Libreria Rasterizer di Adobe PDF {#adobe-pdf-rasterizer-library}

Per ottenere risultati ottimali, Adobe consiglia di utilizzare la libreria Rasterizer di Adobe PDF per i seguenti file:

* File PDF pesanti e ad uso intensivo di contenuti
* File AI con miniature non generati come tali
* Per i file AI con colori SPOT (PMS)

Le miniature e le anteprime generate con PDF Rasterizer offrono una qualità migliore rispetto all&#39;output raster predefinito. La libreria di Adobe PDF Rasterizer non supporta alcuna conversione di spazio colore. Indipendentemente dallo spazio colore del file PDF di origine, Adobe PDF Rasterizer genera solo output RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe consiglia di utilizzare [!DNL Adobe InDesign Server] per estrarre rappresentazioni specifiche di [!DNL Adobe InDesign], come IDML e HTML. Per ulteriori informazioni, consulta [Aggiunta di risorse Experience Manager come riferimenti in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genera e distribuisce più varianti di rich content in tempo reale attraverso la sua rete globale, scalabile e ottimizzata per le prestazioni. Offre esperienze di visualizzazione interattive e semplifica il processo di gestione delle campagne digitali. Per informazioni dettagliate sull&#39;abilitazione di [!DNL Dynamic Media], vedere [Configurazione di Dynamic Media](/help/assets/config-dynamic.md).

Attualmente, [!DNL Dynamic Media] può supportare video con un massimo di 15 GB di contenuto per file.

## Libreria ImageMagick {#imagemagick-library}

Adobe consiglia di utilizzare la libreria ImageMagick nei seguenti scenari:

* Per generare copie trasformate di miniature per i file EPS.
* Per conservare le informazioni del profilo immagine.
* Per mantenere la trasparenza.
* Per elaborare i file PSD e PSB.

Per informazioni sulla configurazione della libreria [!DNL ImageMagick] in [!DNL Experience Manager], vedere [Utilizzo di ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Per informazioni sull&#39;utilizzo ottimale, vedere [Procedure consigliate per la configurazione di ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Libreria trascodifica immagini {#image-transcoding-library}

La Adobe Imaging Transcoding Library è una soluzione di elaborazione delle immagini che esegue funzioni di base per la gestione delle immagini, tra cui codifica, transcodifica, ricampionamento, ridimensionamento e così via.

La libreria di trascodifica immagini supporta i seguenti tipi MIME:

* JPG/JPEG
* PNG (8 bit e 16 bit)
* GIF
* BMP
* TIFF/Compressed TIFF (oltre a TIFF e PTiiff a 32 bit).
* ICO
* ICN

Per ulteriori dettagli, vedere [Libreria trascodifica immagini](/help/assets/imaging-transcoding-library.md).
