---
title: Collegamento degli URL all’applicazione Web
description: Come collegare gli URL all’applicazione web in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: Configuration
solution: Experience Manager, Experience Manager Assets
exl-id: 16798533-855d-4f14-8edb-edba79818dbf
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 5%

---

# Collegamento degli URL all’applicazione Web {#linking-urls-to-your-web-application}

I siti web e le applicazioni accedono ai servizi Dynamic Media tramite chiamate URL. Dopo aver pubblicato una risorsa, Dynamic Media attiva una stringa URL che fa riferimento alla risorsa. Puoi incollare questi URL in un browser web per eseguirne il test.

Puoi effettuare il collegamento agli URL solo se *non* usi Experience Manager come WCM. Il collegamento, anziché l’incorporamento, viene utilizzato quando si desidera distribuire un lettore video come finestra popup o modale. Se utilizzi Experience Manager come WCM, [aggiungi le risorse direttamente nella pagina](adding-dynamic-media-assets-to-pages.md).

Per inserire queste stringhe URL nelle pagine web e nelle applicazioni, copiale da Dynamic Media.

>[!NOTE]
>
>Le stringhe URL sono disponibili solo per le rappresentazioni dinamiche delle risorse. Al momento non sono disponibili per le risorse statiche che risiedono in DAM e non nel server Dynamic Media. Il pulsante URL non viene visualizzato per le rappresentazioni statiche.

Vedi anche [Incorporare il visualizzatore di video o immagini in una pagina Web](embed-code.md).

Vedi anche [Collegare gli URL di YouTube all&#39;applicazione Web](video.md).

Vedi anche [Distribuire immagini ottimizzate per un sito reattivo](responsive-site.md).

Vedi anche [Caricare le risorse](manage-assets.md#uploading-assets).

## Ottenere un URL per una risorsa {#obtaining-a-url-for-an-asset}

Puoi ottenere una stringa URL generata da un predefinito immagine o da un predefinito visualizzatore. Una volta copiato, l’URL viene inserito negli Appunti, in modo da poterlo incollare nelle pagine del sito web o dell’applicazione.

>[!NOTE]
>
>L’URL non è disponibile per la copia finché non hai pubblicato la risorsa selezionata. Inoltre, devi pubblicare anche il predefinito visualizzatore o il predefinito immagine.
>
>Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).
>
>Consulta [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

Esistono diversi modi per ottenere una stringa URL. Tuttavia, i passaggi seguenti mostrano un solo metodo che puoi utilizzare.

**Per ottenere un URL per una risorsa:**

1. Passa alla risorsa *published* di cui desideri copiare l&#39;URL del predefinito immagine o del predefinito visualizzatore e seleziona la risorsa per aprirlo.

   Gli URL sono disponibili per la copia solo *dopo* la prima *pubblicazione* delle risorse. Inoltre, è necessario pubblicare anche il predefinito visualizzatore o il predefinito immagine.

   Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).

   Consulta [Predefiniti visualizzatore pubblicazione](managing-viewer-presets.md#publishing-viewer-presets).

   Consulta [Pubblica predefiniti immagine](managing-image-presets.md#publishing-image-presets).

1. In base alla risorsa selezionata, effettua una delle seguenti operazioni:

   * Se hai selezionato un&#39;immagine, seleziona **[!UICONTROL Rappresentazioni]** nel menu a discesa.

     Sotto l&#39;intestazione **[!UICONTROL Dynamic]**, seleziona un nome di predefinito per visualizzarne il rendering nel frame di destra. Se necessario, scorri l’elenco Rappresentazioni per visualizzare l’intestazione Dinamica.

     Nella parte inferiore della barra a sinistra, seleziona **[!UICONTROL URL]**.

     ![chlimage_1-270](assets/chlimage_1-270.png)

   * Se hai selezionato un set 360 gradi, un set di immagini, un set carosello o un video, seleziona **[!UICONTROL Visualizzatori]** dal menu a discesa.

     Nella barra a sinistra, seleziona un nome per il predefinito visualizzatore. Un’anteprima del set o del video viene aperta in una pagina separata.

     Nella barra a sinistra, in basso, seleziona **[!UICONTROL URL]**.

     ![chlimage_1-271](assets/chlimage_1-271.png)

1. Seleziona e copia il testo nel browser web per visualizzare in anteprima la risorsa o aggiungerla alla pagina del contenuto web.

   Per uscire dalla finestra dell&#39;URL, selezionare **[!UICONTROL X]** o **[!UICONTROL Chiudi]**.

## Ottenere un URL per una risorsa statica {#obtaining-a-url-for-a-static-asset}

Dynamic Media supporta la distribuzione di risorse statiche, che sono risorse aggiuntive oltre alle immagini e ai video. I formati di risorse statiche supportati per la distribuzione includono:

* File 3D
* GIF animato
* File audio
* CSS
* JavaScript (quando l’azienda è configurata con il proprio dominio)
* PDF
* SVG
* XML
* ZIP

**Per ottenere un URL per una risorsa statica:**

1. Passa alla risorsa statica *published* di cui desideri copiare l&#39;URL e seleziona la risorsa per aprirla.

   Ricorda che gli URL sono disponibili solo per copiare *dopo* che hai *pubblicato* la risorsa statica.

   Consulta [Pubblicare risorse](publishing-dynamicmedia-assets.md).

1. Per ottenere l’URL della risorsa statica pubblicata, utilizza uno dei seguenti metodi:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

        Esempio: `https://aem.com/is/content/adobe/image.gif`.

   * Seleziona **[!UICONTROL Risorsa]** > **[!UICONTROL Rappresentazioni dinamiche]**, quindi seleziona una rappresentazione dinamica della risorsa statica e copia l&#39;URL.

     Modificare l&#39;URL copiato in modo da utilizzare `is/content` nel percorso anziché `is/image/`.

## Ottenere un URL per un rendering video pubblicato {#obtaining-a-video-url-for-a-published-video-rendition}

1. In Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud]** > **[!UICONTROL Servizi cloud]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, scorri verso il basso fino all&#39;intestazione **[!UICONTROL Dynamic Media Cloud Services]**, quindi seleziona **[!UICONTROL Mostra configurazioni]**.
1. In **[!UICONTROL Configurazioni disponibili]**, selezionare il nome della configurazione desiderata.

1. Nella pagina **[!UICONTROL Impostazioni cloud per elementi multimediali dinamici]**, in **[!UICONTROL URL servizio video]**, copia l&#39;intero percorso URL. Devi inserire il percorso URL copiato più avanti nei passaggi.

   Ad esempio, il percorso URL potrebbe essere simile al seguente:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   Il percorso sopra riportato è solo un esempio; non è il percorso effettivo copiato.

1. In **[!UICONTROL ID registrazione]**, copia il nome del cliente indicato nell’ultima parte dell’ID.

   Ad esempio, se l&#39;ID di registrazione è `87654321|MyCompany`, il nome del cliente sarà `MyCompany`.

1. Nell&#39;angolo superiore sinistro della pagina, seleziona **[!UICONTROL Servizi cloud]**, quindi seleziona il logo Experience Manager e passa a **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Copia l’intero percorso della rappresentazione video dal JCR (Java™ Content Repository).

   Ad esempio, il percorso della rappresentazione del video potrebbe essere simile al seguente:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   Il percorso sopra riportato è solo un esempio; non è il percorso effettivo copiato.

1. Disporre le informazioni copiate nel seguente ordine in modo che formino un percorso URL completo:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Ad esempio, utilizzando i percorsi di esempio e il nome del cliente di esempio riportati nei passaggi precedenti, il percorso completo viene visualizzato come segue:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Questo esempio è l’URL video completo di una rappresentazione video pubblicata.

## Ottieni un URL video per streaming bitrate adattivo (DASH o HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. In Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Cloud]** > **[!UICONTROL Servizi cloud]**.
1. Nella pagina **[!UICONTROL Cloud Services]**, scorri verso il basso fino all&#39;intestazione **[!UICONTROL Dynamic Media Cloud Services]**, quindi seleziona **[!UICONTROL Mostra configurazioni]**.
1. In **[!UICONTROL Configurazioni disponibili]**, selezionare il nome della configurazione desiderata.
1. Nella pagina **[!UICONTROL Impostazioni servizi cloud per elementi multimediali dinamici]** eseguire le operazioni seguenti:

   * In **[!UICONTROL URL servizio video]**, copia l&#39;intero percorso URL. Il percorso URL copiato sarà necessario nei passaggi seguenti. Ad esempio, il percorso URL potrebbe essere simile al seguente:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   Il percorso sopra riportato è solo un esempio; non è il percorso effettivo copiato.

   * In **[!UICONTROL ID registrazione]**, copia il nome del cliente trovato nell&#39;ultima parte dell&#39;ID. Il nome del cliente così copiato sarà necessario nei passaggi seguenti.

     Ad esempio, se l&#39;ID di registrazione era `87654321|demoCo`, il nome cliente copiato sarebbe `demoCo`.

1. In base al protocollo di consegna video in uso, copia il rispettivo selettore di protocollo. Il selettore di protocollo copiato sarà necessario nei passaggi seguenti.

   | Protocollo di consegna video in uso | Selettore di protocollo da utilizzare |
   |---|---|
   | HTTP <br> Se si utilizza HTTP (distribuzione video non sicura), assicurarsi di modificare https in http nel valore URL del servizio video copiato in precedenza. | `public/` |
   | HTTPS | `public-ssl/` |

1. Copia il percorso completo della risorsa video in Experience Manager, in base a quanto elaborato da Dynamic Media. Questo percorso di risorsa video copiato è necessario nei passaggi seguenti.

   Ad esempio:

   `/content/dam/marketing/MyVideo.mp4`

1. Combina tutti i pezzi copiati in precedenza per creare una stringa nell&#39;ordine seguente:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Ad esempio, utilizzando le informazioni copiate dagli esempi in questi passaggi, la stringa viene visualizzata come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Completare l&#39;URL aggiungendo `.m3u8` alla fine della stringa. Ad esempio, aggiungendo `.m3u8` alla stringa del passaggio precedente, il percorso URL completo verrà visualizzato come segue:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Utilizza HTTP/2 per distribuire le risorse Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 è il nuovo protocollo web aggiornato che migliora il modo in cui browser e server comunicano. Consente di trasferire più rapidamente le informazioni e di ridurre la potenza di elaborazione necessaria. La distribuzione delle risorse Dynamic Media ora può avvenire tramite HTTP/2, il che offre tempi di risposta e caricamento migliori.

Consulta [Distribuzione HTTP2 dei contenuti](http2.md) per informazioni complete su come iniziare a utilizzare HTTP/2 con l&#39;account Dynamic Media.
