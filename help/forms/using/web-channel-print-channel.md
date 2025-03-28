---
title: Canale di stampa e canale web
description: Importazione di modelli di canale di stampa e creazione e abilitazione di modelli di canale web
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: dca7f612-f505-414b-9326-90624be9db39
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Canale di stampa e canale web{#print-channel-and-web-channel}

Le comunicazioni interattive possono essere distribuite attraverso due canali: stampa e web. Il canale di stampa viene utilizzato per creare PDF e comunicazioni cartacee, ad esempio una lettera stampata come promemoria per il pagamento del premio assicurativo, mentre il canale web viene utilizzato per fornire esperienze online, ad esempio l’estratto conto di una carta di credito su un sito web.

Gli autori delle comunicazioni interattive possono riutilizzare risorse quali frammenti di documenti e immagini per creare versioni stampate e web delle comunicazioni interattive.

Uno dei prerequisiti per la [creazione di una comunicazione interattiva](../../forms/using/create-interactive-communication.md) è disporre dei modelli per la stampa e/o il canale Web sul server. Mentre gli autori dei modelli creano il modello di canale web all’interno di AEM, il modello di canale di stampa XDP viene creato in Adobe Forms Designer e caricato sul server.

## Stampa canale {#printchannel}

Il canale di stampa di una comunicazione interattiva utilizza il modello di modulo XFA, XDP. Un XDP è progettato in Adobe Forms Designer. Per ulteriori informazioni sulla creazione di modelli di canale di stampa, vedere [Progettazione layout](../../forms/using/layout-design-details.md). Per utilizzare un modello di canale di stampa nella comunicazione interattiva, devi caricarlo nel server di AEM Forms.

### Carica modello di canale di stampa comunicazione interattiva {#upload-interactive-communication-print-channel-template}

Per caricare il modello, devi essere membro del gruppo utenti di forms. Per caricare il modello del canale di stampa (XDP) in AEM Forms, effettua le seguenti operazioni:

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**.

   Individua e seleziona il modello di canale di stampa (XDP) appropriato e seleziona **[!UICONTROL Apri]**.

## Canale web {#web-channel}

Gli autori e gli amministratori di modelli possono creare, modificare e abilitare i modelli web. Per consentire ad altri utenti di creare modelli Web, devi assegnare loro i diritti necessari. Per ulteriori informazioni, vedere [Amministrazione diritti utente, gruppo e accesso](/help/sites-administering/user-group-ac-admin.md).

### Authoring di un modello di canale web {#authoring-web-channel-template}

Per creare un modello di canale web, devi prima creare una cartella di modelli. Dopo aver creato un modello Web all&#39;interno di una cartella di modelli, è necessario abilitare il modello per consentire agli utenti dei moduli di creare un canale Web di una comunicazione interattiva basata sul modello.

La procedura seguente illustra come creare un modello di canale web:

1. Crea una cartella di modelli per mantenere i modelli web di comunicazione interattiva, se non ne hai già uno. Per ulteriori informazioni, vedere Cartelle modelli in [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md).

   1. Selezionare **[!UICONTROL Strumenti]** ![Strumenti](assets/tools.png) > **[!UICONTROL Browser configurazioni]**.
      * Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
   1. Nella pagina Browser configurazioni, selezionare **[!UICONTROL Crea]**.
   1. Nella finestra di dialogo Crea configurazione, specifica un titolo per la cartella, seleziona **[!UICONTROL Modelli modificabili]** e seleziona **[!UICONTROL Crea]**.

      La cartella viene creata ed elencata nella pagina Browser configurazioni.

1. Passa alla cartella dei modelli appropriata e crea un modello web.

   1. Passare alla cartella dei modelli appropriata selezionando **[!UICONTROL Strumenti]** > **[!UICONTROL Modelli]** > **`[Folder]`**.
   1. Seleziona **[!UICONTROL Crea]**.
   1. Seleziona **[!UICONTROL Comunicazione interattiva - Canale Web]** e seleziona **[!UICONTROL Successivo]**.
   1. Immettere un titolo e una descrizione per il modello, quindi selezionare **[!UICONTROL Crea]**.

      Il modello viene creato e viene visualizzata una finestra di dialogo.

   1. Seleziona **[!UICONTROL Apri]** per aprire il modello creato nell&#39;editor modelli.

      Viene visualizzato l&#39;Editor modelli.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Durante la creazione o la modifica di un modello, un autore di modelli può definire diversi aspetti. La creazione o la modifica di un modello è simile all’authoring delle pagine. Per ulteriori informazioni, vedere Modifica di modelli - Autori di modelli in [Creazione di modelli di pagina](/help/sites-authoring/templates.md).

1. Per consentire l’utilizzo di questo modello per la creazione di comunicazioni interattive, abilita il modello.

   1. Seleziona **[!UICONTROL Strumenti]** ![strumenti](assets/tools.png) > **[!UICONTROL Modelli]**.
   1. Passa al modello appropriato, selezionalo e seleziona **[!UICONTROL Abilita]**. Nel messaggio di avviso, seleziona **[!UICONTROL Abilita]**.

      Il modello è abilitato e il suo stato viene visualizzato come Abilitato. Ora puoi procedere alla creazione di una comunicazione interattiva in cui puoi utilizzare il modello di canale web appena creato.

### Stampa canale come master per canale web {#print-channel-as-master-for-web-channel}

Durante l’authoring di una comunicazione interattiva, gli autori possono selezionare questa opzione per creare il canale web in sincronia con il canale di stampa. L’utilizzo del canale di stampa come master per il canale web assicura che il contenuto, l’ereditarietà e l’associazione dati del canale web siano derivati dal canale di stampa e che le modifiche apportate nel canale di stampa possano essere riflesse nel canale web. Gli autori delle comunicazioni interattive, tuttavia, possono interrompere l’ereditarietà di componenti specifici nel canale web, in base alle esigenze.

![Stampa canale come master](assets/create_ic_print_master_new.png) ![Canale Web con stampa canale come master](assets/create_ic_print_master_web_new.png)
