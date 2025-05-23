---
title: Visualizzazione di dati aggiuntivi nell'elenco Da fare
description: Personalizzare la visualizzazione dell'elenco attività dell'area di lavoro AEM Forms LiveCycle per visualizzare ulteriori informazioni oltre a quelle predefinite.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 988e986f-8e0b-48a2-a529-9c0f931131b9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Visualizzazione di dati aggiuntivi nell&#39;elenco Da fare{#displaying-additional-data-in-todo-list}

Per impostazione predefinita, nell’elenco Da fare dell’area di lavoro di AEM Forms vengono visualizzati il nome visualizzato e la descrizione dell’attività. Tuttavia, puoi aggiungere altre informazioni quali la data di creazione e la data di scadenza. È inoltre possibile aggiungere icone e modificare lo stile della visualizzazione.

![Scheda Da fare di HTML Workspace con la configurazione predefinita](assets/html-todo-list.png)

Questo articolo descrive i passaggi per aggiungere informazioni da visualizzare per ogni attività nell&#39;elenco Da fare.

## Cosa è possibile aggiungere {#what-can-be-added}

È possibile aggiungere le informazioni disponibili in `task.json` inviate dal server. Le informazioni possono essere aggiunte come testo normale oppure è possibile utilizzare gli stili per formattarle.

Per ulteriori informazioni sulla descrizione dell&#39;oggetto JSON, vedi l&#39;articolo [this](/help/forms/using/html-workspace-json-object-description.md).

## Visualizzazione delle informazioni su un&#39;attività {#displaying-information-on-a-task}

1. Segui i [passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).
1. Per visualizzare informazioni aggiuntive per un&#39;attività, è necessario aggiungere le coppie chiave-valore corrispondenti nel blocco attività di `translation.json`.

   Ad esempio, cambia `/apps/ws/locales/en-US/translation.json` per l&#39;inglese:

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >Aggiungi coppie chiave-valore corrispondenti per tutte le lingue supportate.

1. Ad esempio, aggiungi informazioni all’interno del blocco di attività:

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## Definizione di CSS per la nuova proprietà {#defining-css-for-the-new-property}

1. È possibile applicare uno stile alle informazioni (proprietà) aggiunte a un&#39;attività. A tale scopo, è necessario aggiungere le informazioni sullo stile per la nuova proprietà aggiunta a `/apps/ws/css/newStyle.css`.

   Ad esempio, aggiungi:

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## Aggiunta di una voce nel modello HTML {#adding-entry-in-the-html-template}

Infine, è necessario includere una voce nel pacchetto di sviluppo per ogni proprietà che si desidera aggiungere all&#39;attività. Per crearne uno, consulta Creazione del codice dell’area di lavoro di AEM Forms.

1. Copia `task.html`:

   * da: `/libs/ws/js/runtime/templates/`
   * a: `/apps/ws/js/runtime/templates/`

1. Aggiungere le nuove informazioni a `/apps/ws/js/runtime/templates/task.html`.

   Ad esempio, aggiungi in `div class="taskProperties"`:

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
