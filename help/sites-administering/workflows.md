---
title: Amministrazione dei flussi di lavoro
description: Scopri come automatizzare le attività di Adobe Experience Manager utilizzando i flussi di lavoro.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
exl-id: 330f5cc5-1af4-4777-b386-b0755e6781df
source-git-commit: d37df3dc09122909adbb62ede6634939af105e06
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# Amministrazione dei flussi di lavoro{#administering-workflows}

I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM). Flussi di lavoro:

* Consiste in una serie di passaggi eseguiti in un ordine specifico.

   * Ogni passaggio esegue un’attività distinta, ad esempio l’attesa dell’input dell’utente, l’attivazione di una pagina o l’invio di un messaggio e-mail.

* Può interagire con le risorse nell’archivio, gli account utente e i servizi AEM.
* Può coordinare attività complicate che coinvolgono qualsiasi aspetto di AEM.

I processi aziendali stabiliti dalla tua organizzazione possono essere rappresentati come flussi di lavoro. Ad esempio, il processo di pubblicazione dei contenuti dei siti web include in genere passaggi quali l’approvazione e l’approvazione da parte di vari soggetti interessati. Questi processi possono essere implementati come flussi di lavoro di AEM e applicati a pagine di contenuti e risorse.

* [Avvio dei flussi di lavoro](/help/sites-administering/workflows-starting.md)
* [Amministrazione delle istanze dei flussi di lavoro](/help/sites-administering/workflows-administering.md)
* [Gestione dell’accesso ai flussi di lavoro](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Applicazione e partecipazione ai flussi di lavoro: [Utilizzo dei flussi di lavoro](/help/sites-authoring/workflows.md).
>* Creazione di modelli di flusso di lavoro ed estensione delle funzionalità del flusso di lavoro: [Sviluppo ed estensione dei flussi di lavoro](/help/sites-developing/workflows.md).
>* Miglioramento delle prestazioni dei flussi di lavoro che utilizzano risorse server significative: [Elaborazione simultanea dei flussi di lavoro](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>

## Modelli e istanze del flusso di lavoro {#workflow-models-and-instances}

I [modelli di flusso di lavoro](/help/sites-developing/workflows.md#model) in AEM rappresentano e implementano i processi aziendali:

* In genere agiscono su pagine o risorse per ottenere un risultato specifico.
* Queste pagine e/o risorse sono denominate payload del flusso di lavoro.
* I modelli di flusso di lavoro sono costituiti da una serie di passaggi che eseguono un&#39;attività specifica.
* Il payload viene passato da un passaggio all’altro con l’avanzare del flusso di lavoro.

All’avvio (esecuzione) di un modello di flusso di lavoro, viene creata un’istanza di flusso di lavoro. Un modello di flusso di lavoro può essere avviato più volte, ogni volta generando un’istanza di flusso di lavoro distinta. Per ogni istanza, vengono eseguiti i passaggi definiti dal modello di flusso di lavoro.

>[!CAUTION]
>
>I passaggi eseguiti sono quelli definiti dal modello di flusso di lavoro *al momento della generazione dell&#39;istanza*. Per ulteriori dettagli, vedi [Sviluppo ed estensione dei flussi di lavoro - Modelli](/help/sites-developing/workflows.md#model).

Le istanze del flusso di lavoro avanzano nel seguente ciclo di vita:

1. Il modello di flusso di lavoro viene avviato e viene creata ed eseguita un’istanza di flusso di lavoro.

   1. Il payload dell’istanza del flusso di lavoro viene identificato all’avvio del modello.
   1. La variante è di fatto una copia del modello (come al momento della creazione).
   1. Gli autori, gli amministratori o i servizi di AEM possono avviare i modelli di flusso di lavoro.

1. Viene eseguito il primo passaggio del modello di flusso di lavoro.
1. Il passaggio viene completato e il motore del flusso di lavoro utilizza il modello per determinare il passaggio successivo da eseguire.
1. I passaggi successivi nel modello di flusso di lavoro vengono eseguiti e completati.
1. Una volta completato il passaggio finale, l’istanza del flusso di lavoro viene completata e quindi archiviata.

AEM fornisce molti utili modelli di flusso di lavoro. Inoltre, gli sviluppatori dell’organizzazione possono creare modelli di flusso di lavoro personalizzati, personalizzati in base alle esigenze specifiche dei processi aziendali.

## Passaggi del flusso di lavoro {#workflow-steps}

Quando vengono eseguiti, i passaggi del flusso di lavoro sono associati a un’istanza del flusso di lavoro. La cronologia di un’istanza del flusso di lavoro include informazioni su ogni passaggio eseguito per l’istanza. Queste informazioni sono utili per l&#39;analisi dei problemi che si verificano durante l&#39;esecuzione.

Un utente o un servizio esegue i passaggi del flusso di lavoro, a seconda del tipo di passaggio:

* Quando un utente esegue un passaggio, gli viene assegnato un elemento di lavoro inserito nella casella in entrata. L’utente è responsabile del completamento manuale del passaggio in modo che l’istanza del flusso di lavoro possa progredire.
* Quando un servizio esegue un passaggio, al completamento l&#39;istanza del flusso di lavoro passa automaticamente al passaggio successivo.

>[!NOTE]
>
>Se si verifica un errore, l’implementazione del servizio/passaggio deve gestire il comportamento di uno scenario di errore. Il motore del flusso di lavoro stesso tenta nuovamente il processo, quindi registra un errore e arresta l’istanza.

## Stato e azioni del flusso di lavoro {#workflow-status-and-actions}

Un flusso di lavoro può avere uno dei seguenti stati:

* **IN ESECUZIONE**: l&#39;istanza del flusso di lavoro è in esecuzione.
* **COMPLETED**: l&#39;istanza del flusso di lavoro è stata terminata.

* **SOSPESO**: contrassegna il flusso di lavoro come sospeso. Tuttavia, consulta la nota di attenzione seguente su un problema noto con questo stato.
* **ABORTED**: l&#39;istanza del flusso di lavoro è stata terminata.
* **STALE**: l&#39;avanzamento dell&#39;istanza del flusso di lavoro richiede l&#39;esecuzione di un processo in background, ma non è possibile trovare il processo nel sistema. Questa situazione può verificarsi quando si verifica un errore durante l’esecuzione del flusso di lavoro.

>[!NOTE]
>
>Quando l&#39;esecuzione di un passaggio del processo genera errori, il passaggio viene visualizzato nella cartella Posta in arrivo dell&#39;amministratore e lo stato del flusso di lavoro è **IN ESECUZIONE**.

A seconda dello stato, è possibile eseguire azioni sulle istanze del flusso di lavoro in esecuzione quando è necessario intervenire nella normale progressione di un’istanza del flusso di lavoro:

* **Sospendi**: la sospensione modifica lo stato del flusso di lavoro in Sospeso. Vedi Attenzione di seguito:

>[!CAUTION]
>
>Si è verificato un problema noto quando si contrassegna lo stato di un flusso di lavoro come &quot;Sospendi&quot;. In questo stato, è possibile intervenire sugli elementi del flusso di lavoro sospesi in una casella in entrata.

* **Riprendi**: riavvia un flusso di lavoro sospeso nello stesso punto dell&#39;esecuzione in cui è stato sospeso, utilizzando la stessa configurazione.
* **Termina**: termina l&#39;esecuzione del flusso di lavoro e modifica lo stato in **INTERROTTO**. Impossibile riavviare un&#39;istanza di flusso di lavoro interrotta.
