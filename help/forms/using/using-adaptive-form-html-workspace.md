---
title: Utilizzo di un modulo adattivo in HTML Workspace
description: Scopri come utilizzare un modulo adattivo in HTML Workspace che consente ai lavoratori dei campi di accedere al modulo sui loro dispositivi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench
role: User, Developer
exl-id: 3fdd889d-0984-457e-9b12-b55a4593a573
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Utilizzo di un modulo adattivo in HTML Workspace{#using-an-adaptive-form-in-html-workspace}

AEM Forms su JEE consente di utilizzare un modulo adattivo in HTML Workspace.

Poiché è possibile selezionare un XDP durante la progettazione del processo, è stata aggiunta la possibilità di sfogliare da un archivio AEM di un modulo adattivo esistente. Questa funzionalità consente a Process Designer di configurare un modulo adattivo in Start Point e in Task.

## Esperienza di progettazione del processo {#process-design-experience}

Per abilitare i moduli adattivi da utilizzare nella progettazione dei processi, effettua le seguenti operazioni:

* In Assegna attività e punto iniziale è possibile passare a una risorsa di modulo adattivo nell’archivio CRX quando si assegna una risorsa di modulo a un’attività.
* Nel foglio delle proprietà Assegna attività/Punto iniziale del workbench è possibile nascondere la barra degli strumenti globale/di primo livello di un modulo adattivo.
* Puoi utilizzare nuovi profili di azione per le azioni Rendering e Invio nei moduli adattivi.

### Esportazione e importazione di applicazioni LiveCycle {#livecycle-application-export-and-import}

Poiché i moduli adattivi si trovano nell’archivio di AEM, l’esportazione dell’applicazione LiveCycle contiene solo i riferimenti per i moduli adattivi utilizzati. Pertanto, l&#39;esportazione e l&#39;importazione dell&#39;applicazione LiveCycle è un processo in due fasi. L&#39;applicazione LiveCycle include definizioni di processo e così via. Un pacchetto separato contenente moduli adattivi viene esportato da AEM come file ZIP. Durante l’importazione, l’applicazione LiveCycle viene importata tramite Workbench, mentre i moduli adattivi vengono importati tramite AEM.

## Esperienza utente del modulo adattivo in HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

HTML Workspace fornisce alcuni controlli specifici per i moduli adattivi, oltre ai controlli disponibili per i moduli mobili. Quando un utente apre un’attività o un punto iniziale, può aggiungere allegati, salvare, firmare, inviare e navigare nei moduli adattivi in HTML Workspace. Di seguito sono riportate le specifiche:

1. Per allegare i file, utilizza gli allegati delle attività, come in Mobile Forms. Qualsiasi pulsante di tipo File allegato di un modulo adattivo è nascosto.

1. Per salvare un modulo adattivo, fai clic su **Salva**, come in Mobile Forms. Qualsiasi pulsante Salva tipo di modulo adattivo è nascosto.

1. Per inviare un modulo adattivo, utilizza il pulsante **Invia** o instrada le azioni disponibili, come in Mobile Forms. Qualsiasi pulsante Invia tipo di modulo adattivo è nascosto.

1. **Visibilità barra degli strumenti globale modulo adattivo**: se in Process Designer la barra degli strumenti globale/di primo livello viene nascosta, la barra degli strumenti e i pulsanti non vengono visualizzati nei moduli adattivi.

1. **Controlli di navigazione di Workspace per Forms adattivo**: i pulsanti Avanti/Indietro sono disponibili insieme ai pulsanti Salva, Invia e Instrada azione per un modulo adattivo in HTML Workspace. Fai clic sui pulsanti Successivo/Precedente per passare ai pannelli dei moduli adattivi in HTML Workspace. I pulsanti Successivo/Precedente offrono una navigazione approfondita, simile ai controlli di navigazione nella visualizzazione Mobile dei moduli adattivi.

1. **Servizi eSign e componente di riepilogo del modulo adattivo**: il componente Riepilogo non è operativo in HTML Workspace. In altre parole, un modulo adattivo con un componente Riepilogo non è visibile nell’area di lavoro. Invece di eseguire l’invio automatico nel componente E-sign, l’utente dell’area di lavoro fa clic sull’azione Invia o su un’azione di instradamento in HTML Workspace. Dopo la firma, un documento è visibile come documento con firma semplice. Fai clic su **Invia** o su un&#39;azione di instradamento per chiudere/completare l&#39;attività o il punto iniziale.\
   Il documento firmato viene raccolto dal server eSign Services e il file XML dati viene inoltrato al passaggio successivo del processo.

## Passaggi per utilizzare i moduli adattivi nella progettazione dei processi {#steps-to-use-adaptive-forms-in-process-design}

1. Apri Adobe Experience Manager Forms Workbench.

1. Vai a **File > Nuovo > Applicazione** oppure utilizza l&#39;applicazione esistente per creare un&#39;applicazione.

   ![Crea nuova applicazione](assets/create_new_appl.png)

   Crea applicazione

1. Creare un processo o utilizzare un processo esistente nell&#39;applicazione.

   ![Crea nuovo processo](assets/create_new_process.png)

   Crea processo

1. Creare un punto iniziale o assegnare un&#39;attività e fare doppio clic su di essa.
1. Nella sezione **[!UICONTROL Presentazione e dati]**, seleziona **[!UICONTROL utilizza una risorsa CRX]** e fai clic sui puntini di sospensione prima della risorsa.

   ![Utilizzare una risorsa CRX](assets/use_crx_asset.png)

   Utilizzare una risorsa CRX

1. Seleziona il modulo adattivo creato tramite l&#39;interfaccia utente Gestisci Assets e fai clic su **[!UICONTROL OK]**.

   ![Seleziona un modulo adattivo](assets/selecting_form.png)

   Seleziona un modulo adattivo

   >[!NOTE]
   >
   >Per informazioni dettagliate sulla creazione di un modulo adattivo, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Per informazioni dettagliate sulla creazione di un processo, vedere [Creazione e gestione dei processi](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
