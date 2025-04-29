---
title: Distribuzioni consigliate
description: Questo articolo descrive le topologie consigliate per AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 9baa4111-831a-4b68-9ce5-82aeeb06e07f
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 0%

---

# Distribuzioni consigliate{#recommended-deployments}

>[!NOTE]
>
>Questa pagina fa riferimento alle topologie consigliate per AEM. Per ulteriori informazioni sulle funzionalità di clustering e su come configurarle, consulta la [documentazione di Apache Sling Discovery API](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

I microKernel fungono da gestori di persistenza a partire da AEM 6.2. La scelta di un tipo di implementazione adatto alle tue esigenze dipende dallo scopo dell’istanza e dal tipo di implementazione che stai prendendo in considerazione.

Gli esempi seguenti indicano gli usi consigliati nelle configurazioni di AEM più comuni.

## Scenari di distribuzione {#deployment-scenarios}

### Singola istanza TarMK {#single-tarmk-instance}

In questo scenario, una singola istanza TarMK viene eseguita su un singolo server.

**Distribuzione predefinita per le istanze di authoring.**

![chlimage_1-15](assets/chlimage_1-15.png)

I vantaggi:

* Semplice
* Manutenzione semplice
* Buone prestazioni

Gli svantaggi:

* Non scalabile oltre i limiti della capacità del server
* Nessuna capacità di failover

### Standby a freddo TarMK {#tarmk-cold-standby}

Un’istanza TarMK funge da istanza primaria. L&#39;archivio dal sistema primario viene replicato in un sistema di failover in standby.

Il meccanismo di standby a freddo può essere utilizzato anche come backup perché l&#39;intero repository viene costantemente replicato sul server di failover. Il server di failover è in esecuzione in modalità standby a freddo, il che significa che solo HttpReceiver dell&#39;istanza è in esecuzione.

![chlimage_1-16](assets/chlimage_1-16.png)

I vantaggi:

* Semplicità
* Manutenzione
* Prestazioni
* Failover

Gli svantaggi:

* Non scalabile oltre i limiti della capacità del server
* Un server è inattivo la maggior parte delle volte
* Il failover non è automatico. Deve essere rilevato esternamente prima che il sistema di failover possa iniziare a gestire le richieste.

>[!NOTE]
>
>Per ulteriori informazioni su come configurare AEM con TarMK Cold Standby, consulta [questo](/help/sites-deploying/tarmk-cold-standby.md) articolo.

>[!NOTE]
>
>La distribuzione in standby a freddo in questo esempio di TarMK richiede che le istanze principale e in standby siano concesse in licenza separatamente, in quanto esiste una replica costante sul server di failover. Per ulteriori informazioni sulle licenze, consultare le [Condizioni generali di licenza di Adobe](https://www.adobe.com/legal/terms/enterprise-licensing.html).

### Farm TarMK {#tarmk-farm}

Più istanze Oak vengono eseguite ciascuna con un’istanza TarMK. Gli archivi TarMK sono indipendenti e devono essere sincronizzati.

Mantenendo sincronizzati gli archivi, il server di authoring pubblica lo stesso contenuto per ogni membro della farm. Per ulteriori informazioni, vedere [Replica](/help/sites-deploying/replication.md).

**Distribuzione predefinita per gli ambienti di pubblicazione.**

![chlimage_1-17](assets/chlimage_1-17.png)

I vantaggi:

* Prestazioni
* Scalabilità per l&#39;accesso in lettura
* Failover

### Cluster Oak con failover MongoMK per un&#39;elevata disponibilità in un singolo centro dati {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

>[!NOTE]
>
>La versione minima supportata di Mongo è Mongo 6.

Questo approccio implica che più istanze Oak accedono a un set di repliche MongoDB all’interno di un singolo data center, creando in effetti un cluster attivo-attivo per l’ambiente di authoring AEM. I set di replica in MongoDB vengono utilizzati per fornire elevata disponibilità e ridondanza in caso di errore hardware o di rete.

![chlimage_1-18](assets/chlimage_1-18.png)

I vantaggi:

* Possibilità di scalabilità orizzontale con le nuove istanze di authoring di AEM
* Elevata disponibilità, ridondanza e failover automatizzato del livello dati

Gli svantaggi:

* Le prestazioni possono essere inferiori rispetto a TarMK per alcuni scenari

### Cluster Oak con failover MongoMK in più centri dati {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

Questo approccio implica che più istanze di Oak accedono a un set di repliche MongoDB in più data center, creando in effetti un cluster attivo-attivo per l’ambiente di authoring AEM. Con più data center, la replica MongoDB offre la stessa elevata disponibilità e ridondanza, ma ora include la possibilità di gestire un&#39;interruzione del data center.

![oakclustermongofailover2datacenter](assets/oakclustermongofailover2datacenters.png)

I vantaggi:

* Possibilità di scalabilità orizzontale con le nuove istanze di authoring di AEM
* Elevata disponibilità, ridondanza e failover automatizzato del livello dati (comprese le interruzioni del centro dati)

>[!NOTE]
>
>Nel diagramma precedente, AEM Server 3 e AEM Server 4 presentano uno stato inattivo presupponendo una latenza di rete tra i server AEM nel centro dati 2 e il nodo primario MongoDB nel centro dati 1 superiore al requisito documentato in [Adobe Experience Manager con MongoDB - Elenchi di controllo](/help/sites-deploying/aem-with-mongodb.md#checklists). Se la latenza massima è compatibile con i requisiti, ad esempio tramite l’utilizzo di zone di disponibilità, anche i server AEM nel centro dati 2 possono essere attivi, creando un cluster AEM attivo-attivo in più centri dati.

>[!NOTE]
>
>Per ulteriori informazioni sui concetti dell&#39;architettura MongoDB descritti in questa sezione, vedere [Replica MongoDB](https://docs.mongodb.org/manual/replication/).

## Microkernel: quale usare {#microkernels-which-one-to-use}

La regola di base che deve essere presa in considerazione quando si sceglie tra i due micro kernel disponibili è che TarMK è progettato per le prestazioni, mentre MongoMK è utilizzato per la scalabilità.

Puoi utilizzare queste matrici di decisione per stabilire quale sia il tipo di distribuzione più adatto alle tue esigenze.

Adobe consiglia vivamente di utilizzare TarMK come tecnologia di persistenza predefinita utilizzata dai clienti in tutti gli scenari di implementazione, sia per le istanze Author che Publish di AEM, tranne nei casi di utilizzo descritti di seguito.

### Eccezioni per la scelta di AEM MongoMK rispetto a TarMK nelle istanze di authoring {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

Il motivo principale per scegliere il back-end di persistenza MongoMK su TarMK è quello di scalare le istanze orizzontalmente. Ciò significa avere due o più istanze di authoring attive in esecuzione in qualsiasi momento e utilizzare MongoDB come sistema di storage di persistenza. La necessità di eseguire più di un’istanza di authoring deriva in genere dal fatto che la capacità di CPU e di memoria di un singolo server, che supporta tutte le attività di authoring simultanee, non è più sostenibile.

È quasi impossibile prevedere quale sarà il modello di concorrenza esatto dopo la pubblicazione di un nuovo sito. Pertanto, Adobe consiglia di considerare i seguenti criteri quando si valuta se utilizzare MongoMK e due o più nodi attivi dell’istanza di authoring:

1. Numero di utenti con nome connessi in un giorno: in migliaia o più.
1. Numero di utenti simultanei: in centinaia o più.
1. Volume di acquisizioni di risorse al giorno: in centinaia di migliaia o più.
1. Volume giornaliero di modifiche di pagina: in centinaia di migliaia o più (inclusi aggiornamenti automatizzati tramite Multi Site Manager o acquisizioni di feed di notizie, ad esempio).
1. Volume di ricerche al giorno: in decine di migliaia o più.

>[!NOTE]
>
>[È possibile utilizzare un giorno difficile](/help/sites-developing/tough-day.md) per valutare le prestazioni dell&#39;applicazione del cliente nel contesto della configurazione hardware distribuita.

Una distribuzione minima con MongoDB implica in genere la seguente topologia:

* Un set di repliche MongoDB costituito da un nodo primario, due nodi secondari con ciascuna delle istanze MongoDB in esecuzione in una zona di disponibilità con una latenza inferiore a 15 millisecondi su ciascun nodo;
* Un cluster di istanze di authoring con un nodo principale, un nodo non principale ed entrambi attivi in qualsiasi momento, con ciascuna delle istanze di authoring in esecuzione in ciascun centro dati, dove sono in esecuzione le istanze primarie e secondarie di MongoDB.

Inoltre, si consiglia vivamente di configurare l’archivio dati su un file system condiviso o su Amazon S3, in modo che le risorse o i dati binari non vengano memorizzati in MongoDB. In questo modo verranno garantite prestazioni ottimali all&#39;interno dell&#39;implementazione.

Uno dei vantaggi aggiuntivi della distribuzione di un set di repliche MongoDB con un cluster di due o più istanze di authoring è uno scenario di ripristino automatizzato con tempi di inattività minimi in presenza di istanze di authoring, replica MongoDB o errore completo del centro dati. Tuttavia, la scelta di MongoMK rispetto a TarMK non dovrebbe essere esclusivamente guidata dai requisiti di ripristino, in quanto TarMK può anche fornire una soluzione di downtime minima con un meccanismo di failover controllato.

Se non si prevede che i criteri di cui sopra siano soddisfatti durante i primi 18 mesi di implementazione, si consiglia prima di implementare AEM utilizzando TarMK, quindi di rivalutare la configurazione in un secondo momento, quando i criteri di cui sopra saranno applicabili, e infine di determinare se rimanere su TarMK o migrare a MongoMK.

### Eccezioni per la scelta di AEM MongoMK rispetto a TarMK nelle istanze di pubblicazione {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

Si sconsiglia di distribuire MongoMK per le istanze di pubblicazione. Il livello di pubblicazione della distribuzione viene quasi sempre distribuito come farm di istanze di pubblicazione completamente indipendenti in cui viene eseguito TarMK, che vengono mantenute sincronizzate replicando il contenuto dalle istanze di authoring. Questa architettura &quot;senza elementi condivisi&quot;, propria delle istanze di pubblicazione, consente la distribuzione del livello di pubblicazione in scala orizzontale in modo lineare. La topologia farm offre inoltre il vantaggio di applicare qualsiasi aggiornamento o aggiornamento alle istanze di pubblicazione su base continua, in modo tale che eventuali modifiche al livello di pubblicazione non richiedano tempi di inattività.

### Prerequisiti e raccomandazioni per l’implementazione di AEM con MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

È disponibile una serie di prerequisiti e raccomandazioni se stai valutando una distribuzione MongoMK per AEM:

**Prerequisiti obbligatori per le distribuzioni MongoDB:**

1. L’architettura di distribuzione e il dimensionamento di MongoDB devono far parte dell’implementazione del progetto con l’aiuto di architetti Adobe Consulting o MongoDB che hanno familiarità con AEM;
1. Le competenze di MongoDB devono essere presenti all&#39;interno del partner o del team del cliente per poter mantenere e mantenere un ambiente MongoDB esistente o nuovo;
1. Puoi scegliere di distribuire la versione commerciale o open source di MongoDB (AEM supporta entrambe le versioni), ma devi acquistare un contratto di manutenzione e supporto MongoDB direttamente da MongoDB Inc;
1. Le architetture e l&#39;infrastruttura AEM e MongoDB dovrebbero essere definite e convalidate da un architetto Adobe AEM;
1. Esamina il modello di supporto per le distribuzioni di AEM che includono MongoDB.

**Consigli efficaci per le distribuzioni MongoDB:**

* Consulta la [revisione della distribuzione di MongoDB per Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* Rivedi l&#39;[elenco di controllo delle operazioni di MongoDB](https://docs.mongodb.org/manual/administration/production-checklist/);
* Partecipa a una [classe di certificazione su MongoDB - disponibile online](https://university.mongodb.com/).

>[!NOTE]
>
>Per ulteriori domande su queste linee guida, prerequisiti e consigli, contatta l&#39;[Assistenza clienti Adobe](https://helpx.adobe.com/it/marketing-cloud/contact-support.html).
