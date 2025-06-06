---
title: Post-elaborazione di lettere e comunicazioni interattive
description: La post-elaborazione delle lettere in Gestione della corrispondenza consente di creare processi di post AEM e Forms, come la stampa e l’e-mail, e di integrarli con le lettere.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: b48ceb2a-9e5b-4df7-9a3e-2ed7e3849041
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Post-elaborazione di lettere e comunicazioni interattive{#post-processing-of-letters-and-interactive-communications}

## Post-elaborazione {#post-processing}

Gli agenti possono associare ed eseguire flussi di lavoro di post-elaborazione su lettere e comunicazioni interattive. Il processo post da eseguire può essere selezionato nella vista Proprietà del modello Lettera. È possibile impostare i processi di post per la posta elettronica, la stampa, il fax o l&#39;archiviazione delle lettere finali.

![Post elaborazione](assets/ppoverview.png)

Per associare i processi di post a lettere o comunicazioni interattive, è innanzitutto necessario impostare i processi di post. È possibile eseguire due tipi di flussi di lavoro sulle lettere inviate:

1. **Forms Workflow:** si tratta dei flussi di lavoro di gestione dei processi di AEM Forms su JEE. Istruzioni per configurare [Forms Workflow](#formsworkflow).

1. **Flusso di lavoro di AEM:** I flussi di lavoro di AEM possono essere utilizzati anche come processi di post per le lettere inviate. Istruzioni per la configurazione di [AEM Workflow](../../forms/using/aem-forms-workflow.md).

## Flusso di lavoro per moduli {#formsworkflow}

1. In AEM, aprire Configurazione console Web Adobe Experience Manager per il server utilizzando il seguente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Gestione configurazione](assets/2configmanager-1.png)

1. In questa pagina, individua AEM Forms Client SDK Configuration ed espandila facendo clic su di essa.
1. In URL server, immetti il nome del tuo AEM Forms sul server JEE, i dettagli di accesso, quindi fai clic su **Salva**.

   ![Immettere il nome del server LiveCycle](assets/1cofigmanager.png)

1. Specifica nome utente e password.
1. Verificare che sun.util.calendar sia aggiunto alla configurazione del firewall di deserializzazione.

   Vai a Configurazione firewall deserializzazione e in Classi Inserite nell&#39;elenco Consentiti di prefissi di pacchetto, aggiungi sun.util.calendar.

1. Ora i server sono mappati e i processi di post in AEM Forms su JEE sono disponibili nell’interfaccia utente di AEM durante la creazione di lettere.

   ![Crea schermata lettere con post-processi elencati](assets/0configmanager.png)

1. Per autenticare un processo/servizio, copiare il nome di un processo, tornare alla pagina Configurazioni console web Adobe Experience Manager > Configurazione SDK client AEM Forms e aggiungere il processo come nuovo servizio.

   Se ad esempio nell&#39;elenco a discesa della pagina Proprietà della lettera il nome del processo viene visualizzato come Forms Workflow -> ValidCCPostProcess/SaveXML, aggiungere un nome di servizio come `ValidCCPostProcess/SaveXML`.

1. Per utilizzare AEM Forms sui flussi di lavoro JEE per la post-elaborazione, imposta i parametri e gli output necessari. I valori predefiniti dei parametri sono indicati di seguito.

   Vai alla pagina Configurazioni console Web Adobe Experience Manager > **[!UICONTROL Configurazioni gestione corrispondenza]** e configura i seguenti parametri:

   1. **inPDFDoc (parametro documento PDF):** un documento PDF come input. Questo input contiene la lettera sottoposta a rendering come input. I nomi dei parametri indicati sono configurabili. Possono essere configurate dalle configurazioni di Gestione della corrispondenza dalla configurazione.
   1. **inXMLDoc (parametro dati XML):** un documento XML come input. Questo input contiene i dati immessi dall&#39;utente sotto forma di XML.
   1. **inXDPDoc (parametro documento XDP):** un documento XML come input. Questo input contiene il layout sottostante (XDP).
   1. **inAttachmentDocs (parametro Attachment Documents):** Parametro di input elenco. Questo input contiene tutti gli allegati come input.
   1. **redirectURL (output URL di reindirizzamento):** tipo di output che indica l&#39;URL a cui reindirizzare.

   Il flusso di lavoro dei moduli deve avere come input il parametro del documento PDF o il parametro dei dati XML con lo stesso nome specificato in **[!UICONTROL Configurazioni gestione corrispondenza]**. Questo è necessario affinché il processo sia elencato nel menu a discesa Post Process (Pubblica elaborazione).

## Impostazioni sull’istanza Publish {#settings-on-the-publish-instance}

1. accedere a `https://localhost:publishport/aem/forms`.
1. Passa a **[!UICONTROL Lettere]** per visualizzare la lettera pubblicata disponibile nell&#39;istanza di pubblicazione.
1. Configurare le impostazioni di AEM DS. Vedere [Configurazione delle impostazioni di AEM DS](../../forms/using/configuring-the-processing-server-url.md).

>[!NOTE]
>
>Quando si utilizzano flussi di lavoro Forms o AEM, prima di effettuare qualsiasi invio dal server di pubblicazione è necessario configurare il servizio delle impostazioni DS. In caso contrario, la presentazione del modulo non avrà esito positivo.

## Recupero istanze lettera {#letter-instances-retrieval}

Le istanze di lettere salvate possono essere ulteriormente manipolate, ad esempio il recupero delle istanze di lettere e l&#39;eliminazione delle istanze di lettere, utilizzando le seguenti API definite in LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API lato server</strong></td>
   <td><strong>Nome operazione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Genera l'eccezione ICCE; </p> </td>
   <td>getLetterInstance</td>
   <td>Recupera l’istanza della lettera specificata </td>
  </tr>
  <tr>
   <td>Il valore public void deleteLetterInstance(String letterInstanceId) genera ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>È stata eliminata l'istanza lettera specificata </td>
  </tr>
  <tr>
   <td>L’elenco getAllLetterInstances(Query) genera l’eccezione ICCE; </td>
   <td>getAllLetterInstances </td>
   <td>Questa API recupera le istanze di lettere in base al parametro di query di input. Per recuperare tutte le istanze di lettere, il parametro di query può essere passato come null.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) genera ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Verifica se esiste una LetterInstance con il nome specificato </td>
  </tr>
 </tbody>
</table>

## Associazione di un processo di post a una lettera {#associating-a-post-process-with-a-letter}

Nell&#39;interfaccia utente di CCR, completare i passaggi seguenti per associare un processo post a una lettera:

1. Passa il puntatore del mouse su una lettera e seleziona **Visualizza proprietà**.
1. Seleziona **Modifica**.
1. Nel menu a discesa Proprietà di base, selezionare il processo di post da associare alla lettera. Sia i processi di post relativi ad AEM che quelli relativi a Forms sono elencati nel menu a discesa.
1. Seleziona **Salva**.
1. Dopo aver configurato la lettera con l’elaborazione post, pubblicala e, facoltativamente, nell’istanza di pubblicazione, specifica l’URL di elaborazione nel servizio Impostazioni di AEM DS. In questo modo il processo di post viene eseguito sull’istanza di elaborazione.

## Ricarica un&#39;istanza bozza di lettera  {#reloaddraft}

Un’istanza di bozza della lettera può essere ricaricata nell’interfaccia utente utilizzando il seguente URL:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID: l&#39;ID univoco dell&#39;istanza della lettera inviata.

Per ulteriori informazioni sul salvataggio di una bozza di lettera, vedere [Salvataggio delle bozze e invio delle istanze di lettere](../../forms/using/create-correspondence.md#savingdrafts).
