---
title: Convenzioni di denominazione per il test delle risorse
description: I nodi nell’archivio sono soggetti alle convenzioni di denominazione dell’archivio dei contenuti Java. Tuttavia, Adobe Experience Manager impone ulteriori convenzioni per il nome dei nodi delle risorse.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 1%

---

# Convenzioni di denominazione per il test delle risorse{#naming-conventions-for-assets-testing}

I nodi dell&#39;archivio sono soggetti alle convenzioni di denominazione dell&#39;[archivio dei contenuti Java](/help/sites-developing/the-basics.md#java-content-repository). Tuttavia, Adobe Experience Manager impone ulteriori convenzioni per il nome dei nodi delle risorse.

## Interfaccia classica {#classic-ui}

L’interfaccia utente classica impone restrizioni più severe:

* Convalida il nome della risorsa quando un nome di nodo esplicito:

   * viene fornito il titolo della risorsa da convertire nel nome del nodo
   * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una risorsa viene creata dall’interfaccia classica):

   * Da &#39;a&#39; a &#39;z&#39;
   * Da &#39;A&#39; a &#39;Z&#39;
   * Da &#39;0&#39; a &#39;9&#39;
   * _ (trattino basso)
   * `-` (trattino/segno meno)
