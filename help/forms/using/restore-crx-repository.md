---
title: Impossibile ripristinare l’archivio CRX danneggiato applicabile al server cluster JEE
description: Scopri come ripristinare un archivio CRX danneggiato.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 716d8eb2-2010-4d55-b8fe-bd4f6f256a4d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# Impossibile ripristinare l’archivio CRX danneggiato {#unable-to-restore-corrupt-crx-repository}

## Problema   {#issue}

Per AEM Forms su JEE che utilizza un database relazionale, il tempo sul computer che ospita AEM Forms e il database relazionale deve sempre essere sincronizzato in modo assoluto. Se l’ora su questi computer non è sincronizzata, l’archivio CRX di AEM Forms sul server JEE può diventare inaccessibile. Potrebbe apparire danneggiato e diventare inaccessibile tramite URL. Errore `AuthenticationsupportService missing` registrato.

## Prerequisiti {#prerequisites}

Esegui il backup dell’archivio CRX prima di eseguire i passaggi indicati di seguito.

## Soluzione {#solution}

1. Vai a `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Individuare il bundle `oak-core` e verificare che sia in esecuzione.

1. Riavviare il bundle `oak-core` se non è in esecuzione. Se l&#39;icona ![Pause button](/help/forms/using/assets/stop.png) è presente davanti al bundle `oak-core`, indica che il bundle è in esecuzione.

1. Se il problema non è ancora stato risolto, eseguire il ripristino dall&#39;archivio CRX dal backup o ricreare l&#39;archivio CRX se il backup non è disponibile.


## Si applica a {#applies-to}

Questa soluzione si applica ad AEM Forms su cluster JEE.
