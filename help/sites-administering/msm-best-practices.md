---
title: Best practice MSM
description: Trova le best practice compilate dai team tecnici e di consulenza di Adobe per iniziare a utilizzare AEM Multi Site Manager.
topic-tags: site-features, best-practices
feature: Multi Site Manager
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 907ed679-5a91-4581-b0ab-ed550586da71
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 34%

---

# Best practice MSM{#msm-best-practices}

## Generale {#general}

MSM è un framework configurabile per automatizzare la distribuzione dei contenuti. Le implementazioni spesso coinvolgono parti importanti di un sito Web e si estendono su più organizzazioni e aree geografiche. È quindi vivamente consigliato pianificare le implementazioni MSM con la stessa attenzione con cui pianifichi il tuo sito Web:

* Pianifica attentamente **la struttura e i flussi di contenuto** prima di iniziare l&#39;implementazione.
* **Mantieni al minimo la quantità di Live Copy.** L&#39;elaborazione delle Live Copy richiede molte risorse. Più Live Copy esistono nel sistema, più possono esserne influenzate le prestazioni: dall’elaborazione degli indici Live Copy interni, alle operazioni Live Copy come i rollout, alle operazioni dell’interfaccia utente come la visualizzazione delle relazioni Live Copy nella barra dei riferimenti di amministrazione di Sites. Si consiglia di creare Live Copy di siti o rami di un sito, in cui le relazioni Live Copy vengono ereditate dalle pagine del sito o del ramo. Evita di creare singole Live Copy per le pagine di un sito o di un ramo quando l’intera struttura può essere trasformata in una Live Copy.
* **Personalizza tutto il necessario, ma il meno possibile.** Sebbene MSM supporti un elevato grado di personalizzazione (ad esempio le configurazioni di rollout), in genere la best practice per le prestazioni, l&#39;affidabilità e l&#39;aggiornamento del sito Web è quella di ridurre al minimo la personalizzazione.
* Stabilisci anticipatamente un modello di **governance** e forma gli utenti di conseguenza per assicurarti che proceda tutto in maniera ottimale. Dal punto di vista della governance, una best practice consiste nel **ridurre al minimo l&#39;autorità di cui dispongono i produttori locali di contenuti** per allocare/connettere contenuti ad altri utenti locali e alle rispettive Live Copy. Ciò è dovuto al fatto che le ereditarietà chained non gestite possono aumentare notevolmente la complessità di una struttura MSM e comprometterne le prestazioni e l&#39;affidabilità.

* Una volta che esiste un piano per la struttura, i flussi di contenuto, l&#39;automazione e la governance - **prototipo e verifica accuratamente il sistema**, prima di avviare l&#39;implementazione live.
* Tieni presente che **Adobe Consulting e i principali System Integrator** hanno una solida esperienza nella pianificazione e nell&#39;implementazione dell&#39;automazione dei contenuti con MSM, per cui possono aiutarti sia all&#39;inizio del progetto MSM che durante l&#39;intera implementazione.

>[!NOTE]
>
>Ulteriori informazioni sull’utilizzo di MSM sono disponibili negli articoli della Knowledge Base:
>
>* [Risoluzione dei problemi e domande frequenti relativi a MSM](troubleshoot-msm.md)
>

>[!NOTE]
>
>È inoltre possibile utilizzare il [componente Riferimento](/help/sites-authoring/default-components-foundation.md#reference) per riutilizzare una singola pagina o paragrafo. Nota bene:
>
>* MSM è più flessibile e consente un controllo dettagliato su quali contenuti vengono sincronizzati e quando.
>* [I componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono ora consigliati rispetto ai componenti di base.
>

## Sorgenti Live Copy e configurazioni Blueprint {#live-copy-sources-and-blueprint-configurations}

Tieni presente che una Live Copy può essere creata utilizzando [pagine normali](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) o una [configurazione blueprint](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Entrambi sono casi d’uso validi.

I vantaggi aggiuntivi dell’utilizzo di una configurazione blueprint sono i seguenti:

* Consenti all&#39;autore di utilizzare l&#39;opzione **Rollout** su una blueprint per inviare (esplicitamente) le modifiche alle Live Copy che ereditano da questa blueprint.
* Consenti all&#39;autore di utilizzare **Crea sito**, in modo che l&#39;utente possa selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definisci una configurazione di rollout predefinita per le Live Copy che hanno una relazione con la blueprint.

Nel caso in cui non venga fatto riferimento a una configurazione blueprint, i rollout possono essere avviati solo dalle Live Copy stesse, essenzialmente richiamando il contenuto dal sorgente.

Quando crei un sito con Live Copy, è vantaggioso creare configurazioni blueprint per garantire la disponibilità dell’intero set di funzioni MSM.

>[!NOTE]
>
>Non è possibile eseguire il rollout dei CUG nella scheda Autorizzazioni in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione della Live Copy.

## Sincronizzazione dei componenti e dei contenitori {#components-and-container-synchronization}

In generale, la regola di rollout in MSM per quanto riguarda la sincronizzazione dei componenti è:

* I componenti vengono implementati per sincronizzare tutte le risorse contenute nella blueprint.
* I contenitori sincronizzano solo la risorsa corrente.

Ciò significa che i componenti sono trattati come un aggregato e in un rollout il componente stesso e tutti i suoi figli vengono sostituiti con quelli nei progetti. Ciò significa che se una risorsa viene aggiunta localmente a tale componente, andrà persa per il contenuto della blueprint al momento del rollout.

Per supportare la nidificazione dei componenti in modo che i componenti aggiunti localmente vengano mantenuti in un rollout, il componente deve essere dichiarato come contenitore. Ad esempio, il parsys predefinito è dichiarato come contenitore in modo da poter supportare contenuti aggiunti localmente.

>[!NOTE]
>
>Aggiungi la proprietà `cq:isContainer` al componente per designarlo come contenitore.

## Crea sito {#create-site}

Tieni presente che AEM dispone di due approcci principali per la creazione di Live Copy:

* Durante la [creazione di una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

  Questo può essere considerato l’approccio più generico, che consente di creare Live Copy da qualsiasi pagina. La struttura del contenuto di una Live Copy corrisponde esattamente all’origine.

* Quando [si crea un sito](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

  Si tratta di un approccio più specializzato, principalmente per la creazione di siti Web con una struttura multilingue.

Di seguito sono riportate alcune considerazioni da tenere presenti durante la creazione di un sito:

* Per creare un sito, è necessaria una [configurazione blueprint](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Per consentire la selezione dei percorsi linguistici da creare in un nuovo sito, le lingue root corrispondenti devono esistere nella blueprint (sorgente).
* Una volta creato un [nuovo sito come Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (utilizzando **Crea**, quindi **Sito**), i primi due livelli di questa Live Copy sono *Shallow*. Gli elementi figli della pagina non appartengono alla relazione live, ma se viene trovata una relazione live corrispondente al trigger, verrà comunque generato un rollout.

  Consente di evitare:

   * aggiunta manuale di lingue nella blueprint (sotto il primo livello)
   * aggiungere manualmente il contenuto direttamente sotto la lingua root,
   * non comporta il trasferimento automatico di questo nuovo contenuto alla live copy al momento del rollout.

## Siti Web MSM e multilingue {#msm-and-multilingual-websites}

MSM può contribuire alla creazione di siti Web multilingue in due modi:

* Durante la creazione di lingue master.

   * Sebbene MSM stesso **non fornisca la traduzione del contenuto**, può essere integrato con connettori di traduzione di terze parti che lo fanno. Tieni presente che:

      * MSM consente di annullare l’ereditarietà a livello di pagina e/o di componente. Questo aiuta a evitare la sovrascrittura dei contenuti tradotti (da una Live Copy, con contenuti non ancora tradotti da una blueprint) al prossimo rollout.
      * Alcuni connettori di traduzione di terze parti automatizzano questa gestione delle ereditarietà MSM.

        Per ulteriori informazioni, rivolgiti al fornitore di servizi di traduzione.

      * Un approccio alternativo per la creazione e la traduzione di lingue master consiste nell’utilizzare copie in lingua insieme al Translation Integration Framework di AEM preconfigurato.

* Durante il rollout del contenuto dai master lingua.

   * Ad esempio, dal master in lingua francese a siti specifici per paese, come Francia/francese, Canada/francese, Svizzera/francese.

Per ulteriori informazioni consulta [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) e [Best practice per la traduzione](/help/sites-administering/tc-bp.md).

## Modifiche alla struttura e rollout {#structure-changes-and-rollouts}

Le modifiche alla struttura del contenuto in una struttura blueprint/sorgente vengono riportate in modo diverso in una Live Copy. Dipende dal tipo di modifica:

* **La creazione di** nuove pagine in una blueprint determinerà la creazione delle pagine corrispondenti in Live Copy dopo il rollout con la configurazione di rollout standard.

* **L&#39;eliminazione di** pagine in una blueprint determinerà l&#39;eliminazione delle pagine corrispondenti dalle Live Copy dopo il rollout con la configurazione di rollout standard.

* **Lo spostamento di** pagine in una blueprint **non** determinerà lo spostamento delle pagine corrispondenti nelle Live Copy dopo il rollout con la configurazione di rollout standard:

   * Questo comportamento si spiega con il fatto che lo spostamento di una pagina include implicitamente l’eliminazione di una pagina. Questo potrebbe causare un comportamento imprevisto al momento della pubblicazione, in quanto l’eliminazione delle pagine sull’autore disattiva automaticamente il contenuto corrispondente al momento della pubblicazione. Questo può anche avere un effetto a catena sugli elementi correlati come collegamenti, segnalibri e altri.
   * L’ereditarietà dei contenuti nelle rispettive pagine Live Copy viene aggiornata per riflettere la nuova posizione delle loro sorgenti nella blueprint.
   * Per realizzare completamente lo spostamento di una pagina da una blueprint a una Live Copy, considera le seguenti best practice:

>[!NOTE]
>
>Funzionerà solo con il trigger [Al momento del rollout](/help/sites-administering/msm-sync.md#rollout-triggers).

* Crea una configurazione di rollout personalizzata:

   * Questa nuova configurazione deve includere l’azione:

     `PageMoveAction`

     Non aggiungere altre azioni a questa configurazione.

* Posiziona la nuova configurazione:

   * Per eseguire il rollout completo della pagina, spostala durante l’eliminazione delle rispettive pagine nella posizione precedente nella Live Copy:

      * Posiziona la configurazione appena creata prima della configurazione di rollout standard.

        La configurazione di rollout standard si occuperà di eliminare le pagine nella loro posizione precedente.

   * Per distribuire lo spostamento della pagina mantenendo le rispettive pagine nella vecchia posizione nelle Live Copy (essenzialmente duplicando il contenuto):

      * Posiziona la configurazione appena creata dopo la configurazione di rollout standard.

        In questo modo nessun contenuto verrà eliminato nella Live Copy o disattivato dalla pubblicazione.

## Personalizzazione dei rollout {#customizing-rollouts}

Le configurazioni di rollout MSM sono altamente personalizzabili. L’automazione dei rollout può avere conseguenze di vasta portata. Come best practice, pianifica *molto* attentamente prima, ad esempio:

* automazione dei rollout; ad esempio, con [trigger onModify](#onmodify),
* personalizzazione di [tipi di nodo/proprietà](#node-types-properties),
* avvio dei flussi di lavoro successivi,
* e/o l’attivazione del contenuto come parte dei rollout.

### onModify {#onmodify}

Quando utilizzi il [trigger di rollout](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` tieni presente che:

* L&#39;automazione dei rollout con `onModify` trigger può avere un impatto negativo sulle prestazioni dell&#39;authoring, in quanto attiva i rollout dopo *ogni* modifica di pagina.

* Il risultato del rollout può differire da quello previsto, ad esempio:

   * Non puoi specificare l’ordine degli eventi di modifica risultanti.
   * L&#39;architettura basata su eventi non può garantire la sequenza degli eventi passati al Rollout Manager.

* L’utilizzo di tale configurazione di rollout potrebbe causare conflitti se si verificano aggiornamenti simultanei della stessa risorsa.

Pertanto, ti consigliamo di *utilizzare solo* trigger `onModify` se i vantaggi dell&#39;avvio automatico del rollout superano eventuali problemi di prestazioni.

### Tipi di nodo/proprietà {#node-types-properties}

Ricorda che:

* Oltre a personalizzare le azioni di rollout, MSM ti consente anche di personalizzare le proprietà dei nodi in fase di rollout. La configurazione di [MSM OSGi consente di escludere i tipi di nodo](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) dall&#39;essere copiati dall&#39;origine alla Live Copy.

## Ulteriori informazioni {#further-information}

Questa e le pagine seguenti trattano i problemi correlati:

* [Creazione e sincronizzazione di Live Copy](/help/sites-administering/msm-livecopy.md)
* [Panoramica Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitti di rollout MSM](/help/sites-administering/msm-rollout-conflicts.md)
