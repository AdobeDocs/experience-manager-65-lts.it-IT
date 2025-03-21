---
title: ContextHub
description: ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: c7c42bcd-d90a-430a-bbcd-b104d0670ebf
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali. L’API JavaScript lato client ti consente di accedere ai dati per personalizzare il contenuto.

>[!NOTE]
>
>L&#39;implementazione di riferimento [We.Retail](/help/sites-developing/we-retail.md) implementa ContextHub e può fungere da riferimento durante l&#39;integrazione di ContextHub nel progetto.

>[!CAUTION]
>
>Il percorso contenente la configurazione ContextHub di esempio utilizzata dall&#39;implementazione di riferimento [We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) deve essere utilizzato solo come riferimento per la creazione di una configurazione personalizzata.
>
>Non utilizzare in un progetto come configurazione ContextHub personalizzata.

## Persistenza {#persistence}

ContextHub archivia i dati contestuali persistenti sul client. L’API JavaScript di ContextHub consente di accedere agli store per creare, aggiornare ed eliminare i dati in base alle esigenze. ContextHub rappresenta un livello dati sulle pagine.

Ogni archivio ContextHub è un’istanza di un tipo di archivio predefinito:

* ContextHub fornisce diversi [tipi di archivio di esempio](/help/sites-developing/ch-samplestores.md).
* Usa le console AEM per [creare store](ch-configuring.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di archivio personalizzati](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accedere ai dati dell&#39;archivio](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) tramite JavaScript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi usare l&#39;API JavaScript per [determinare i segmenti risolti](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentazione {#presentation}

La barra degli strumenti [ContextHub](/help/sites-authoring/ch-previewing.md) consente agli addetti al marketing e agli autori di visualizzare e manipolare i dati dell&#39;archivio per simulare l&#39;esperienza utente durante la creazione delle pagine. La barra degli strumenti è costituita da gruppi di moduli di interfaccia utente che forniscono accesso agli store ContextHub.

Ogni modulo dell’interfaccia utente ContextHub è un’istanza di un tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](/help/sites-developing/ch-samplemodules.md).
* Usa le console di AEM per [aggiungere moduli di interfaccia utente](ch-configuring.md#adding-a-ui-module) e per [raggrupparli in modalità interfaccia utente](ch-configuring.md#adding-a-ui-mode).

* Gli sviluppatori possono [creare tipi di moduli personalizzati](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono [aggiungere il componente ContextHub alla pagina](/help/sites-developing/ch-adding.md).
