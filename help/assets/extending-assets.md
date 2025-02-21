---
title: Personalizza ed estendi [!DNL Assets]
description: Scopri come personalizzare ed estendere Condivisione risorse e Editor risorse, con un’interfaccia e un set di funzionalità specifiche per gli utenti.
contentOwner: AG
role: Developer
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Personalizza ed estendi [!DNL Assets] {#customizing-and-extending-assets}

L’Editor risorse è il punto di accesso principale utilizzato dagli utenti di un sito web Adobe Enterprise Manager per trovare, visualizzare e manipolare le risorse digitali nell’archivio.

In qualità di sviluppatore di [!DNL Experience Manager], puoi personalizzare ed estendere Asset Editor in diversi modi, presentando agli utenti un&#39;interfaccia e un set di funzionalità specifiche.

È possibile personalizzare o migliorare i seguenti aspetti della funzionalità:

* [Estendi editor risorse](asseteditorx.md)
* [Estendere la ricerca Assets](searchx.md)
* [Elaborare Assets utilizzando gestori di contenuti multimediali e flussi di lavoro](media-handlers.md)
* [Integrare Assets con il flusso di attività](extending-activity-stream.md)
* [Sviluppo di proxy Assets](proxy.md)
* [Best practice per configurare ImageMagick](best-practices-for-imagemagick.md)

## Personalizzare l&#39;aspetto {#customizing-the-look-and-feel}

Sono personalizzabili i seguenti aspetti dell’Editor risorse:

* Logo: puoi aggiungere il logo della tua organizzazione all’interfaccia.
* Colori e font: è possibile modificare i colori e i font utilizzati nell’interfaccia.
* Codice HTML: per una personalizzazione più completa è possibile modificare il codice HTML sottostante che definisce le interfacce.

## Personalizzare le rappresentazioni {#customizing-renditions}

Nella terminologia [!DNL Experience Manager Assets] una rappresentazione è la forma in cui viene presentata una risorsa. In generale, una particolare risorsa può avere più rappresentazioni. Ad esempio, un’immagine a colori può avere una rappresentazione nelle dimensioni originali, un’altra con dimensioni ridotte e un’altra con dimensioni ridotte e convertita in scala di grigio.

È possibile personalizzare le rappresentazioni in cui è disponibile una particolare risorsa e crearne di nuove.
