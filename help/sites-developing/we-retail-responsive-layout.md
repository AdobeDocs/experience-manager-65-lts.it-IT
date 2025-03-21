---
title: Prova del layout dinamico in We.Retail
description: Scopri come provare il layout dinamico in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 25e035ce-0445-43a3-bd75-513a2e601b6a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 9%

---

# Prova del layout dinamico in We.Retail{#trying-out-responsive-layout-in-we-retail}

Tutte le pagine We.Retail utilizzano il componente Contenitore di layout per implementare una progettazione reattiva. Il contenitore layout fornisce un sistema paragrafo che consente di posizionare i componenti all’interno di una griglia reattiva. Questa griglia può ridisporre il layout in base alle dimensioni e al formato del dispositivo o della finestra. Il componente viene utilizzato insieme alla modalità **Layout** nell&#39;editor pagina, che consente di creare e modificare il layout dinamico in base al dispositivo.

## Prova {#trying-it-out}

1. Modifica la pagina Arctic Surfing nella sezione Esperienze del ramo principale lingua.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Passa a **Anteprima** per visualizzare la pagina così come verrebbe visualizzata da un visitatore del sito Web. Scorri verso il basso fino al contenuto dell&#39;articolo *Aloha spirits in Norther Norway*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Ridimensiona la finestra del browser e osserva come il layout si adatta dinamicamente al ridimensionamento.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Passa alla modalità Layout. La barra degli strumenti dell’emulatore viene visualizzata automaticamente e consente di pianificare il layout per dispositivo di destinazione.

   Selezionando un componente vengono visualizzate le opzioni mobile e nascosta nel menu Modifica insieme alle maniglie di ridimensionamento del componente.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. Se si trascina il quadratino di ridimensionamento del componente, viene visualizzata automaticamente la griglia di layout che consente di ridimensionarlo.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, vedere il documento di creazione [Layout reattivo](/help/sites-authoring/responsive-layout.md) o il documento dell&#39;amministratore [Configurazione del contenitore di layout e della modalità di layout](/help/sites-administering/configuring-responsive-layout.md) per informazioni tecniche complete.
