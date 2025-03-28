---
title: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE
description: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE
contentOwner: khsingh
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
feature: Adaptive Forms,AEM Forms on OSGi
role: User, Developer
exl-id: d0f54236-5dc2-4c64-87c5-85e5e85e8cf7
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 20%

---

# Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Casella in entrata AEM e HTML Workspace {#aem-inbox-and-html-workspace}

Puoi utilizzare la Casella in entrata AEM per eseguire e monitorare i flussi di lavoro AEM incentrati su Forms su OSGi. Al contrario, HTML Workspace consente di eseguire e monitorare i flussi di lavoro JEE per AEM Forms. La tabella seguente ti aiuta a comprendere diverse azioni importanti disponibili nella Casella in entrata di AEM per i flussi di lavoro AEM incentrati su Forms su OSGi e nei flussi di lavoro HTML Workspace per AEM Forms JEE.

<table>
 <tbody>
  <tr>
   <td>Azioni</td>
   <td>Casella in entrata AEM</td>
   <td>HTML Workspace</td>
  </tr>
  <tr>
   <td>Avvio di un processo, un'attività o un'applicazione modulo<br /> </td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Invio di attività</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Assegnazione di un'attività a un gruppo</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Invio a più route</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Tracciamento cronologia e riepilogo attività</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Notifiche e-mail</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Riassegnazione delle attività</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Allegati a livello di campo per i moduli adattivi</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Vista calendario</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Commenti a livello di attività</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Code (coda personale condivisa, operazioni di richiesta di risarcimento dalla coda)</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Notifica fuori sede</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
    <tr>
   <td>Personalizzazione degli elementi dell’interfaccia utente</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Assegnazione di un'attività a più utenti</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
 </tbody>
</table>

## Flussi di lavoro di AEM incentrati su moduli su flussi di lavoro OSGi e AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

I flussi di lavoro AEM incentrati sui moduli su OSGi e i flussi di lavoro JEE per AEM Forms (AEM Forms su JEE Process Management) presentano una serie diversa di funzionalità. La tabella seguente consente di comprendere le funzionalità importanti disponibili nei flussi di lavoro AEM basati su moduli su OSGi e in AEM Forms su flussi di lavoro JEE:

<table>
 <tbody>
  <tr>
   <td>Funzionalità</td>
   <td>Flussi di lavoro AEM incentrati su moduli su OSGi<br /> </td>
   <td>Flussi di lavoro di AEM Forms JEE</td>
  </tr>
  <tr>
   <td>Moduli adattivi</td>
   <td>Funzione supportata</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Integrazione con altre soluzioni AEM</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma a mano</td>
   <td>Funzione supportata</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Modelli e-mail personalizzati</td>
   <td>Funzione supportata</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Definizione della priorità dell'attività</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Esegui il timeout di un'attività dopo la data di scadenza</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Loop all'interno del flusso di lavoro</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Selezione dinamica di un assegnatario </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Utilizzo di metadati personalizzati</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma elettronica (Adobe Sign)</td>
   <td>Supportato <sup>[1]</sup></td>
   <td>Supportato <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gestione di applicazioni task e form</td>
   <td>Supportato <sup>[2]</sup><br /> </td>
   <td>Supportato <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Document Services</td>
   <td>Supportato <sup>[3]</sup></td>
   <td>Supportato <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Rendering dell’attività completata come modulo adattivo o documento PDF</td>
   <td>Funzione supportata</td>
   <td>Supportati [4]</td>
  </tr>
  <tr>
   <td>Integrazione con Gestione della corrispondenza</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
   <tr>
   <td>Gateway , NESSUNA ATTESA </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
   <tr>
   <td>Variabili per archiviare i dati </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>O, E Divisione</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Avatar utente</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Invia un messaggio e-mail alla fine del flusso di lavoro</td>
   <td>Supportato <sup>[7]</sup></td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Chiamare un servizio Web da un flusso di lavoro</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Fasi del flusso di lavoro</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Moduli adattivi di sola lettura</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Nascondere il pulsante di salvataggio predefinito</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Sezione Controllo granulare sui dettagli del flusso di lavoro</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Servizio di polling/pianificazione</td>
   <td>Disponibile con il prodotto</td>
   <td>Implementazione personalizzata richiesta</td>
  </tr>
  <tr>
   <td>App Forms adattiva</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio assemblatore</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio PDF Generator</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio Forms</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio di output</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Document Assurance</td>
   <td>Supportato</td>
   <td>Supportato </td>
  </tr>
  <tr>
   <td>Esegui script</td>
   <td>Supporta ECMAScript</td>
   <td>Supporta snippet di codice Java</td>
  </tr>
  <tr>
   <td>Assemblatore</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>  
  <tr>
   <td>HTML5 Forms, PDF forms interattivo, set di moduli</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Reporting processi</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Categorie punto d'inizio</td>
   <td>Non supportato </td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Approvazione attività in blocco </td>
   <td>Non supportato </td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Salva bozza con un nome personalizzato</td>
   <td>Non supportato </td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Avvia un processo con dati processo esistenti<br /> </td>
   <td>Non supportato</td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Salvataggio di un punto d'inizio come bozza</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Vista Manager</td>
   <td>Non supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Cerca modelli</td>
   <td>Non supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Integrazione con applicazioni di terze parti</td>
   <td><sup>[6]</sup> non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Allegati a livello di attività per l'applicazione del flusso di lavoro o il punto d'inizio</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>E-mail promemoria</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Cambia titolo in caso di timeout attività</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>E-mail su delega attività e attestazione attività</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Delega tra gruppi disgiunti</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Trasformazione XSLT</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Priorità attività dinamica</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Titolo dinamico</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
    <tr>
   <td>Descrizione dinamica</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
 </tbody>
</table>

1. Per firmare un modulo adattivo compilato, puoi utilizzare i flussi di lavoro AEM incentrati sui moduli su OSGi. I flussi di lavoro AEM incentrati sui moduli su OSGi supportano la firma out-of-the-form. L&#39;esperienza di [firma in-form](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) non è supportata.

1. Per eseguire e monitorare i flussi di lavoro basati su moduli su AEM Forms OSGi e HTML Workspace AEM Forms, è necessario accedere alla casella in entrata di AEM.
1. I servizi documentali AEM Forms nativi sono disponibili per i flussi di lavoro AEM incentrati su moduli su OSGi e per i flussi di lavoro AEM Forms su JEE. AEM Workflow utilizza servizi di documenti nativi per flussi di lavoro AEM incentrati su moduli in flussi di lavoro OSGi e AEM Forms JEE (Process Management).
1. I flussi di lavoro AEM Forms JEE possono eseguire il rendering solo di un modulo adattivo. Non supporta il rendering di un modulo adattivo come documento PDF.
1. I flussi di lavoro di AEM Forms JEE non dispongono di un passaggio separato per Adobe Sign. È necessario un modulo adattivo abilitato per Adobe Sign per i flussi di lavoro JEE per AEM Forms. Per ulteriori dettagli, consulta la [documentazione di Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. È possibile utilizzare il passaggio [Richiama servizio modello dati modulo](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) per richiamare un servizio Web e inviare o recuperare dati da un&#39;applicazione di terze parti.
1. Puoi utilizzare il passaggio [Invia e-mail](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) per inviare e-mail.

## Differenze tra la casella in entrata di AEM e le funzioni dell’app AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei modi principali per avviare un flusso di lavoro incentrato su Forms sono l&#39;utilizzo di [Posta in arrivo AEM](../../forms/using/manage-applications-inbox.md) e dell&#39;app AEM Forms. Tuttavia, le funzionalità della casella in entrata di AEM e dell’app AEM Forms sono diverse. La casella in entrata di AEM funziona solo con [flussi di lavoro incentrati su Forms](../../forms/using/aem-forms-workflow.md), mentre l&#39;app AEM Forms funziona sia con flussi di lavoro incentrati su Forms che con la gestione dei processi.

Nella tabella seguente sono elencate le funzionalità della casella in entrata di AEM e dell’app AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Azioni</strong></p> </td>
   <td><p><strong>Casella in entrata AEM</strong></p> </td>
   <td><p><strong>App AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Avvio di un'applicazione modulo</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Invio di attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Delega di attività</p> </td>
   <td><p>Funzione supportata</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Tracciamento cronologia e riepilogo attività</p> </td>
   <td><p>Funzione supportata</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di allegati a livello di attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione degli allegati a livello di task</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di allegati a livello di campo</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione del calendario</p> </td>
   <td><p>Funzione supportata</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di commenti</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
 </tbody>
</table>
