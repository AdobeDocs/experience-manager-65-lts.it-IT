---
title: Aggiunta di font per il rendering grafico
description: AEM consente di generare elementi grafici che incorporano testo estratto in modo dinamico dal contenuto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 5ceaa9f0-aba1-40a3-97ef-f5ade0c2a54a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Aggiunta di font per il rendering grafico{#adding-fonts-for-graphic-rendering}

AEM consente di generare elementi grafici che incorporano testo estratto in modo dinamico dal contenuto.

A questo scopo, puoi anche caricare e utilizzare i tuoi font.

Attualmente tutte le implementazioni della piattaforma Java supportano [caratteri TrueType](https://en.wikipedia.org/wiki/Truetype).

1. Apri CRXDE Lite e passa alla cartella dell’applicazione del progetto:

   `/apps/<your-project>/`

1. In `/apps/<your-project>/` creare un nodo:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`

   Salva tutte le modifiche.

1. Copiare i file dei caratteri in questa cartella, ad esempio utilizzando WebDAV.

   >[!NOTE]
   >
   >I file di font nel repository devono avere il suffisso `*.ttf` o `*.TTF`.

1. Aggiorna la [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Aggiungere il percorso alla cartella dei caratteri, ovvero `/apps/<your-project>/fonts`.

1. Torna a CRXDE Lite. Nella cartella dovrebbe essere presente un nodo `.fontlist` contenente il nome dei caratteri importati.

   Questi font sono ora pronti per essere utilizzati nell’API Java.

Per informazioni dettagliate su come utilizzare i font con l&#39;API Java, consulta la [documentazione per la classe Font dell&#39;API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
