---
title: Insidie del codice
description: Insidie di codifica comuni da evitare durante lo sviluppo per AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 95656312-2648-455e-80fb-3e03bf1cd633
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Insidie del codice{#code-pitfalls}

## Evitare le associazioni Sling nel codice Java {#avoid-sling-bindings-in-java-code}

Le associazioni Sling rappresentano un modo inappropriato per accedere a un servizio nel 90% dei casi. È invece necessario utilizzare *@Reference* o *@Inject* annotazioni.

## Evitare Thread.interrupt nel codice Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* è pericoloso perché può chiudere i file, inclusi i file Lucene e i file di cache persistenti, se chiamati al momento sbagliato.

## Evitare di combinare la sincronizzazione Java con ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Questo può portare a una situazione di tipo &quot;race condition&quot; in cui il codice alla fine si blocca.
