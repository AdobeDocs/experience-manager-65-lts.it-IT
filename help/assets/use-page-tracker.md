---
title: Utilizzare il tracciamento delle pagine e incorporare il codice nelle pagine web
description: Scopri come includere il tracciamento delle pagine e incorporare i codici JavaScript nel codice del sito web per consentire ad Adobe Analytics di acquisire i dati di utilizzo relativi alle risorse.
contentOwner: AG
role: Architect, Admin
feature: Asset Reports
solution: Experience Manager, Experience Manager Assets
exl-id: bf8b2e51-60f8-423e-8ed6-167d71d6ec94
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Utilizzare il tracciamento delle pagine e il codice di incorporamento nelle pagine web {#using-page-tracker-and-embed-code-in-web-pages}

Tracciamento pagina è una parte di codice JavaScript che includi nel codice di siti Web di terze parti per consentire ad Adobe Analytics di acquisire i dati di utilizzo relativi a [!DNL Adobe Experience Manager Assets] su questi siti Web.

Per acquisire eventi, come clic specifici di una risorsa, includi anche il codice da incorporare nel codice di un sito Web di terze parti.

Il codice di esempio seguente mostra l’aspetto di una pagina web contenente sia il codice di tracciamento pagina che il codice di incorporamento:

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## Aggiungi codice di tracciamento pagina {#adding-page-tracker-code}

Puoi aggiungere il codice di tracciamento della pagina all’interno della sezione di intestazione del codice del sito web. Il seguente snippet di codice visualizza il codice di tracciamento pagina incluso in una pagina web di esempio:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## Aggiungi codice di incorporamento {#add-embed-code}

Puoi aggiungere il codice di incorporamento nel corpo del codice del sito web. Il seguente snippet di codice visualizza il codice di incorporamento incluso in una pagina web di esempio:

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
