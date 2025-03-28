---
title: Recupero variabili attività nell’URL di riepilogo
description: Riutilizzare le informazioni su un'attività e generare un URL di riepilogo per riepilogare o descrivere un'attività.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 1cd2aae7-306f-4f7a-b4d2-e8c64827c09a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Recupero variabili attività nell’URL di riepilogo {#getting-task-variables-in-summary-url}

Nella pagina di riepilogo vengono visualizzate le informazioni relative all&#39;attività. Questo articolo descrive come riutilizzare le informazioni relative alle attività nella pagina di riepilogo.

In questa orchestrazione di esempio, un dipendente invia un modulo di richiesta di congedo. Il modulo di domanda viene quindi inviato al responsabile del dipendente per l&#39;approvazione.

1. Creare un modulo di rendering HTML di esempio (html.esp) per resourseType **Dipendenti/PtoApplication**.

   Il renderer presuppone che le seguenti proprietà siano impostate sul nodo:

   * ename
   * empid
   * motivo
   * durata

   >[!NOTE]
   >
   >Questo renderer è il modello della pagina di riepilogo.

   Il seguente codice di esempio per questo renderer è contenuto in:

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Modifica l’orchestrazione per estrare le quattro proprietà dai dati del modulo inviati. In seguito, creare un nodo in CRX di tipo **Dipendenti/PtoApplication**, con le proprietà popolate.

   1. Crea un processo **crea riepilogo PTO** e utilizzalo come processo secondario prima dell&#39;operazione **Assegna attività** nell&#39;orchestrazione.
   1. Definisci **employeeName**, **employeeID**, **ptoReason**, **totalDays** e **nodeName** come variabili di input nel nuovo processo. Queste variabili verranno trasmesse come dati del modulo inviati.

      Definisci anche una variabile di output **ptoNodePath** utilizzata durante l&#39;impostazione dell&#39;URL di riepilogo.

   1. Nel processo **crea riepilogo PTO**, utilizzare il componente **imposta valore** per impostare i dettagli di input in una mappa **nodeProperty**(**nodeProps**).

      Le chiavi in questa mappa devono essere identiche a quelle definite nel renderer HTML nel passaggio precedente.

      Aggiungere inoltre una chiave **sling:resourceType** con il valore **Employees/PtoApplication** nella mappa.

   1. Utilizzare il processo secondario **storeContent** dal servizio **ContentRepositoryConnector** nel processo **create PTO summary**. Questo processo secondario crea un nodo CRX.

      Sono necessarie tre variabili di input:

      * **Percorso cartella**: il percorso in cui viene creato il nuovo nodo di CRX. Imposta il percorso come **/content**.
      * **Nome nodo**: assegnare la variabile di input nodeName a questo campo. Questa è una stringa con nome di nodo univoco.
      * **Tipo di nodo**: definire il tipo come **nt:unstructured**. L&#39;output di questo processo è nodePath. Il percorso nodePath è il percorso CRX del nodo appena creato. Il ndoePath è l&#39;output finale del processo di riepilogo **create PTO**.

   1. Passa i dati del modulo inviati (**employeeName**, **employeeID**, **ptoReason** e **totalDays**) come input per il nuovo processo **crea riepilogo PTO**. Considera l&#39;output come **ptoSummaryNodePath**.

1. Definisci l&#39;URL di riepilogo come espressione XPath contenente i dettagli del server insieme a **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Nell’area di lavoro di AEM Forms, quando apri un’attività, l’URL di riepilogo accede al nodo CRX e il renderer HTML visualizza il riepilogo.

Il layout del riepilogo può essere modificato senza modificare il processo. Il renderer HTML visualizza il riepilogo in modo appropriato.
