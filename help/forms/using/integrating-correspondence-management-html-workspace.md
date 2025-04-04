---
title: Integrazione di applicazioni di terze parti nell’area di lavoro di AEM Forms
description: Integra applicazioni di terze parti, come Gestione della corrispondenza, nell’area di lavoro di AEM Forms.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
exl-id: b383fa80-1643-41f3-bc6c-176727fea688
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Integrazione di applicazioni di terze parti nell’area di lavoro di AEM Forms{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms Workspace supporta la gestione delle attività di assegnazione delle attività e completamento per moduli e documenti. Questi moduli e documenti possono essere XDP Forms, Flex® Forms o Guide (obsolete) di cui è stato eseguito il rendering in formati XDP, PDF, HTML o Flex.

Queste funzionalità vengono ulteriormente migliorate. AEM Forms ora supporta la collaborazione con applicazioni di terze parti che supportano funzionalità simili all’area di lavoro di AEM Forms. Una parte comune di questa funzionalità è il flusso di lavoro di un&#39;assegnazione e la successiva approvazione di un&#39;attività. AEM Forms offre un’unica esperienza unificata per gli utenti aziendali di AEM Forms, in modo che tutte le assegnazioni di attività o approvazioni per le applicazioni supportate possano essere gestite tramite l’area di lavoro di AEM Forms.

Ad esempio, consideriamo Gestione della corrispondenza come il candidato di esempio per l’integrazione con l’area di lavoro di AEM Forms. Gestione della corrispondenza ha il concetto di &quot;Lettera&quot;, che può essere rappresentata e consente azioni.

## Creare risorse di gestione della corrispondenza {#create-correspondence-management-assets}

Per prima cosa, crea un modello di esempio per la gestione della corrispondenza di cui viene eseguito il rendering nell’area di lavoro di AEM Forms. Per ulteriori dettagli, vedere [Creare un modello di lettera](../../forms/using/create-letter.md).

Accedi al modello Gestione corrispondenza con il relativo URL per verificare se è possibile eseguire correttamente il rendering del modello Gestione corrispondenza. L&#39;URL ha un pattern simile a `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

Dove `encodedLetterId` è l&#39;ID della lettera con codifica URL. Specifica lo stesso ID lettera quando definisci il processo di rendering per l’attività dell’area di lavoro in Workbench.

## Creare un’attività per riprodurre e inviare una lettera in AEM Workspace {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

Prima di eseguire questi passaggi, assicurati di essere membro dei seguenti gruppi:

* cm-agent-users
* Utenti Workspace

Per ulteriori informazioni, vedere [Aggiungere e configurare gli utenti](/help/forms/using/admin-help/adding-configuring-users.md).

Utilizza i seguenti passaggi per creare un’attività per eseguire il rendering e inviare una lettera in AEM Workspace:

1. Avvia Workbench. Accedere a localhost come amministratore.
1. Selezionate File > Nuovo (New) > Applicazione (Application). Nel campo Nome applicazione immettere `CMDemoSample` e quindi fare clic su Fine.
1. Selezionare `CMDemoSample/1.0` e fare clic con il pulsante destro del mouse su `NewProcess`. Nel campo del nome, immettere `CMRenderer` e quindi fare clic su Fine.
1. Trascina il selettore attività Punto iniziale e configuralo:

   1. In Dati presentazione, seleziona Usa risorsa CRX.

      ![useacrxasset](assets/useacrxasset.png)

   1. Cercare una risorsa. Nella finestra di dialogo Seleziona risorsa modulo, la scheda Lettere elenca tutte le lettere presenti sul server.

      ![Scheda Lettera](assets/letter_tab_new.png)

   1. Selezionare la lettera appropriata e fare clic su **OK**.

1. Fai clic su Gestisci profili azione. Viene visualizzata la finestra di dialogo Gestisci profilo azione. Verificare che il processo di rendering e il processo di invio siano selezionati in modo appropriato.
1. Per aprire la lettera con un file XML dati, sfogliare e selezionare il file di dati appropriato nel processo di preparazione dei dati.
1. Fare clic su OK.
1. Definire le variabili per Output punto iniziale e Allegati attività. Le variabili definite contengono i dati Output punto iniziale e Allegati attività.
1. (Facoltativo) Per aggiungere un altro utente al flusso di lavoro, trascina un selettore di attività, configuralo e assegnalo a un utente. Scrivere un wrapper personalizzato (esempio fornito di seguito) o scaricare e installare il DSC (fornito di seguito) per il modello di lettera esatta, l&#39;output del punto iniziale e l&#39;allegato dell&#39;operazione.

   Di seguito è riportato un esempio di wrapper personalizzato:

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [Ottieni file](assets/dscsample.zip)
Scarica DSC: un esempio di DSC è disponibile nel file DSCSample.zip allegato in precedenza. Scarica e decomprimi il file DSCSample.zip. Prima di utilizzare il servizio DSC, è necessario configurarlo. Vedere [Configurare il servizio DSC](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p).

   Nella finestra di dialogo Definisci attività, seleziona l&#39;attività appropriata come getLetterInstanceInfo e fai clic su **OK**.

1. Distribuire l&#39;applicazione. Se viene richiesto di effettuare il check-in e salvare le risorse.
1. Accedi all&#39;area di lavoro di AEM Forms all&#39;indirizzo https://&#39;[server]:[porta]&#39;/lc/content/ws.
1. Apri l&#39;attività aggiunta, CMRenderer. Viene visualizzata la lettera Gestione corrispondenza.

   ![cminworkspace](assets/cminworkspace.png)

1. Inserisci i dati richiesti e invia la lettera. La finestra si chiude. In questo processo, l’attività viene assegnata all’utente specificato nel flusso di lavoro al passaggio 9.

   >[!NOTE]
   >
   >Il pulsante Invia non viene attivato finché non vengono compilate tutte le variabili richieste nella lettera.
