---
title: Risoluzione dei problemi di replica
description: Questo articolo fornisce informazioni su come risolvere i problemi di replica.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 015def31-c7de-42b3-8218-1284afcb6921
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Risoluzione dei problemi di replica{#troubleshooting-replication}

Questa pagina fornisce informazioni su come risolvere i problemi di replica.

## Problema {#problem}

La replica (replica non inversa) non riesce per qualche motivo.

## Risoluzione {#resolution}

Esistono diversi motivi per cui la replica non riesce. Questo articolo spiega l’approccio che si potrebbe adottare quando si analizzano questi problemi.

**Le repliche vengono attivate quando si fa clic sul pulsante Attiva? Se NON lo è, eseguire le operazioni seguenti:**

1. Vai a /crx/de/index.jsp e accedi come amministratore.
1. Verifica se esiste un nodo /bin/replicate o /bin/replicate.json. Se il nodo esiste, eliminalo e salvalo.

**Le repliche vengono messe in coda nelle code dell&#39;agente di replica?**

Seleziona questa opzione andando su /etc/replication/agents.author.html, quindi fai clic sugli agenti di replica da controllare.

**Se una o più code di agenti sono bloccate:**

1. La coda mostra lo stato **bloccato**? In caso affermativo, l’istanza Publish non è in esecuzione o non risponde? Controlla l’istanza Publish per vedere cosa c’è di sbagliato. In altre parole, controlla i registri e verifica se è presente un errore OutOfMemory o un altro problema. Se è semplicemente lento, prendi le immagini thread e analizzale.
1. Lo stato della coda indica che **la coda è attiva - n. in sospeso**? In pratica, il processo di replica potrebbe essere bloccato in un socket letto in attesa della risposta dell’istanza Publish o di Dispatcher. Ciò potrebbe significare che l’istanza Publish o Dispatcher è sotto un carico elevato o è bloccata in un blocco. In questo caso, prendi le immagini thread da authoring e pubblica.

   * Apri le immagini thread dall’autore in un analizzatore di immagini thread, verifica se il processo di eventi sling dell’agente di replica è bloccato in un socketRead.
   * Apri le immagini thread da Publish in un analizzatore di immagini thread e analizza cosa potrebbe causare la mancata risposta dell’istanza Publish. Dovresti trovare un thread il cui nome contiene POST /bin/receive che è il thread che riceve la replica dall’autore.

**Se tutte le code dell&#39;agente sono bloccate**

1. È possibile che un determinato contenuto non possa essere serializzato in /var/replication/data a causa di un danneggiamento dell’archivio o per altri problemi. Controlla logs/error.log per un errore correlato. Per cancellare l’elemento di replica non valido, effettua le seguenti operazioni:

   1. Vai a https://&lt;host>:&lt;port>/crx/de e accedi come utente amministratore.
   1. Fare clic su Strumenti nel menu principale.
   1. Fare clic sul pulsante della lente di ingrandimento.
   1. Selezionare &quot;XPath&quot; come Tipo.
   1. Nella casella &quot;Query&quot; immettere l&#39;ordine di query /jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job) per @slingevent:created
   1. Fare clic su &quot;Search&quot; (Cerca).
   1. Nei risultati, gli elementi principali sono gli ultimi sette processi con eventi. Fai clic su ciascuna replica e trova le repliche bloccate corrispondenti a quelle visualizzate nella parte superiore della coda.

**Creare un replication.log**

A volte è utile impostare tutte le registrazioni di replica da aggiungere in un file di registro separato a livello di DEBUG. Per effettuare questo collegamento:

1. Vai a https://host:port/system/console/configMgr e accedi come amministratore.
1. Trovare la configurazione del logger di registrazione Sling Apache e creare un&#39;istanza facendo clic sul pulsante **+** a destra della configurazione di fabbrica. Verrà creato un nuovo logger di registrazione.
1. Imposta la configurazione come segue:

   * Livello registro: DEBUG
   * File di registro: logs/replication.log
   * Logger: com.day.cq.replication

1. Se pensi che il problema sia correlato in qualche modo a sling eventing/jobs, puoi anche aggiungere questo pacchetto Java™ nelle categorie:org.apache.sling.event

## Sospensione coda agente di replica  {#pausing-replication-agent-queue}

A volte può essere opportuno mettere in pausa la coda di replica per ridurre il carico sul sistema di authoring, senza disabilitarla. Attualmente, ciò è possibile solo tramite un hack di configurazione temporanea di una porta non valida. Dalla versione 5.4 in poi, il pulsante Pausa nella coda dell’agente di replica presenta alcune limitazioni

1. Lo stato non è persistente, il che significa che se si riavvia un server o se il bundle di replica viene riciclato, viene ripristinato lo stato di esecuzione.
1. La pausa è inattiva per un periodo più breve (OOB 1 ora dopo nessuna attività con replica da parte di altri thread) e non per un periodo più lungo. Perché c’è una funzione in sling che evita i thread inattivi. In pratica, verifica se un thread della coda processi è stato inutilizzato per un periodo di tempo più lungo. In tal caso, avvia i cicli di pulizia. A causa del ciclo di pulizia, il thread viene arrestato e l&#39;impostazione di pausa viene quindi persa. Poiché i processi sono persistenti, viene avviato un nuovo thread per elaborare la coda che non contiene dettagli sulla configurazione in pausa. A causa di questa coda si trasforma in stato di esecuzione.

## Le autorizzazioni pagina non vengono replicate al momento dell’attivazione dell’utente {#page-permissions-are-not-replicated-on-user-activation}

Le autorizzazioni di pagina non vengono replicate perché sono memorizzate nei nodi a cui è concesso l’accesso, non con l’utente.

In generale, le autorizzazioni di pagina non devono essere replicate dall’autore alla pubblicazione e non sono per impostazione predefinita. Questo perché i diritti di accesso dovrebbero essere diversi in questi due ambienti. Pertanto, Adobe consiglia di configurare gli ACL in fase di pubblicazione, separatamente da Author.

## Coda di replica bloccata durante la replica delle informazioni sullo spazio dei nomi da Author a Publish {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

A volte la coda di replica viene bloccata quando si tenta di replicare le informazioni sullo spazio dei nomi dall’istanza di authoring all’istanza di pubblicazione. Ciò si verifica perché l&#39;utente di replica non dispone del privilegio `jcr:namespaceManagement`. Per evitare questo problema, assicurati che:

* L&#39;utente di replica (configurato nella scheda [Trasporto](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)>Utente) esiste anche nell&#39;istanza di pubblicazione.
* L’utente dispone dei privilegi di lettura e scrittura nel percorso in cui viene installato il contenuto.
* L&#39;utente dispone del privilegio `jcr:namespaceManagement` a livello di repository. È possibile concedere il privilegio nel modo seguente:

1. Accedere a CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) come amministratore.
1. Fare clic sulla scheda **Controllo di accesso**.
1. Seleziona **Archivio**.
1. Fai clic su **Aggiungi voce** (icona più).
1. Immettere il nome dell&#39;utente.
1. Selezionare `jcr:namespaceManagement` dall&#39;elenco dei privilegi.
1. Fai clic su **OK**.
