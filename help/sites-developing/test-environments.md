---
title: Quali ambienti di test sono necessari?
description: Diversi ambienti devono essere considerati parte del test
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: f74fbf2b-62bb-4fac-9ecb-5ace90ba0275
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Quali ambienti di test sono necessari?{#which-test-environments-will-be-needed}

Per definire le configurazioni da testare, prendi in considerazione quanto segue:

**Sviluppo** - Per unit test e alcuni Integration test.

**Test** - Per la maggior parte dei test.

**Live** - Per le prestazioni finali e gli stress test. Anche per i test di accettazione con il cliente.

Decidi quali istanze sono necessarie e dove (in genere almeno una per ogni livello di test):

**Autore** - Questa istanza consente agli autori di inserire e pubblicare contenuti.

**Pubblicazione** - Questa istanza presenta il sito Web nel relativo modulo pubblicato per l&#39;accesso da parte dei visitatori.

Testato con Dispatcher.

Infine, è necessario considerare l&#39;hardware effettivo: tutti i test delle prestazioni devono essere eseguiti su un sistema il più vicino possibile all&#39;ambiente live finale. Per questo motivo, si consiglia inoltre di suddividere il lancio del progetto in:

**Lancio morbido** - Disponibilità ridotta, che consente di eseguire test delle prestazioni, ottimizzare e ottimizzare in condizioni realistiche l&#39;ambiente di produzione.

**Lancio rigido** - Disponibilità completa.
