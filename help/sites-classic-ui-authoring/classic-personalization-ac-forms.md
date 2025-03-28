---
title: Creazione di Adobe Campaign Forms in AEM
description: AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database di Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
exl-id: 3a39c4ba-353a-41ee-bfe6-e7eb4323f170
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Creazione di Adobe Campaign Forms in AEM{#creating-adobe-campaign-forms-in-aem}

AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database di Adobe Campaign.

Puoi gestire le sottoscrizioni di nuovi contatti, il loro annullamento e i dati del profilo utente, il tutto integrando i relativi dati nel database di Adobe Campaign.

Per utilizzare Adobe Campaign Forms in AEM, è necessario seguire questi passaggi, descritti in questo documento:

1. Rendi disponibile un modello.
1. Crea un modulo.
1. Modifica il contenuto del modulo.

Per impostazione predefinita, sono disponibili tre tipi di moduli specifici di Adobe Campaign:

* Salvare un profilo
* Abbonati a un servizio
* Annullare l’abbonamento a un servizio

Questi moduli definiscono un parametro URL che accetta la chiave primaria crittografata di un profilo Adobe Campaign. In base a questo parametro URL, il modulo aggiorna i dati del profilo Adobe Campaign associato.

Anche se questi moduli vengono creati in modo indipendente, in un caso d’uso tipico viene generato un collegamento personalizzato a una pagina di modulo all’interno del contenuto della newsletter, in modo che i destinatari possano aprire il collegamento e apportare modifiche ai dati del loro profilo (sia che si tratti dell’annullamento dell’abbonamento, dell’abbonamento o dell’aggiornamento del profilo).

Il modulo viene aggiornato automaticamente in base all’utente. Per ulteriori informazioni, vedere [Modifica contenuto modulo](#editing-form-content).

## Come rendere disponibile un modello {#making-a-template-available}

Prima di poter creare moduli specifici per Adobe Campaign, è necessario rendere disponibili i diversi modelli nell’applicazione AEM.

Adobe Campaign Prima di tutto, verifica che la connessione tra le istanze di authoring e pubblicazione funzioni correttamente. Consulta [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Assicurati che la proprietà **acMapping** nel nodo **jcr:content** della pagina sia impostata su **mapRecipient** o **profile** quando utilizzi rispettivamente Adobe Campaign 6.1.x o Adobe Campaign Standard
>

### Creazione di un modulo {#creating-a-form}

1. Inizia in siteadmin.
1. Scorrere la struttura ad albero per arrivare al punto in cui si desidera creare il modulo nel sito Web scelto.
1. Seleziona **Nuovo** > **Nuova pagina...**.
1. Seleziona il modello **Profilo Adobe Campaign (AC 6.1)** o **Profilo Adobe Campaign (ACS)** e immetti le proprietà della pagina.

   >[!NOTE]
   >
   >Se il modello non è disponibile, vedere la sezione [Come rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

1. Fai clic su **Crea** per creare il modulo.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Puoi quindi [modificare e configurare il contenuto del modulo](#editing-form-content).

## Modifica del contenuto di un modulo {#editing-form-content}

Forms dedicato ad Adobe Campaign dispone di componenti specifici. Questi componenti dispongono di un’opzione che consente di collegare ogni campo del modulo a un campo del database di Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedere [Come rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Questa sezione descrive solo collegamenti specifici ad Adobe Campaign. Per ulteriori informazioni su una panoramica più generale sull&#39;utilizzo dei moduli in Adobe Experience Manager, vedere [Componenti Editmode](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Passare al modulo da modificare.
1. Nella casella degli strumenti, seleziona **Pagina** > **Proprietà pagina...**, quindi passa alla scheda **Servizi cloud** della finestra popup.
1. Aggiungere il servizio Adobe Campaign facendo clic su **Aggiungi servizio** e selezionando la configurazione corrispondente all&#39;istanza Adobe Campaign nell&#39;elenco a discesa del servizio. Questa configurazione viene eseguita durante la configurazione della connessione tra le istanze. Per ulteriori informazioni, vedere [Connessione di AEM ad Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessario, sblocca la configurazione facendo clic sull’icona del lucchetto per poter aggiungere il servizio Adobe Campaign.

1. Accedere ai parametri generali del modulo utilizzando il pulsante **Modifica** presente all&#39;inizio del modulo. La scheda **Modulo** consente di selezionare una pagina di ringraziamento alla quale l&#39;utente verrà reindirizzato dopo aver convalidato il modulo.

   Il modulo **Avanzate** ti consente di selezionare il tipo di modulo. Il campo **Opzioni post** consente di scegliere tra tre tipi di Adobe Campaign Form:

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: Abbonati ai servizi**: consente di gestire gli abbonamenti di un destinatario in Adobe Campaign.
   * **Adobe Campaign: annulla abbonamento a servizi**: consente di annullare gli abbonamenti di un destinatario in Adobe Campaign.

   Il campo **Configurazione azione** consente di specificare se si desidera creare o meno il profilo del destinatario nel database di Adobe Campaign, se non esiste ancora. A tale scopo, selezionare l&#39;opzione **Crea utente se non esistente**.

1. Aggiungere i componenti selezionati trascinandoli dalla casella degli strumenti e rilasciandoli nel modulo. Per ulteriori informazioni sui componenti specifici di Adobe Campaign disponibili, vedere [Componenti di Adobe Form](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configurare i campi aggiunti facendo doppio clic su di essi. La scheda **Adobe Campaign** ti consente di collegare il campo a un campo nella tabella dei destinatari di Adobe Campaign. Puoi anche specificare se il campo fa parte della chiave di riconciliazione, che consente di riconoscere i destinatari già presenti nel database di Adobe Campaign.

   >[!CAUTION]
   >
   >Il **Nome elemento** deve essere diverso per ogni campo modulo. Se necessario, modificala.
   >
   >Ogni modulo deve contenere un componente **Chiave primaria crittografata** per gestire correttamente i destinatari nel database di Adobe Campaign.

1. Attiva la pagina selezionando **Pagina** > **Attiva pagina** nella casella degli strumenti. La pagina viene attivata sul sito. Per visualizzarlo, vai all’istanza della pubblicazione AEM. I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.

## Verifica di un modulo {#testing-a-form}

Dopo aver creato un modulo e averne modificato il contenuto, può essere opportuno verificare manualmente il funzionamento previsto.

>[!NOTE]
>
>È necessario disporre di un componente **Chiave primaria crittografata** in ogni modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura si immette il numero epk manualmente, in pratica, gli utenti riceveranno un collegamento a questa pagina (se annullare l’abbonamento, abbonarsi o aggiornare il profilo) all’interno di una newsletter. In base all’utente, il pk si aggiorna automaticamente.
>
>Per creare il collegamento, si utilizza la variabile **Identificatore risorsa principale**(Adobe Campaign Standard) o **Identificatore crittografato** (Adobe Campaign 6.1) (ad esempio, in un componente **Text &amp; Personalization (Campaign)**), che collega al codice postale in Adobe Campaign.

A questo scopo, devi ottenere manualmente l’EPK di un profilo Adobe Campaign e quindi aggiungerlo all’URL:

1. Per ottenere la chiave principale crittografata (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard - Passa a **Profili e tipi di pubblico** > **Profili**, in cui sono elencati i profili esistenti. Accertati che nella tabella sia visualizzato il campo **Identificatore risorsa principale** in una colonna (per configurarlo, tocca o fai clic su **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign 6.11, vai a **Profili e destinazioni** > **Destinatari**, in cui sono elencati i profili esistenti. Assicurarsi che nella tabella sia visualizzato il campo **Identificatore crittografato** in una colonna (per configurare questo campo, fare clic con il pulsante destro del mouse su una voce e selezionare **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, apri la pagina del modulo nell’istanza di pubblicazione e aggiungi l’EPK del passaggio 1 come parametro URL: utilizza lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Il modulo può ora essere utilizzato per modificare i dati e le sottoscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e aver inviato il modulo, puoi verificare in Adobe Campaign che i dati appropriati siano stati aggiornati.

I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.
