---
title: Personalizzazione delle schede per un’attività
description: Come personalizzare i nomi delle schede per le attività, nell’area di lavoro di AEM Forms LiveCycle.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 88f5093c-f249-4e4b-900a-5897f47e513c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Personalizzazione delle schede per un’attività {#customizing-tabs-for-a-task}

È possibile personalizzare i nomi delle schede per il componente `Start Process` nella visualizzazione Uber `Start Process` e il componente `Task Details` nella visualizzazione Uber `ToDo`.

1. Segui i [passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Modificare il valore di `tabname` nel file `translation.json`.

   Modificare ad esempio `/apps/ws/locales/en-US/translation.json` per l&#39;inglese nel modo seguente.

   * Per le attività avviate nel processo di avvio, utilizzare lo snippet seguente del blocco `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Per le attività in Da fare, utilizzare lo snippet seguente del blocco `"todo" : {}`.

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >Aggiungi una coppia chiave-valore corrispondente per tutte le lingue supportate.
