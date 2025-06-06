---
title: Modalità di esecuzione
description: Scopri come regolare l’istanza di AEM per scopi specifici utilizzando le modalità di esecuzione.
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b21555f2-bc07-4653-a5da-966b9aa7ea1f
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---

# Modalità di esecuzione{#run-modes}

Le modalità di esecuzione consentono di regolare l’istanza di AEM per uno scopo specifico, ad esempio authoring o pubblicazione, test, sviluppo, Intranet o altri.

Operazioni disponibili:

* [Definire insiemi di parametri di configurazione per ogni modalità di esecuzione](#defining-configuration-properties-for-a-run-mode).

  Un set di base di parametri di configurazione viene applicato a tutte le modalità di esecuzione e puoi quindi regolare altri set in base allo scopo dell’ambiente specifico. Questi vengono applicati in base alle esigenze.

* [Definire i bundle aggiuntivi da installare per una modalità particolare](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Tutte le impostazioni e le definizioni vengono archiviate in un unico repository e attivate impostando la **Modalità di esecuzione**.

## Modalità di esecuzione dell’installazione {#installation-run-modes}

Le modalità di esecuzione dell’installazione (o fisse) vengono utilizzate al momento dell’installazione e quindi corrette per l’intera durata dell’istanza, e non possono essere modificate.

Sono disponibili modalità di esecuzione dell’installazione pronte all’uso:

* `author`
* `publish`

Si tratta di due coppie di modalità di esecuzione che si escludono a vicenda; ad esempio, è possibile:

* definisci `author` o `publish`, non entrambi allo stesso tempo

>[!CAUTION]
>
>Quando si utilizza una delle modalità di esecuzione precedenti (authoring, pubblicazione), il valore utilizzato al momento dell&#39;installazione definisce la modalità di esecuzione per l&#39;*intera durata* dell&#39;installazione.
>
>Per queste modalità di esecuzione *non è possibile* modificarle dopo l&#39;installazione.

## Modalità di esecuzione personalizzate {#customized-run-modes}

Puoi anche creare modalità di esecuzione personalizzate. Queste possono essere combinate per coprire scenari quali:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* come richiesto . . .

Ad ogni avvio è possibile selezionare anche modalità di esecuzione personalizzate.

## Definizione delle proprietà di configurazione per una modalità di esecuzione {#defining-configuration-properties-for-a-run-mode}

Un insieme di valori per le proprietà di configurazione, utilizzati per una particolare modalità di esecuzione, può essere salvato nel repository.

La modalità di esecuzione è indicata da un suffisso nel nome della cartella. Questo consente di memorizzare tutte le configurazioni in un archivio come. Ad esempio:

* `config`

  Applicabile a tutte le modalità di esecuzione

* `config.author`

  Utilizzato per la modalità di esecuzione dell’autore

* `config.publish`

  Utilizzato per la modalità di esecuzione pubblicazione

* `config.<run-mode>`

  Utilizzato per la modalità di esecuzione applicabile; ad esempio, config

Per ulteriori informazioni sulla definizione dei singoli nodi di configurazione all&#39;interno di queste cartelle e sulla creazione di configurazioni per combinazioni di più modalità di esecuzione, vedere [Configurazione OSGi nel repository](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

>[!NOTE]
>
>Per le [modalità di esecuzione dell&#39;installazione](#installation-run-modes) (ad esempio, creazione) non è possibile modificare la modalità di esecuzione dopo l&#39;installazione. Tuttavia, le modifiche alle singole proprietà di configurazione avranno effetto al riavvio.

## Definizione di bundle aggiuntivi da installare per una modalità di esecuzione {#defining-additional-bundles-to-be-installed-for-a-run-mode}

È inoltre possibile specificare bundle aggiuntivi da installare per una particolare modalità di esecuzione. Per queste definizioni, le cartelle di installazione vengono utilizzate per contenere i bundle. Anche in questo caso la modalità di esecuzione è indicata da un prefisso:

* `install.author`
* `install.publish`

Queste cartelle sono di tipo `nt:folder` e devono contenere il bundle appropriato.

## Avvio di CQ con una modalità di esecuzione specifica {#starting-cq-with-a-specific-run-mode}

Se sono state definite configurazioni per più modalità di esecuzione, è necessario definire quale deve essere utilizzata all&#39;avvio. Esistono diversi metodi per specificare quale modalità di esecuzione utilizzare; l’ordine di risoluzione è:

1. [proprietà di sistema (](#using-a-system-property-in-the-start-script)
1. [&#128279;](#using-the-sling-properties-file)
1. [&#128279;](#using-the-r-option)
1. [Rilevamento del nome file](#filename-detection-renaming-the-jar-file)

Quando si utilizza un server applicazioni è inoltre possibile [definire la modalità di esecuzione in web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Utilizzo del file sling.properties {#using-the-sling-properties-file}

Il file `sling.properties` può essere utilizzato per definire la modalità di esecuzione richiesta:

1. Modifica il file di configurazione:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Aggiungi le seguenti proprietà; l’esempio seguente è per autore:

   `sling.run.modes=author`

### Utilizzo dell&#39;opzione -r {#using-the-r-option}

È possibile attivare una modalità di esecuzione personalizzata utilizzando l&#39;opzione `-r` all&#39;avvio dell&#39;avvio rapido. Ad esempio, utilizza il seguente comando per avviare un’istanza di AEM con la modalità di esecuzione impostata su dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Utilizzo di una proprietà di sistema nello script iniziale {#using-a-system-property-in-the-start-script}

È possibile utilizzare una proprietà di sistema nello script di avvio per specificare la modalità di esecuzione.

* Ad esempio, utilizza quanto segue per avviare un’istanza come istanza di pubblicazione di produzione negli Stati Uniti:

  `-Dsling.run.modes=publish,prod,us`

### Rilevamento del nome file - Ridenominazione del file jar {#filename-detection-renaming-the-jar-file}

Le due modalità di esecuzione dell’installazione seguenti possono essere attivate rinominando il file jar dell’installazione prima dell’installazione:

* pubblicazione
* author

Il file jar deve utilizzare la convenzione di denominazione:

`cq5-<run-mode>-p<port-number>`

Ad esempio, impostare la modalità di esecuzione `publish` denominando il file jar:

`cq5-publish-p4503`

### Definizione della modalità di esecuzione in web.xml (con Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

Quando utilizzi un server applicazioni puoi anche configurare la proprietà:

`sling.run.modes`

nel file:

`WEB-INF/web.xml`

Si trova nel file AEM `war` e deve essere aggiornato prima della distribuzione.

Per ulteriori dettagli, vedere [Installazione di AEM con un server applicazioni](/help/sites-deploying/application-server-install.md).
