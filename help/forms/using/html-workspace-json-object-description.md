---
title: Descrizione oggetto JSON dell’area di lavoro di AEM Forms
description: Informazioni concettuali sugli oggetti JavaScript JSON utilizzati nell’area di lavoro di AEM Forms LiveCycle per la personalizzazione, l’estensione, la modifica e il riutilizzo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
exl-id: 1b6c09f7-6f89-4fe9-8217-bf1a301bf9cb
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 8%

---

# Descrizione oggetto JSON dell’area di lavoro di AEM Forms {#aem-forms-workspace-json-object-description}

Di seguito sono descritti gli oggetti JSON utilizzati nell’area di lavoro di AEM Forms.

1. Categoria

   Le categorie sono presenti nella scheda del processo iniziale dell&#39;area di lavoro. Queste categorie vengono utilizzate per classificare i punti d&#39;inizio.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>nome</td>
   <td>V</td>
   <td>Nome categoria</td>
  </tr>
  <tr>
   <td>id</td>
   <td>V</td>
   <td>ID categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>V</td>
   <td>Descrizione categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>V</td>
   <td>Contiene un ID della categoria padre<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>M</td>
   <td>Contiene un elenco di tutti i punti d'inizio presenti in una categoria</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>M</td>
   <td>Contiene l'elenco delle categorie figlio dirette di una categoria<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Tutti i punti iniziali e i Preferiti sono categorie definite sul lato client. La categoria Preferiti contiene tutti i punti d&#39;inizio contrassegnati dall&#39;utente come preferiti. La categoria Tutti i punti iniziali contiene tutti i punti iniziali.

1. Punto d&#39;inizio

   Il punto iniziale viene utilizzato per avviare un processo dall&#39;area di lavoro quando viene richiamato.

   | **Proprietà** | **Solo client** | **Commenti** |
   |---|---|---|
   | categoryId | V | Contiene l’ID della categoria a cui appartiene il punto d’inizio. |
   | descrizione | V | Contiene la descrizione di un punto d&#39;inizio. |
   | nome | V | Contiene il nome del punto d&#39;inizio. |
   | serializedImageTicket | V | Contiene un ticket immagine corrispondente al punto iniziale. Questo ticket di immagine viene utilizzato nel campo imageUrl del punto d’inizio per ottenere l’immagine del punto d’inizio dal server. |
   | serviceName | V | Contiene il nome del servizio per il punto d&#39;inizio. |
   | startpointId | V | Contiene l’ID del punto d’inizio. |
   | isFavorite | M | Indica se il punto d&#39;inizio è preferito o meno. True se il punto d&#39;inizio è il preferito, altrimenti false. |
   | isDefaultImage | M | Indica se esiste un&#39;immagine specificata per il processo. True se non è presente alcuna immagine associata al processo else false. |
   | attività | M | Contiene l&#39;attività creata quando viene richiamato il punto d&#39;inizio. |
   | imageUrl | M | Contiene l’URL dell’immagine corrispondente al punto d’inizio. |

1. Attività

   Le attività vengono assegnate a utenti/gruppi e includono un’interfaccia utente, un modulo o una Guida TV (obsoleta) che può essere compilata con i dati. Quando agli utenti viene assegnata un’attività, viene fornito loro il modulo o la Guida per completare e inviare.

<table>
 <tbody>
  <tr>
   <td>Proprietà<br /> </td>
   <td>Solo client<br /> </td>
   <td>Commenti<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>V</td>
   <td>La classe dell'attività è 'LC8' quando l'attività è lc8, altrimenti 'Standard'.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>V</td>
   <td>Contiene il timestamp del completamento dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>V</td>
   <td>Contiene l’ID di un gruppo a cui è possibile consultare l’attività. Viene impostato durante la progettazione del processo.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>V</td>
   <td>Contiene la marca temporale al momento della creazione dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>createId<br /> </td>
   <td>V</td>
   <td>Contiene l'ID dell'utente che ha creato l'attività.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>V</td>
   <td>Contiene dettagli sull'assegnazione corrente dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>scadenza<br /> </td>
   <td>V</td>
   <td>Contiene la marca temporale che indica quando un'attività raggiungerà la scadenza.<br /> </td>
  </tr>
  <tr>
   <td>descrizione<br /> </td>
   <td>V</td>
   <td>Contiene la descrizione dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>V</td>
   <td>Contiene il nome visualizzato dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>V</td>
   <td>Contiene l’ID di un gruppo a cui è possibile inoltrare l’attività. Viene impostato durante la progettazione del processo.<br /> </td>
  </tr>
  <tr>
   <td>istruzioni<br /> </td>
   <td>V</td>
   <td>Contiene istruzioni per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>V</td>
   <td>True se l'attività è bloccata.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>V</td>
   <td>True se è necessario aprire il modulo attività per completare l'attività.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>V</td>
   <td>Se è true, all'apertura dell'attività la schermata completa del modulo viene visualizzata per la prima volta.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>V</td>
   <td>Se è true, la route deve essere selezionata per completare l'attività.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>V</td>
   <td>Gli allegati vengono visualizzati se è vero.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>V</td>
   <td>Se true, l'attività viene creata dal punto iniziale.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>V</td>
   <td>True se l'attività è visibile nell'area di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>V</td>
   <td>Timestamp del prossimo promemoria.<br /> </td>
  </tr>
  <tr>
   <td>priorità<br /> </td>
   <td>V</td>
   <td>Contiene la priorità dell'attività.<br /> 1 = Priorità più alta<br /> 2 = Priorità alta<br /> 3 = Priorità normale<br /> 4 = Priorità bassa<br /> 5 = Priorità più bassa<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>V</td>
   <td>ID dell'istanza del processo di cui fa parte l'attività.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>V</td>
   <td>Stato dell'istanza di processo dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>V</td>
   <td>Contiene il numero di promemoria per l'attività.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>V</td>
   <td>Contiene un elenco di route associate all'attività. L'utente può completare l'attività selezionando una delle route dall'elenco route.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>V</td>
   <td>Contiene il nome della route selezionata al completamento dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>V</td>
   <td>Contiene il ticket immagine corrispondente all’attività. Questo ticket immagine viene utilizzato nel campo imageUrl dell'attività per ottenere l'immagine per l'attività dal server.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>V</td>
   <td>Contiene il nome del servizio per l'attività.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>V</td>
   <td>Contiene il titolo del servizio per l'attività.<br /> </td>
  </tr>
  <tr>
   <td>stato<br /> </td>
   <td>V</td>
   <td>1 = Creato (l'attività viene creata dal punto iniziale).<br /> 2 = Creato e salvato (l'attività viene creata dal punto iniziale e salvata).<br /> 3 = Assegnato (l'attività viene assegnata all'utente dopo l'avvio del processo).<br /> 4 = Assegnato e salvato (l'attività viene assegnata e salvata)<br /> 100 = Completata (attività completata).<br /> 101 = Scaduto (l'attività ha raggiunto la scadenza).<br /> 102 = Terminato<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>V</td>
   <td>Contiene il nome dell'attività impostata durante la progettazione del processo.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>V</td>
   <td>Contiene l'URL di riepilogo attività.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>V</td>
   <td>È un elenco di controllo di accesso per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>V</td>
   <td>ID di un'attività.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>V</td>
   <td>Timestamp dell'ultimo aggiornamento dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>M</td>
   <td>Contiene l'URL del modulo per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>M</td>
   <td>Contiene il tipo di modulo attività. Utilizzando questo campo, l'attività viene rappresentata sul client come PDF per, modulo SWF e così via.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>M</td>
   <td>Se true, le azioni di instradamento sono visibili nell'area di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>M</td>
   <td>Se true, azioni quali inoltra, consulta e condividi sono visibili nell'area di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>supportedOffline<br /> </td>
   <td>M</td>
   <td>Se è true, il modulo può essere portato offline. Solo per moduli PDF.<br /> </td>
  </tr>
  <tr>
   <td>supportedSave<br /> </td>
   <td>M</td>
   <td>Se true, l'utente può salvare l'attività.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>M</td>
   <td>Questo oggetto contiene opzioni utilizzate per inviare moduli PDF tramite lettore nel caso in cui il modulo PDF non contenga alcun pulsante di invio.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>M</td>
   <td>Indica se esiste un'immagine specificata per il processo. True se non è presente alcuna immagine associata al processo else false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>M</td>
   <td>Contiene un elenco di attività utilizzate nella scheda della cronologia dei dettagli dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>M</td>
   <td>True se l'utente connesso è il proprietario dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>M</td>
   <td>Contiene tutte le azioni che possono essere eseguite sull'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>M</td>
   <td>Contiene tutte le azioni di route disponibili per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>M</td>
   <td>Contiene comandi come inoltra, condividi e consulta se disponibili per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>M</td>
   <td>Contiene comandi come lock, unlock, abandon, return, claim e così via, se disponibili.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>M</td>
   <td>Contiene informazioni sull'istanza del processo dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Contiene la matrice di oggetti delle variabili di processo, se presenti.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>M</td>
   <td>Contiene l'elenco delle attività in sospeso per l'istanza di processo dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>M</td>
   <td>È un array di oggetti. Ogni oggetto contiene dettagli sulla route e il messaggio di conferma corrispondente, se presente.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>M</td>
   <td>URL per i dati del modulo di un'attività.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>M</td>
   <td>Questa è la configurazione per i moduli applicativi di terze parti.<br /> </td>
  </tr>
  <tr>
   <td>inviato<br /> </td>
   <td>M</td>
   <td>True se l'attività viene inviata.<br /> </td>
  </tr>
  <tr>
   <td>allegati<br /> </td>
   <td>M</td>
   <td>Elenco degli allegati per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>assegnazioni<br /> </td>
   <td>M</td>
   <td>Elenco delle assegnazioni di un'attività.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtro

   Il filtro è fondamentalmente una coda di utenti o gruppi. Quando un’attività viene assegnata a un utente/gruppo, viene aggiunta nella coda corrispondente.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>V</td>
   <td>True se la coda è la coda predefinita dell'utente connesso, altrimenti false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>nome<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome del proprietario della coda.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>V</td>
   <td>ID della coda.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>V</td>
   <td>Contiene il tipo di coda.<br /> 0 - Coda utenti.<br /> 1 Coda condivisa.<br /> 2. Coda gruppo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>M</td>
   <td>Contiene una query associata a un filtro. Questa query viene utilizzata per cercare le attività dall'elenco attività completo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>attività</td>
   <td>M</td>
   <td>Contiene l'elenco di tutte le attività che appartengono a un filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fuori sede

   È possibile gestire la pianificazione fuori sede e controllare il flusso di attività assegnate all&#39;utente in assenza dell&#39;utente.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong><br type="_moz" /> </td>
   <td><strong>Solo client</strong><br type="_moz" /> </td>
   <td><strong>Commenti</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>V</td>
   <td>Contiene oggetti array di pianificazioni fuori sede di un utente. In ogni oggetto di pianificazione, il campo startDate contiene la data di inizio della pianificazione e il campo endDate contiene la data di fine della pianificazione. Se endDate è null nella pianificazione, significa che l'utente non ha pianificato la data di fine della pianificazione fuori sede.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>V</td>
   <td>True se non è presente alcun designato primario nel caso in cui l'utente sia fuori sede.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>V</td>
   <td>True se l'utente è fuori sede.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>V</td>
   <td>Contiene i dettagli dell'utente assegnato come primario designato dall'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>V</td>
   <td>Contiene un array di oggetti per designare fuori sede specifico per il processo. In ogni oggetto designato specifico del processo, processName contiene il nome del processo, isNotDesignated è true se nessun utente è assegnato per il processo corrispondente e userDesignated è null se nessun altro utente ha assegnato i dettagli dell'utente assegnato per il processo corrispondente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processi<br type="_moz" /> </td>
   <td>M</td>
   <td>Contiene un elenco di tutti i processi disponibili per l'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>M</td>
   <td>Contiene le impostazioni fuori sede iniziali dell'utente recuperate inizialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>M</td>
   <td>Contiene le impostazioni fuori sede modificate.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>M</td>
   <td>Contiene un elenco di utenti in cui un utente connesso esegue la ricerca fino alla data corrente.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Istanza processo

   Quando un processo viene richiamato tramite l&#39;area di lavoro o il workbench, viene creata un&#39;istanza di processo.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>V</td>
   <td>Descrizione dell'istanza del processo<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>iniziatore</td>
   <td>V</td>
   <td>Nome dell'iniziatore di un'istanza del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>V</td>
   <td>ID dell'iniziatore dell'istanza del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>V</td>
   <td>Timestamp al completamento del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>V</td>
   <td>ID dell'istanza del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>V</td>
   <td>0 = Avviato<br /> 1 = In Esecuzione<br /> 2 = Completato<br /> 3 = Completato<br /> 4 = Terminato<br /> 5 = Terminato<br /> 6 = Sospeso<br /> 7 = In Sospensione<br /> 8 = In Sospensione<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>V</td>
   <td>Timestamp all'avvio del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>V</td>
   <td>Array di oggetti delle variabili di processo. Ogni oggetto variabile di processo contiene il nome, che è il nome della variabile di processo, il valore, che è il valore della variabile di processo e il tipo, che è il tipo della variabile di processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>elenco attività<br type="_moz" /> </td>
   <td>M</td>
   <td>Attività generate da questa istanza del processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nome processo

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>V</td>
   <td>Versione principale di un processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>V</td>
   <td>Versione secondaria di un processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>V</td>
   <td>Titolo del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>M</td>
   <td>Elenco delle istanze di processo per questo processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Oggetto assegnazione attività

   L&#39;oggetto assegnazione attività contiene informazioni sull&#39;assegnazione dell&#39;attività. Di seguito sono riportate le proprietà dell&#39;assegnazione dell&#39;attività.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>V</td>
   <td>Timestamp della creazione di questa assegnazione di un'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>V</td>
   <td>0 = Assegnazione iniziale<br /> 1 = Inoltra (l'attività è stata inoltrata al proprietario corrente dell'attività).<br /> 2 = Restituita (l'attività è stata restituita al proprietario corrente dell'attività dal proprietario precedente).<br /> 3 = Richiesto (l'attività è stata richiesta dal proprietario corrente dell'attività).<br /> 4 = riassegnazione (l'attività è stata assegnata al proprietario corrente dell'attività dopo l'escalation)<br /> 5 = Amministratore assegnato (l'attività è stata assegnata dall'amministratore al proprietario corrente dell'attività).<br /> 6 = Consultato ( L'attività è stata consultata dall'attuale proprietario)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>V</td>
   <td>Timestamp dell'aggiornamento dell'assegnazione di un'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>V</td>
   <td>ID coda del proprietario corrente dell'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome del proprietario corrente dell'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>V</td>
   <td>ID del proprietario corrente dell'attività.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Oggetto ACL attività

   L&#39;oggetto ACL dell&#39;attività contiene informazioni su autorizzazioni quali inoltro, condivisione, consultazione e così via di un&#39;attività. Di seguito sono riportate le proprietà dell&#39;ACL dell&#39;attività.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>V</td>
   <td>Se è true, è possibile aggiungere allegati all'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>V</td>
   <td>Se è true, è possibile aggiungere note all'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>V</td>
   <td>Se true, l'attività può essere reclamata.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>V</td>
   <td>Se true, è possibile consultare l'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>V</td>
   <td>Se true, l'attività può essere inoltrata.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>V</td>
   <td>Se true, l'attività può essere condivisa.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Allegato attività

   È possibile aggiungere allegati a un&#39;attività. L&#39;allegato può essere di tipo allegato e nota. Di seguito sono riportate le proprietà dell&#39;oggetto allegato.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>V</td>
   <td>Timestamp al momento della creazione dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>V</td>
   <td>ID dell'utente che ha aggiunto l'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome dell'utente che ha aggiunto l'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>V</td>
   <td>Descrizione dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>nomeFile<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>V</td>
   <td>ID dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>V</td>
   <td>Timestamp dell'ultima modifica dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>V</td>
   <td>Se true, la nota è una nota estesa (lunga).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>autorizzazioni<br type="_moz" /> </td>
   <td>V</td>
   <td>Autorizzazioni associate a un allegato. Il campo allowRead è per l'autorizzazione di lettura, allowWrite è per l'autorizzazione di scrittura, allowDelete è per l'autorizzazione di eliminazione.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dimensione<br type="_moz" /> </td>
   <td>V</td>
   <td>Dimensione dell'allegato in byte.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>V</td>
   <td>ID dell'attività a cui viene aggiunto l'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo<br type="_moz" /> </td>
   <td>V</td>
   <td>Il tipo è allegato per i file e il tipo è nota per le note.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>M</td>
   <td>Contiene la data di creazione dell'allegato in base alle impostazioni dell'interfaccia utente dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>M</td>
   <td>Descrizione dell'allegato formattato. Utilizzato per visualizzare caratteri speciali presenti nella descrizione dell'allegato nell'area di lavoro AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>M</td>
   <td>Nome allegato formattato. Utilizzato per visualizzare i caratteri speciali presenti nel nome dell’allegato nell’area di lavoro di AEM Forms. Solo per le note.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. User

   Di seguito sono riportate le proprietà dell&#39;oggetto utente.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>indirizzo<br type="_moz" /> </td>
   <td>V</td>
   <td>Indirizzo dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome comune dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>V</td>
   <td>Descrizione dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>V</td>
   <td>Elenco del gruppo di utenti.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome visualizzato dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>e-mail<br type="_moz" /> </td>
   <td>V</td>
   <td>ID e-mail dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>V</td>
   <td>True se l'utente è fuori sede.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>V</td>
   <td>Cognome dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>V</td>
   <td>ID dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>V</td>
   <td>Nome dell'organizzazione dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>V</td>
   <td>Indirizzo postale dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telefono<br type="_moz" /> </td>
   <td>V</td>
   <td>Numero di contatto dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>phoneNumber<br type="_moz" /> </td>
   <td>V</td>
   <td>Numero di contatto dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id utente<br type="_moz" /> </td>
   <td>V</td>
   <td>ID di accesso dell'utente.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
