---
title: Struttura della gestione multisito per contenuti di destinazione
description: Un diagramma mostra come è strutturato il supporto multisito per contenuti mirati
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
exl-id: 435fcee8-ddb4-4b3c-a55f-fca1b91b7d52
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 38%

---

# Struttura della gestione multisito per contenuti di destinazione{#how-multisite-management-for-targeted-content-is-structured}

Il diagramma seguente mostra come è strutturato il supporto multisito per contenuti di destinazione.

Le aree vengono visualizzate al di sotto di **/content/campaigns/&lt;brand>** e, per impostazione predefinita, ogni marchio ha un’area master che viene creata automaticamente. Ogni area contiene la propria serie di attività, esperienze e offerte.

![chlimage_1-268](assets/chlimage_1-268.png)

Per cercare contenuti mirati, le pagine o i siti possono essere mappati su un’area. Se non è configurata alcuna area, AEM torna all’area master per questo marchio specifico.

Il diagramma seguente è un esempio di come funziona la logica per tre siti, denominati site1, site2 e site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 cerca myarea1 per brand1 e otherarea2 per brand2 in base alla mappatura dell’area.
* site2 cerca myarea1 per brand1 e master area per brand2 in quanto viene definita solo la mappatura di area per brand1.
* site3 cerca l’area master per brand1 e brand2 in quanto per questo sito non è definita alcuna altra mappatura di area.
