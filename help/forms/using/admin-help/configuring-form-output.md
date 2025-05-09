---
title: Configurazione dell’output del modulo
description: Scopri come configurare l’output del modulo. Per configurare l’output del modulo e abilitare questa funzione, utilizza gli script personalizzati prima dell’invio del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2823d38e-f544-408e-9437-3d0fc622dc34
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# Configurazione dell’output del modulo{#configuring-form-output}

## Specifica il tipo di output HTML restituito al browser Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. Nell&#39;elenco Tipo di output della casella di gruppo Output modulo selezionare una delle opzioni seguenti:

   **Full HTML:** per eseguire il rendering del modulo in tag HTML completi (una pagina HTML completa). Questo valore è quello predefinito.

   **Corpo modulo:** Per eseguire il rendering del modulo entro `<BODY>` tag (non una pagina HTML completa).

1. Fai clic su Salva.

## Specifica il percorso in cui viene eseguito il rendering del contenuto PDF {#specify-the-location-where-pdf-content-is-rendered}

1. In Output modulo, nell&#39;elenco Rendering a (Render at), selezionate una delle seguenti opzioni:

   **Client:** Per eseguire il rendering di PDF forms in Adobe Acrobat o Adobe Reader. Il rendering lato client migliora le prestazioni dei moduli AEM e si applica solo alla trasformazione dei moduli PDFF.

   **Server:** Per eseguire il rendering di PDF forms nel server applicazioni.

   **Auto:** per eseguire il rendering del modulo PDF nel percorso specificato dal valore di configurazione `dynamicRender` del file XDP. Questo valore è quello predefinito.

1. Fai clic su Salva.

## Configurazione della chiamata di script personalizzati prima dell’invio del modulo {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Per abilitare la funzione, effettua le seguenti operazioni:

1. Accedi alla console di amministrazione.
1. Vai a **Servizi** > **Moduli**.
1. Specificate il tipo di output come corpo del modulo.
1. Salva le impostazioni.
1. Dichiara una variabile JavaScript, __CUSTOM_SCRIPTS_VERSION, nella sezione head del codice HTML e impostane il valore su 1.

   >[!NOTE]
   >
   >*Per disattivare la funzionalità, è possibile rimuovere la variabile JavaScript o impostarne il valore su 0.*
