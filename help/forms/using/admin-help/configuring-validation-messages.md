---
title: Configurazione dei messaggi di convalida
description: Scopri come specificare la modalità di visualizzazione dei messaggi di convalida e la loro posizione rispetto al modulo restituito nel browser web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1172f1f2-b297-4021-a9ee-507b0a4e628a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# Configurazione dei messaggi di convalida {#configuring-validation-messages}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Per i moduli sottoposti a rendering come HTML, gli errori di convalida dei moduli che si verificano vengono visualizzati per l’utente. È possibile personalizzare la visualizzazione dei messaggi di convalida. A seconda della posizione in cui vengono visualizzati i messaggi di convalida, è inoltre possibile controllare la posizione del messaggio nel modulo e le dimensioni del bordo del frame.

## Specificare la modalità di visualizzazione dei messaggi di convalida {#specify-how-validation-messages-are-displayed}

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. In Output di convalida, nell&#39;elenco Reporting, selezionare una delle opzioni seguenti:

   **Finestra di messaggio:** Per visualizzare i messaggi di convalida in una finestra di dialogo separata.

   **Frame:** Per visualizzare i messaggi di convalida in un frame della stessa finestra.

   **Nessun frame:** Per visualizzare i messaggi di convalida nella stessa finestra. Questo valore è quello predefinito.

   **Tramite API (con dati):** Per restituire i messaggi di convalida tramite API (con dati). I messaggi di convalida non vengono visualizzati sullo schermo.

   **Tramite API (con modulo):** Per restituire i messaggi di convalida tramite l&#39;API (con il modulo). I messaggi di convalida non vengono visualizzati sullo schermo.

   **Nessuno:** Per non visualizzare i messaggi di convalida.

1. Fai clic su Salva.

## Specificare il percorso dei messaggi di convalida relativi al modulo restituito nel browser Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Quando Reporting è impostato su Frame o su No Frame, è possibile specificare la posizione dei messaggi di convalida.

1. In Output di convalida, nell&#39;elenco Posizione, selezionare una delle opzioni seguenti:

   **Sinistra:** per visualizzare i messaggi di convalida sul lato sinistro del browser Web.

   **Destra:** Per visualizzare i messaggi di convalida sul lato destro del browser Web.

   **Top**: per visualizzare i messaggi di convalida nella parte superiore del browser Web. Questo valore è quello predefinito.

   **Inferiore**: per visualizzare i messaggi di convalida nella parte inferiore del browser Web.

1. Fai clic su Salva.

## Specificare la dimensione del bordo del frame {#specify-the-frame-border-size}

Quando Reporting è impostato su Frame, è possibile specificare la dimensione del bordo del frame.

1. In Output di convalida digitare le dimensioni in pixel del bordo del frame nella casella Dimensione bordo.

   La dimensione del bordo deve essere uguale o maggiore di 0. Il valore predefinito è 1.

1. Fai clic su Salva.
