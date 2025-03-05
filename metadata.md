---
product: adobe experience manager
description: Documentazione di Adobe Experience Manager 6.5 LTS.
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.it-IT
hide: y
type: Documentation
solution: Experience Manager
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 59969e1e669f6aef3f0d480b5dbdad0bdf28a1d7
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 52%

---


# Metadati per uso interno

I metadati nel sistema di authoring GitHub sono gerarchici e vengono definiti in base ai seguenti livelli crescenti di precedenza.

1. metadata.md
1. Sommario
1. Articolo

I metadati definiti nel file metadata.md si applicano all’intero archivio, ma possono essere ignorati a livello di sommario e articolo. Eventuali esclusioni dei metadati devono essere eseguite al livello più basso possibile.

I metadati nell’archivio experience-manager-cloud-service.en sono il minimo richiesto.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

Sommario

* `sub-product`
* `user-guide-title`

Articolo

* `title`
* `description`
* `contentOwner` (solo sul contenuto della risorsa principale in `/help/assets`)
