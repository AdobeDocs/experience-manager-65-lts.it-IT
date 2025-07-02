---
title: Configurare l’assegnazione tag delle risorse tramite Smart Content Service
description: Scopri come configurare l'assegnazione tag avanzati e l'assegnazione tag avanzati migliorati in [!DNL Adobe Experience Manager], utilizzando il Servizio di contenuti avanzati.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
exl-id: be7c294c-149b-4825-8376-573f9e2987e2
source-git-commit: 1cedead501597fb655c2c7b87336b29cbf048294
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 20%

---

# Prepara [!DNL Assets] per assegnazione tag avanzati {#configure-asset-tagging-using-the-smart-content-service}

Prima di iniziare a assegnare tag alle risorse utilizzando Smart Content Services, è necessario integrare [!DNL Experience Manager Assets] con Adobe Developer Console per utilizzare Smart Service di [!DNL Adobe Sensei]. Una volta configurato, il servizio viene addestrato utilizzando alcune immagini e un tag.
Prima di utilizzare il Servizio di contenuti avanzati, verifica quanto segue:

* [Integrare con Adobe Developer Console](#integrate-adobe-io).
* [Formazione del Servizio di contenuti avanzati](#training-the-smart-content-service).
* Installa il [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it) più recente.

>[!IMPORTANT]
>
>Consulta [preparare Assets per l&#39;assegnazione tag avanzati](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/administer/config-smart-tagging) per la configurazione di tag avanzati in AEM 6.5.

**Nuovi utenti**

Smart Content Services non è più disponibile per i nuovi utenti locali di [!DNL Experience Manager Assets].

**Utenti esistenti**

Gli utenti on-premise esistenti che dispongono già di questa funzionalità possono continuare a utilizzare Smart Content Services.

## Integrare con Adobe Developer Console {#integrate-adobe-io}

Quando si esegue l&#39;integrazione con Adobe Developer Console, il server [!DNL Experience Manager] autentica le credenziali del servizio con il gateway di Adobe Developer Console prima di inoltrare la richiesta al Servizio di contenuti avanzati. Per l’integrazione, è necessario un account Adobe ID con privilegi di amministratore per l’organizzazione e una licenza del Servizio di contenuti avanzati acquistata e abilitata per la tua organizzazione.

Per configurare il Servizio di contenuti avanzati, segui questi passaggi di livello principale:

1. Crea un&#39;integrazione in [Adobe Developer Console](#create-adobe-io-integration).

1. Crea la configurazione dell&#39;account tecnico [IMS](#create-ims-account-config) utilizzando la chiave API e altre credenziali di Adobe Developer Console.

1. [Configura il Servizio di contenuti avanzati](#configure-smart-content-service).

1. [Verifica la configurazione](#validate-the-configuration).

### Creare l’integrazione con Adobe Developer Console {#create-adobe-io-integration}

Per utilizzare le API del Servizio di contenuti avanzati, creare un&#39;integrazione in Adobe Developer Console per ottenere [!UICONTROL la chiave API] (generata nel campo [!UICONTROL ID CLIENT] dell&#39;integrazione di Adobe Developer Console), [!UICONTROL ID ORGANIZZAZIONE] e [!UICONTROL SEGRETO CLIENT] per [!UICONTROL le impostazioni del Servizio di tag avanzati di Assets] della configurazione cloud in [!DNL Experience Manager].

1. Accedi a [https://developer.adobe.com](https://developer.adobe.com/) in un browser. Selezionare l&#39;account appropriato e verificare che il ruolo organizzazione associato sia **amministratore** di sistema.

1. Crea un progetto con il nome desiderato. Fai clic su **[!UICONTROL Aggiungi API]**.

1. Nella pagina **[!UICONTROL Aggiungi un’API]**, seleziona **[!UICONTROL Experience Cloud]** e **[!UICONTROL Contenuti avanzati]**. Fai clic su **[!UICONTROL Avanti]**.

1. Selezionare **[!UICONTROL OAuth Server-to-Server]**. Fai clic su **[!UICONTROL Avanti]**.
Per informazioni dettagliate su come eseguire questa configurazione, consulta la documentazione di Developer Console, a seconda dei requisiti:

   * Panoramica:
      * [Autenticazione da server a server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

   * Creazione di nuove credenziali OAuth:
      * [Guida all’implementazione delle credenziali da server a server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)

   * Migrazione di una credenziale JWT esistente a una credenziale OAuth:
      * [Migrazione dalle credenziali dell’account di servizio (JWT) alle credenziali da server a server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)


1. Nella pagina **[!UICONTROL Seleziona profili di prodotto]**, seleziona **[!UICONTROL Servizi di contenuti avanzati]**. Fai clic su **[!UICONTROL Salva API configurata]**.

   In una pagina vengono visualizzate ulteriori informazioni sulla configurazione. Tieni aperta questa pagina per copiare e aggiungere questi valori nelle [!UICONTROL Impostazioni del servizio di assegnazione tag avanzati di Assets] della configurazione cloud in [!DNL Experience Manager] per configurare gli smart tag.

   ![Credenziali OAuth in Developer Console](assets/ims-configuration-developer-console.png)

### Creare la configurazione dell’account tecnico IMS {#create-ims-account-config}

Devi creare la configurazione dell’account tecnico IMS seguendo questi passaggi:

1. Nell’interfaccia utente di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

1. Fai clic su **[!UICONTROL Crea]**.

1. Nella finestra di dialogo Configurazione account tecnico IMS, utilizza i seguenti valori:

   ![Finestra di configurazione Adobe IMS](assets/adobe-ims-config.png)

   | Campo | Descrizione |
   | -------- | ---------------------------- |
   | Soluzione cloud | Scegli **[!UICONTROL Tag avanzati]** dal menu a discesa. |
   | Titolo | Aggiungi il titolo della configurazione dell’account IMS. |
   | Server autorizzazioni | Aggiungi `https://ims-na1.adobelogin.com` |
   | ID client | Da fornire tramite [console Adobe Developer](https://developer.adobe.com/console/). |
   | Segreto client | Da fornire tramite [console Adobe Developer](https://developer.adobe.com/console/). |
   | Ambito | Da fornire tramite [console Adobe Developer](https://developer.adobe.com/console/). |
   | ID organizzazione | Da fornire tramite [console Adobe Developer](https://developer.adobe.com/console/). |

1. Selezionare la configurazione creata e fare clic su **[!UICONTROL Verifica stato]**.

1. Confermare la finestra di dialogo Verifica stato e fare clic su Chiudi una volta che la configurazione è nello stato integro.

### Crea una nuova configurazione {#configure-smart-content-service}

Per configurare l&#39;integrazione, utilizzare i valori dei campi [!UICONTROL ID ACCOUNT TECNICO], [!UICONTROL ID ORGANIZZAZIONE], [!UICONTROL SEGRETO CLIENT] e [!UICONTROL ID CLIENT] dell&#39;integrazione Adobe Developer Console. La creazione di una configurazione cloud di tag avanzati consente l&#39;autenticazione delle richieste API dalla distribuzione [!DNL Experience Manager].

1. In [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Smart Tag]** per aprire le [!UICONTROL Configurazioni smart tag].

1. Fai clic su **[!UICONTROL Crea]** per creare una nuova configurazione. In caso contrario, fare clic su **[!UICONTROL Proprietà]** per aggiornare la configurazione esistente.

1. Compila i campi seguenti:

   ![Configurazione tag avanzati](assets/smart-tags-config.png)

   | Campo | Descrizione |
   | -------- | ---------------------------- |
   | Titolo | Aggiungi il titolo della configurazione dell’account IMS. |
   | Configurazione Adobe IMS associata | Scegli la configurazione dal menu a discesa. |
   | URL del servizio | `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`. Ad esempio, `https://smartcontent.adobe.io/apac`. È possibile specificare `na`, `emea` o `apac` come aree in cui è ospitata l&#39;istanza di authoring di Experience Manager. |

   >[!NOTE]
   >
   >Se il provisioning del servizio gestito di Experience Manager è stato eseguito prima del 1° settembre 2022, utilizza il seguente URL del servizio:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

1. Fai clic su **[!UICONTROL Salva e chiudi]**.

### Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi utilizzare un MBean JMX per convalidarla. Per eseguire la convalida, effettua le seguenti operazioni.

1. Accedi al server di [!DNL Experience Manager] all’indirizzo `https://[aem_server]:[port]`.

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]** per aprire la console OSGi. Fai clic su **[!UICONTROL Principale] > [!UICONTROL JMX]**.

<!--
1. Click `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.-->

1. Fai clic su `com.day.cq.dam.similaritysearch.internal.impl (SCS)`.

   ![Finestra Mbean](assets/mbean.png)

1. Fai clic su `validateConfigs()`. Nella finestra di dialogo **[!UICONTROL Validate Configurations]** (Convalida configurazioni), fai clic su **[!UICONTROL Invoke]** (Richiama).

I risultati della convalida vengono visualizzati nella stessa finestra di dialogo.

### Abilitare l&#39;assegnazione tag avanzati nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] (facoltativo) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.

1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.

1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Assegna tag avanzati a risorse]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungere il passaggio Assegna tag avanzati a risorse dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

1. Apri le proprietà del passaggio per modificare i dettagli. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag](assets/smart-tag-step-properties-workflow1.png)

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se vuoi che il flusso di lavoro venga completato anche con esito negativo del passaggio di assegnazione tag automatica.

   Inoltre, per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l&#39;assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

   ![Configura il flusso di lavoro Risorsa di aggiornamento DAM per aggiungere il passaggio smart tag e selezionare l&#39;handler avanzato](assets/smart-tag-step-properties-workflow2.png)

1. Fai clic sull&#39;icona Fine ![fine](assets/do-not-localize/check-ok-done-icon.png) per chiudere il passaggio del processo.

1. Fai clic su **[!UICONTROL Sincronizza]** per salvare il flusso di lavoro.

## Formazione del Servizio di contenuti avanzati {#training-the-smart-content-service}

Affinché il Servizio di contenuti avanzati riconosca la tassonomia aziendale, eseguilo su una serie di risorse che includono già tag rilevanti per la tua azienda. Per assegnare tag efficaci alle immagini del tuo marchio, il Servizio di contenuti avanzati richiede che le immagini di formazione siano conformi a determinate linee guida. Dopo l’addestramento, il servizio può applicare la stessa tassonomia a un set di risorse simile.

Puoi addestrare il servizio più volte per migliorarne la capacità di applicare tag rilevanti. Dopo ogni ciclo di formazione, esegui un flusso di lavoro sui tag e verifica che alle risorse siano assegnati i tag appropriati.

Puoi addestrare il Servizio di contenuti avanzati periodicamente o in base ai requisiti.

>[!NOTE]
>
>Il flusso di lavoro di formazione viene eseguito solo sulle cartelle.

### Linee guida per la formazione {#guidelines-for-training}

Per ottenere risultati ottimali, le immagini del set di apprendimento sono conformi alle seguenti linee guida:

**Quantity and size (Quantità e dimensioni)**: almeno 30 immagini per tag. Almeno 500 pixel sul lato più lungo.

**Coerenza**: le immagini utilizzate per un tag specifico sono visivamente simili.

Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/coherence.png)

**Copertura**: utilizza una varietà sufficiente di immagini nel corso di formazione. L’idea è quella di fornire alcuni esempi, ma ragionevolmente diversi, in modo che Experience Manager impari a concentrarsi sulle cose giuste. Se applichi lo stesso tag a immagini visivamente diverse, includi almeno cinque esempi per ogni tipo.

Ad esempio, per il tag *model-down-pose*, includi più immagini di formazione simili all&#39;immagine evidenziata di seguito affinché il servizio identifichi più accuratamente immagini simili durante l&#39;assegnazione dei tag.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: il servizio si addestra meglio alle immagini che hanno meno distrazione (sfondi prominenti, accompagnamenti non correlati, come oggetti/persone con il soggetto principale).

Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per la formazione.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag come `raincoat` e `model-side-view`, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacità del Servizio di contenuti avanzati di addestrarsi sui tag e di applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione. Per ottenere i migliori risultati, Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.

### Formazione periodica {#periodic-training}

Puoi abilitare il Servizio di contenuti avanzati per la formazione periodica sulle risorse e sui tag associati all’interno di una cartella. Apri la pagina [!UICONTROL Proprietà] della cartella di risorse, seleziona **[!UICONTROL Abilita tag avanzati]** nella scheda **[!UICONTROL Dettagli]** e salva le modifiche.

![enable_smart_tags](assets/enable_smart_tags.png)

Una volta selezionata questa opzione per una cartella, [!DNL Experience Manager] esegue automaticamente un flusso di lavoro di formazione per addestrare il Servizio di contenuti avanzati sulle risorse della cartella e sui relativi tag. Per impostazione predefinita, il flusso di lavoro di formazione viene eseguito settimanalmente alle 00:30 del sabato.

### Formazione on-demand {#on-demand-training}

Puoi addestrare il Servizio di contenuti avanzati quando necessario dalla console Flusso di lavoro.

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di flusso di lavoro]**, seleziona il flusso di lavoro **[!UICONTROL Apprendimento dei tag avanzati]**, quindi fai clic su **[!UICONTROL Avvia flusso di lavoro]** nella barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]**, individua la cartella del payload che include le risorse con tag per l&#39;apprendimento del servizio.
1. Specifica un titolo per il flusso di lavoro e aggiungi un commento. Quindi fare clic su **[!UICONTROL Esegui]**. Le risorse e i tag vengono inviati per la formazione.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una volta elaborate le risorse di una cartella per l’apprendimento, solo le risorse modificate vengono elaborate nei cicli di apprendimento successivi.

### Visualizzare i rapporti di formazione {#viewing-training-reports}

Per verificare se il Servizio di contenuti avanzati è stato addestrato sui tag nel set di formazione di risorse, controlla il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Rapporti risorse]**, fai clic su **[!UICONTROL Crea]**.
1. Seleziona il report **[!UICONTROL Apprendimento dei tag avanzati]** e fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi fare clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il report, fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Esamina i dettagli del rapporto.

   Il rapporto mostra lo stato di formazione per i tag che hai appreso. La presenza del colore verde nella colonna **[!UICONTROL Training Status (Stato formazione)]** indica che per il tag è stato eseguito il training del servizio di contenuti avanzati. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag.

   Se non trovi i tuoi tag in questo rapporto, esegui nuovamente il flusso di lavoro di formazione per questi tag.

1. Per scaricare il report, selezionarlo dall&#39;elenco e fare clic su **[!UICONTROL Scarica]** nella barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo di Microsoft Excel.

## Limitazioni {#limitations}

* I tag avanzati migliorati si basano su modelli di apprendimento delle immagini e dei relativi tag. Questi modelli non sono sempre perfetti per identificare i tag. La versione corrente del Servizio di contenuti avanzati presenta le seguenti limitazioni:

   * Incapacità di riconoscere le sottili differenze nelle immagini. Ad esempio, magliette e magliette normali.
   * Impossibilità di identificare i tag in base a modelli/parti minuscole di un’immagine. Ad esempio, i logo sulle magliette.
   * L&#39;assegnazione tag è supportata nelle impostazioni internazionali in cui è supportato [!DNL Experience Manager].

* Per cercare le risorse con tag avanzati (regolari o migliorati), utilizza l&#39;Omnisearch [!DNL Assets] (ricerca full-text). Non esiste un predicato di ricerca separato per i tag avanzati.

>[!MORELIKETHIS]
>
>* [Panoramica e formazione dei tag avanzati](enhanced-smart-tags.md)
>* [Risoluzione dei problemi relativi agli smart tag per le credenziali OAuth](config-oauth.md)
>* [Esercitazione video sugli smart tag](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
