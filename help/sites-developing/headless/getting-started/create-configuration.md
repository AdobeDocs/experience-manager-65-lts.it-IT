---
title: Guida rapida alla creazione di una configurazione headless
description: Crea una configurazione come primo passaggio per iniziare a utilizzare headless in AEM 6.5.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: 6792f5c0-074e-4465-9b84-8be78abd6b8f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 66%

---

# Guida rapida alla creazione di una configurazione headless {#creating-configuration}

Come primo passo per iniziare a utilizzare le funzioni headless in AEM 6.5, devi creare una configurazione.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Il browser di configurazioni fornisce un’API di configurazione generica, una struttura del contenuto e un meccanismo di risoluzione per le configurazioni in AEM.

Nel contesto della gestione dei contenuti headless in AEM, considera una configurazione come un’area di lavoro all’interno di AEM dove puoi creare modelli di contenuto, che definiscono la struttura dei contenuti e dei frammenti di contenuto futuri. Puoi avere più configurazioni per separare questi modelli.

>[!NOTE]
>
>Se hai familiarità con i [modelli di pagina in un’implementazione completa di AEM,](/help/sites-authoring/templates.md) l’utilizzo delle configurazioni per la gestione dei modelli di contenuto è simile.

## Come creare una configurazione {#how-to-create-a-configuration}

Un amministratore deve creare una configurazione solo una volta oppure, molto raramente, se è necessaria una nuova area di lavoro per organizzare i modelli di contenuto. Ai fini di questa guida introduttiva, è sufficiente creare una sola configurazione.

1. Accedi ad AEM e dal menu principale seleziona **Strumenti > Generale > Browser configurazioni**.
1. Specifica un **Titolo** per la configurazione.
   * Un nome verrà generato automaticamente in base al titolo e regolato in base alle [convenzioni di denominazione di AEM.](/help/sites-developing/naming-conventions.md). Sarà il nome del nodo nell’archivio.
1. Seleziona le seguenti opzioni:
   * **Modelli per frammenti di contenuto**
   * **Query GraphQL persistenti**

   ![Crea configurazione](assets/create-configuration.png)

1. Fai clic su **Crea**.

Se necessario, puoi creare più configurazioni. È inoltre possibile nidificare le configurazioni.

>[!NOTE]
>
>In base ai requisiti di implementazione, oltre a **Modelli per frammenti di contenuto** e **Query GraphQL persistenti** potrebbe essere necessario selezionare anche altre opzioni di configurazione.

## Passaggi successivi {#next-steps}

Utilizzando questa configurazione, ora puoi passare alla seconda parte della guida introduttiva e [creare modelli per frammenti di contenuto.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
