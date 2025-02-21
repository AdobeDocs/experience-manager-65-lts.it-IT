---
title: Utilizzo dei punti d'inizio
description: Passaggi per lavorare con un processo Adobe Experience Manager Forms dal dispositivo mobile definito in Workbench.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Utilizzo dei punti d&#39;inizio{#working-with-startpoints}

Un punto iniziale richiama un processo creato in Workbench. È associata a un modulo che richiama il processo quando il modulo viene inviato.

>[!NOTE]
>
>I termini punti iniziali, processo iniziale e modulo vengono utilizzati in modo intercambiabile quando si fa riferimento a questo concetto.

Per avviare un processo dall&#39;app Adobe Experience Manager (AEM) Forms, devi avere un punto d&#39;inizio di tipo **Workspace** nel processo. È inoltre necessario selezionare l&#39;opzione **[!UICONTROL Visibile in Mobile Workspace]** per il punto iniziale.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Per avviare un processo definito in Workbench**

1. Per visualizzare i punti iniziali disponibili nell&#39;app AEM Forms, vai alla [schermata iniziale](../../forms/using/home-screen.md).
1. Nella schermata **[!UICONTROL Home]**, per impostazione predefinita, viene visualizzato l&#39;elenco **[!UICONTROL All Forms]**.

   Il punto iniziale è associato a un modulo. Selezionare il modulo associato al punto d&#39;inizio nell&#39;elenco per aprirlo.

   Viene aperto il modulo associato al punto d&#39;inizio.

1. Immetti i dettagli nel modulo **[!UICONTROL Startpoint]**.

   Puoi aggiungere annotazioni a questa attività utilizzando il pulsante [allegato](../../forms/using/add-attachments.md).

1. Dopo aver compilato il modulo, seleziona il pulsante **[!UICONTROL Invia]**.

Se l&#39;app non è in linea, il modulo e i relativi dati vengono salvati nella cartella Posta in uscita.

Se l&#39;app è online, l&#39;attività viene sincronizzata con il server AEM Forms e assegnata all&#39;utente specificato nel processo.

Per utilizzare l&#39;attività nell&#39;elenco delle attività, vedere [Apertura di un&#39;attività](/help/forms/using/open-task.md).
