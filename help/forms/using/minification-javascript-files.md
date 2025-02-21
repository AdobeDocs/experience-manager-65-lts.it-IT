---
title: Minificazione dei file JavaScript
description: Istruzioni per generare codice ridotto dopo le personalizzazioni dell’area di lavoro di AEM Forms per ottimizzare i file JS per il web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# Minificazione dei file JavaScript {#minification-of-the-javascript-files}

La minimizzazione rimuove dal codice sorgente i caratteri ridondanti, come spazi vuoti, nuove righe e commenti. Questo migliora le prestazioni riducendo le dimensioni del codice. Anche se la minimizzazione non influisce sulla funzionalità, riduce la leggibilità del codice.

Per generare un codice minimizzato per le modifiche semantiche, segui la procedura riportata di seguito.

1. Copia `client-html/src/main/webapp/js` da src-package nel file system.

   >[!NOTE]
   >
   >Per ulteriori dettagli sui pacchetti, vedere [Introduzione alla personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md).

1. Aggiorna i percorsi in `main.js` che si trovano in client-html/src/main/webapp/js, per modelli/visualizzazioni aggiunti/aggiornati.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, cambia:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   A

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Aggiornare `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` in caso di modifica/aggiunta dell&#39;alias in `main.js`.

   Ad esempio, l&#39;aggiunta di un nuovo modello Sharequeue, ad esempio mySharequeue, cambia:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   A

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. In client-html/src/main/webapp/js/minifier, esegui il comando:

   ```shell
   mvn clean install
   ```

   Genera una cartella di file minimizzati, in client-html/src/main/webapp/js con main.js minimizzato e registry.js.

>[!NOTE]
>
>La minimizzazione funziona solo su una JVM a 64 bit.

>[!NOTE]
>
>Se minimizzi, l’aggiornamento è interessato.
