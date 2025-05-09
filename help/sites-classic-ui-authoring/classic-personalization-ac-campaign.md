---
title: Utilizzo di Adobe Campaign 6.1 e Adobe Campaign Standard
description: Puoi creare contenuti e-mail in AEM ed elaborarli in e-mail Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
exl-id: df3c15e0-549b-449f-9f50-bb40e1740159
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 2%

---

# Utilizzo di Adobe Campaign 6.1 e Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

Puoi creare contenuti e-mail in AEM ed elaborarli in e-mail Adobe Campaign. Per farlo, devi:

1. Crea una newsletter in AEM da un modello specifico di Adobe Campaign.
1. Seleziona [un servizio Adobe Campaign](#selectingtheadobecampaigncloudservice) prima di modificare il contenuto per accedere a tutte le funzionalità.
1. Modifica il contenuto.
1. Convalida il contenuto.

Il contenuto può quindi essere sincronizzato con una consegna in Adobe Campaign. Istruzioni dettagliate sono descritte in questo documento.

>[!NOTE]
>
>Prima di poter utilizzare questa funzionalità, devi configurare AEM per l&#39;integrazione con [Adobe Campaign](/help/sites-administering/campaignonpremise.md) o [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Invio di contenuti e-mail tramite Adobe Campaign {#sending-email-content-via-adobe-campaign}

Dopo aver configurato AEM e Adobe Campaign, puoi creare i contenuti di consegna e-mail direttamente in AEM, quindi elaborarli in Adobe Campaign.

Quando crei contenuti Adobe Campaign in AEM, devi collegare un servizio Adobe Campaign prima di modificarli per accedere a tutte le funzionalità.

Esistono due casi possibili:

* Il contenuto può essere sincronizzato con una consegna da Adobe Campaign. Questo consente di utilizzare il contenuto di AEM in una consegna.
* (Solo Adobe Campaign on-premise) Il contenuto può essere inviato direttamente ad Adobe Campaign, che genera automaticamente una nuova consegna e-mail. Questa modalità presenta limitazioni.

Istruzioni dettagliate sono descritte in questo documento.

### Creazione di nuovi contenuti e-mail {#creating-new-email-content}

>[!NOTE]
>
>Quando aggiungi modelli e-mail, assicurati di aggiungerli in **/content/campaigns** per renderli disponibili.
>

1. In AEM, seleziona la cartella **Siti Web**, quindi sfoglia l&#39;esploratore per scoprire dove vengono gestite le campagne e-mail. Nell&#39;esempio seguente, il nodo interessato è **Siti Web** > **Campagne** > **Geometrixx Outdoors** > **Campagne e-mail**.

   >[!NOTE]
   >
   >[Gli esempi di e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md#weretail). Scarica contenuti Geometrixx di esempio da Package Share.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Seleziona **Nuovo** > **Nuova pagina** per creare nuovi contenuti e-mail.
1. Seleziona uno dei modelli disponibili specifici di Adobe Campaign, quindi specifica le proprietà generali della pagina. Per impostazione predefinita sono disponibili tre modelli:

   * **E-mail Adobe Campaign (AC 6.1)**: ti consente di aggiungere contenuto a un modello predefinito prima di inviarlo ad Adobe Campaign 6.1 per la consegna.
   * **E-mail Adobe Campaign (ACS)**: ti consente di aggiungere contenuto a un modello predefinito prima di inviarlo ad Adobe Campaign Standard per la consegna.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Fai clic su **Crea** per creare l&#39;e-mail o la newsletter.

### Selezione del servizio cloud Adobe Campaign e del modello {#selecting-the-adobe-campaign-cloud-service-and-template}

Per l’integrazione con Adobe Campaign, devi aggiungere alla pagina un servizio cloud Adobe Campaign. In questo modo puoi accedere alla personalizzazione e ad altre informazioni su Adobe Campaign.

Inoltre, potrebbe essere necessario selezionare il modello Adobe Campaign, modificare l’oggetto e aggiungere contenuto di testo normale per gli utenti che non visualizzeranno l’e-mail in HTML.

1. Seleziona la scheda **Pagina** nella barra laterale, quindi seleziona **Proprietà pagina.**
1. Nella scheda **Servizi cloud** della finestra popup, seleziona **Aggiungi servizio** per aggiungere il servizio Adobe Campaign e fai clic su **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Seleziona la configurazione che corrisponde alla tua istanza di Adobe Campaign dall&#39;elenco a discesa, quindi fai clic su **OK**.

   >[!NOTE]
   >
   >Assicurarsi di fare clic su **OK** o **Applica** dopo l&#39;aggiunta del servizio cloud. In questo modo la scheda **Adobe Campaign** funziona correttamente.

1. Se desideri applicare un modello di consegna e-mail specifico (da Adobe Campaign), diverso dal modello predefinito di **mail**, seleziona nuovamente **Proprietà pagina**. Nella scheda **Adobe Campaign**, immetti il nome interno del modello di consegna e-mail nell&#39;istanza di Adobe Campaign correlata.

   In Adobe Campaign Standard, il modello è **Consegna con contenuto AEM**. In Adobe Campaign 6.1, il modello è **Email delivery con contenuto AEM**.

   Quando selezioni il modello, AEM abilita automaticamente i componenti **Adobe Campaign Newsletter**.

### Modifica del contenuto delle e-mail {#editing-email-content}

Puoi modificare il contenuto delle e-mail nell’interfaccia utente classica o nell’interfaccia touch.

1. Immetti l&#39;oggetto e la versione del testo dell&#39;e-mail selezionando **Proprietà pagina** > **E-mail** dalla casella degli strumenti.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Modifica il contenuto dell’e-mail aggiungendo gli elementi desiderati tra quelli disponibili nella barra laterale. Per eseguire questa operazione, trascinali. Quindi fai doppio clic sull’elemento da modificare.

   Ad esempio, puoi aggiungere testo contenente campi di personalizzazione.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Consulta [Componenti Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) per una descrizione dei componenti disponibili per le newsletter/campagne e-mail di Adobe Campaign.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Inserimento della personalizzazione {#inserting-personalization}

Durante la modifica del contenuto, puoi inserire:

* Campi contestuali di Adobe Campaign. Si tratta di campi che puoi inserire all’interno del testo e che verranno adattati in base ai dati del destinatario (ad esempio, nome, cognome o qualsiasi dato della dimensione di destinazione).
* Blocchi di personalizzazione di Adobe Campaign. Si tratta di blocchi di contenuto predefinito non correlati ai dati del destinatario, ad esempio il logo di un brand o il collegamento a una pagina speculare.

Consulta [Componenti Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) per una descrizione completa dei componenti di Campaign.

>[!NOTE]
>
>* Vengono presi in considerazione solo i campi della dimensione di targeting **Profili** di Adobe Campaign.
>* Quando si visualizzano le proprietà da **Sites**, non si dispone dell&#39;accesso ai campi contestuali di Adobe Campaign. Puoi accedervi direttamente dall’e-mail durante la modifica.
>

1. Inserisci un nuovo componente **Newsletter** > **Testo e Personalization (Campaign)**.
1. Apri il componente facendo doppio clic su di esso. La finestra **Modifica** dispone di una funzionalità che consente di inserire gli elementi di personalizzazione.

   >[!NOTE]
   >
   >I campi di contesto disponibili corrispondono alla dimensione di targeting **Profili** in Adobe Campaign.
   >
   >Vedi [Collegamento di una pagina di AEM a un&#39;e-mail di Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Seleziona **ClientContext** nella barra laterale per testare i campi di personalizzazione utilizzando i dati nei profili utente tipo.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Viene visualizzata una finestra che consente di selezionare l’utente tipo desiderato. I campi di personalizzazione vengono sostituiti automaticamente dai dati del profilo selezionato.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Anteprima di una newsletter {#previewing-a-newsletter}

Puoi visualizzare in anteprima come si presenterà la newsletter e la personalizzazione.

1. Aprire la newsletter che si desidera visualizzare in anteprima e fare clic su Anteprima (lente di ingrandimento) per ridurre la barra laterale.
1. Fai clic su una delle icone del client e-mail per visualizzare l’aspetto della newsletter in ogni client e-mail.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Espandi la barra laterale per iniziare di nuovo la modifica.

### Approvazione di contenuti in AEM {#approving-content-in-aem}

Al termine del contenuto, puoi avviare il processo di approvazione. Vai alla scheda **Flusso di lavoro** della casella degli strumenti e seleziona il flusso di lavoro **Approva per Adobe Campaign**.

Questo flusso di lavoro preconfigurato prevede due passaggi: revisione e quindi approvazione oppure revisione e infine rifiuto. Tuttavia, questo flusso di lavoro può essere esteso e adattato a un processo più complesso.

![chlimage_1-182](assets/chlimage_1-182.png)

Per approvare il contenuto per Adobe Campaign, applica il flusso di lavoro selezionando **Flusso di lavoro** nella barra laterale e selezionando **Approva per Adobe Campaign**, quindi fai clic su **Avvia flusso di lavoro**. Segui i passaggi e approva il contenuto. Puoi anche rifiutare il contenuto selezionando **Rifiuta** invece di **Approva** nell&#39;ultimo passaggio del flusso di lavoro.

![chlimage_1-183](assets/chlimage_1-183.png)

Dopo l’approvazione, il contenuto viene visualizzato come approvato in Adobe Campaign. L’e-mail può quindi essere inviata.

In Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

In Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>Il contenuto non approvato può essere sincronizzato con una consegna in Adobe Campaign, ma la consegna non può essere eseguita. Solo i contenuti approvati possono essere inviati tramite le consegne di Campaign.

## Collegamento di AEM con Adobe Campaign Standard e Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Per informazioni dettagliate, consulta [Collegamento di AEM con Adobe Campaign Standard e Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) in [Utilizzo di Adobe Campaign 6.1 e Adobe Campaign Standard](/help/sites-authoring/campaign.md) nella documentazione standard sull&#39;authoring.
