---
title: Valutazione della complessità dell’aggiornamento con AEM Analyzer
description: Scopri come utilizzare AEM Analyzer per valutare la complessità dell’aggiornamento.
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 87c30912-c89a-42f1-b37b-ec439e7318c7
source-git-commit: 6b846e456466492f4be2c1e5a1f6b3913ae4dab4
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 15%

---

# Valutazione della complessità dell’aggiornamento con AEM Analyzer {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## Panoramica {#overview}

AEM 6.5 LTS Analyzer fornisce una valutazione dell’implementazione AEM corrente indicando le aree che devono essere aggiornate per fornire un’esperienza di aggiornamento fluida a 6.5 LTS.

Lo strumento genera un rapporto che identifica le aree di potenziale refactoring.

## Rapporto di AEM 6.5 LTS Analyzer {#aem-65lts-analyzer-report}

Il rapporto di AEM 6.5 LTS Analyzer viene utilizzato per acquisire una comprensione di alto livello della preparazione generale all’aggiornamento. Il rapporto contiene i risultati per diverse categorie di problemi che devono essere risolti per garantire un aggiornamento corretto a AEM 6.5 LTS.

Il rapporto di AEM 6.5 LTS Analyzer include le seguenti categorie:

* Funzionalità dell’applicazione che richiedono il refactoring
* Elementi dell’archivio da spostare in una posizione supportata
* Problemi di configurazione
* Funzioni di AEM 6.5 rimosse da nuove funzionalità o attualmente non supportate in AEM 6.5 LTS
* Rimuovere l’utilizzo di API Java e Guava

Informazioni aggiuntive sulle categorie e sulle possibili implicazioni e soluzioni associate a esse vengono fornite tramite i collegamenti presenti nel rapporto di AEM 6.5 LTS Analyzer.

## Disponibilità {#analyzer-availability}

AEM Analyzer può essere scaricato come file zip dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). Puoi installare il pacchetto tramite [Gestione pacchetti](/help/sites-administering/package-manager.md) nell&#39;istanza AEM di origine.

## Considerazioni importanti sull’utilizzo di AEM Analyzer {#important-considerations-for-using-aem-analyzer}

Leggi la sezione seguente per comprendere le considerazioni importanti sull’esecuzione di AEM Analyzer:

* Il rapporto di Analyzer viene creato utilizzando l’output del rilevatore pattern di AEM. La versione del rilevatore pattern utilizzata da Analyzer è inclusa nel pacchetto di installazione di AEM Analyzer
* AEM Analyzer può essere eseguito solo dall&#39;utente **admin** o da un utente del gruppo **amministratori**
* Analyzer è supportato sulle istanze di AEM con versione 6.5 e successive.

>[!NOTE]
>
>Per evitare un impatto sulle istanze aziendali critiche, si consiglia di eseguire AEM Analyzer in un ambiente di staging il più simile possibile all’ambiente di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito su un clone dell’ambiente di authoring di produzione.

* La generazione dei contenuti dei rapporti di AEM Analyzer può richiedere molto tempo, da alcuni minuti ad alcune ore. Il tempo necessario dipende in larga misura dalle dimensioni e dalla natura del contenuto dell’archivio AEM, dalla versione di AEM e da altri fattori
* A causa del tempo significativo che potrebbe essere necessario per generare il contenuto del rapporto, questo viene generato da un processo in background e mantenuto in una cache. La visualizzazione e il download del rapporto dovrebbero essere relativamente veloci poiché viene utilizzata la cache del contenuto fino alla scadenza o all’aggiornamento esplicito del rapporto. Durante la generazione del contenuto del rapporto puoi chiudere la scheda del browser e tornare in un secondo momento per visualizzare il rapporto una volta che il relativo contenuto è disponibile nella cache.

## Visualizzazione del rapporto di AEM Analyzer {#viewing-the-aem-analyzer-report}

Per visualizzare il rapporto di AEM Analyzer, segui i passaggi seguenti:

1. Seleziona Adobe Experience Manager e passa a **Strumenti - Operazioni - 6.5 LTS Modernizer**

   ![Visualizza report analisi 1](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. Fai clic su **AEM 6.5 LTS Analyzer** per aprirlo

   ![Visualizza report analisi 2](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. Fai clic su **Genera report** per eseguire AEM Analyzer

   ![Visualizza report analisi 3](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. Durante la generazione del rapporto da parte di AEM Analyzer, è possibile visualizzare lo stato di avanzamento dello strumento sullo schermo. Visualizza lo stato di avanzamento in termini di percentuale di completamento. Vengono inoltre visualizzati il numero di elementi analizzati e il numero di risultati

   ![Visualizza report analisi 4](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. Una volta generato il rapporto di 6.5 LTS Analyzer, viene visualizzato un riepilogo e il numero dei risultati in un formato tabulare organizzato in base al tipo di risultato e al livello di importanza. Per ottenere ulteriori dettagli su un particolare risultato, è possibile fare clic sul numero corrispondente al tipo di risultato nella tabella

   ![Visualizza report analisi 5](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. È possibile scaricare il report in formato CSV facendo clic su **Esporta in CSV**. È possibile forzare l&#39;analizzatore a cancellare la cache e rigenerare il report facendo clic su **Aggiorna report**. Se la cache scade, devi rigenerare il rapporto.

## Interpretazione del rapporto di AEM Analyzer {#interpreting-the-aem-analyzer-report}

Quando lo strumento 6.5 LTS Analyzer viene eseguito nell&#39;istanza di AEM, il rapporto viene visualizzato come risultati nella finestra dello strumento.

Il rapporto si presenta con questo formato:

* **Panoramica rapporto**: informazioni sul rapporto stesso, tra cui:

   * **Ora del report**: quando il contenuto del report è stato generato e reso disponibile per la prima volta
   * **Data di scadenza**: quando scade la cache del contenuto del report
   * **Periodo di tempo di generazione**: la quantità di tempo in cui è stato generato il report
   * **Conteggio risultati**: numero totale di risultati inclusi nel report

* **Panoramica del sistema**: informazioni sul sistema AEM su cui è stato eseguito Analyzer
* **Categorie dei risultati**: diverse sezioni che riguardano ciascuna uno o più risultati della stessa categoria. Ogni sezione include quanto segue: nome della categoria, sottotipi, conteggio e importanza dei risultati, riepilogo, collegamento alla documentazione della categoria e informazioni su singoli risultati.

  ![Riepilogo report analisi](/help/sites-deploying/assets/analyzer-report-summary.png)

  A ciascun risultato viene assegnato un livello di importanza per dare un’indicazione approssimativa del grado di priorità dell’intervento richiesto.

>[!NOTE]
>
>Per ulteriori informazioni su ciascuna categoria di risultati, vedere [Categorie del rilevatore pattern](https://experienceleague.adobe.com/it/docs/experience-manager-pattern-detection/table-of-contents/aso).

Per comprendere i livelli di importanza, seguire la tabella seguente:

| Importanza | Descrizione |
|---|---|
| INFO | Questo risultato è fornito a scopo informativo. |
| ADVISORY (AVVISO) | Questo risultato potrebbe costituire un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| CRITICAL (CRITICO) | È molto probabile che questo risultato costituisca un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |

## Interpretazione del rapporto CSV di AEM 6.5 LTS Analyzer {#interpreting-the-aem-65lts-analyzer-report}

Quando fai clic sull&#39;opzione **CSV** nell&#39;istanza di AEM, il rapporto Analyzer in formato CSV viene creato dalla cache del contenuto e restituito al browser. A seconda delle impostazioni del browser, il report viene scaricato automaticamente come file con il nome predefinito `report.csv`.

Se la cache è scaduta, il rapporto viene rigenerato prima che il file CSV venga generato e scaricato.

Il formato CSV del rapporto include informazioni generate dall’output del rilevatore pattern, ordinate e organizzate per tipo di categoria, sottotipo e livello di importanza. Il formato è adatto alla visualizzazione e la modifica in un’applicazione come Microsoft Excel. Ha lo scopo di fornire tutte le informazioni sui risultati in un formato ripetibile che può essere utile quando si confrontano i rapporti nel tempo per misurare l’avanzamento.

Le colonne del rapporto in formato CSV sono:

* **code** (codice): codice della categoria
* **type** (tipo): nome della categoria
* **subtype** (sottotipo): sottotipo della categoria
* **importance** (importanza): livello di importanza
* **identifier** (identificatore): identificatore principale del risultato
* **message** (messaggio): messaggio fornito per il risultato
* **context** (contesto): una stringa JSON contenente dati sul risultato

Un valore di &quot;`\N`&quot; in una colonna per un singolo risultato indica che non sono stati forniti dati.

## Interfaccia HTTP {#http-interface}

6.5 LTS Analyzer fornisce un’interfaccia HTTP che può essere utilizzata come alternativa all’interfaccia utente in AEM. L&#39;interfaccia supporta sia i comandi `HEAD` che `GET`. Può essere utilizzato per generare il rapporto di Analyzer e restituirlo in uno dei tre formati seguenti: JSON, CSV e valori delimitati da tabulazioni (TSV).

I seguenti URL sono disponibili per l&#39;accesso HTTP, dove `<host>` è il nome host, insieme alla porta se necessario, del server in cui è installato Analyzer:

* `http://<host>/apps/aem66-analyzer/analysis/report.json` per il formato JSON
* `http://<host>/apps/aem66-analyzer/analysis/report.csv` per il formato CSV
* `http://<host>/apps/aem66-analyzer/analysis/report.tsv` per il formato TSV

### Esecuzione di una richiesta HTTP {#executing-an-http-request}

Un modo semplice per eseguire una richiesta HTTP consiste nell’aprire una scheda nello stesso browser in cui hai già effettuato l’accesso ad AEM come amministratore. Puoi inserire l’URL nella scheda del browser e visualizzare o scaricare i risultati dal browser.

È inoltre possibile utilizzare uno strumento della riga di comando come `curl` o `wget` e qualsiasi applicazione client HTTP. Se non utilizzi una scheda del browser con una sessione autenticata, devi fornire nel commento un nome utente e una password amministratore.

Di seguito è riportato un esempio di come eseguire questa operazione:

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## Regolazione della durata della cache {#adjusting-the-cache-lifetime}

La durata predefinita della cache di AEM 6.5 LTS Analyzer è di 24 ore. Con l’opzione per aggiornare un rapporto e rigenerare la cache, sia nell’istanza di AEM che nell’interfaccia HTTP, questo valore predefinito è probabilmente appropriato per la maggior parte degli utilizzi di AEM 6.5 LTS Analyzer. Se il tempo di generazione del rapporto è particolarmente lungo per l’istanza di AEM, è possibile regolare la durata della cache per ridurre al minimo la rigenerazione del rapporto.

Il valore della durata della cache viene archiviato come proprietà `maxCacheAge` nel seguente nodo dell&#39;archivio:

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

Il valore di questa proprietà corrisponde alla durata della cache, in secondi. Un amministratore può regolare la durata della cache utilizzando CRX/DE Lite.

## Utilizzo di Content Transformer {#using-content-transformer}

### Disponibilità {#content-transformer-availability}

Il Content Transformer è fornito in bundle con AEM 6.5 LTS Analyzer che può essere scaricato come file zip dal portale di distribuzione software.

### Considerazioni importanti sull’utilizzo di Content Transformer {#important-considerations-for-using-content-transformer}

Consulta la sezione seguente per comprendere le considerazioni importanti sull’utilizzo del Content Transformer (CT):

* Per utilizzare Content Transformer, devi prima eseguire AEM Analyzer nel tuo ambiente AEM
* Anche se è possibile eseguire Content Transformer nell’ambiente di produzione, si consiglia di eseguirlo su un clone dell’ambiente di produzione. È importante assicurarsi che AEM Analyzer e CT vengano eseguiti nello stesso ambiente
* Devi essere un amministratore dell’ambiente in cui desideri eseguire Content Transformer
* Un&#39;operazione di rimozione che può modificare il contenuto di origine creerà un pacchetto di backup dei percorsi di origine in `/etc/packages/modernizer-content-transformation` per impostazione predefinita prima della trasformazione. Anche se la finestra di dialogo per la rimozione dell’operazione dispone di un’opzione per disabilitare/abilitare la creazione del pacchetto di backup, si consiglia vivamente di selezionare sempre l’opzione per abilitare la creazione del pacchetto
* Ogni pagina di Content Transformer è configurata per elencare un massimo di 50 risultati. Pertanto, è possibile trasformare un massimo di 50 risultati alla volta. Questa operazione viene eseguita per fornire una risposta tempestiva nell’interfaccia utente.

### Apertura di Content Transformer {#opening-the-content-transformer}

1. Accedi all&#39;istanza AEM di origine come amministratore e passa alla pagina iniziale all&#39;indirizzo *https://host:port/aem/start.htm*
1. Passa a **Strumenti - Operazioni - 6.5 LTS Modernizer**

   ![Apertura di Content Transformer 1](/help/sites-deploying/assets/opening-content-transformer-1.png)

1. Fai clic sulla scheda del report **Content Transformer for 6.5 LTS Analyzer**

   ![Apertura di Content Transformer 2](/help/sites-deploying/assets/opening-content-transformer-2.png)

1. Se il report di Analyzer non viene generato, nella pagina **Trasforma contenuto** verrà visualizzato **Nessun report**. Se tutti i risultati relativi al contenuto sono stati rimossi, verrà visualizzato lo stesso messaggio **Nessun report**

   ![Apertura di Content Transformer 3](/help/sites-deploying/assets/opening-content-transformer-3.png)

1. Di seguito è riportato un esempio di come si presenterà la pagina Panoramica di Content Transformer se la creazione del rapporto di AEM Analyzer ha avuto esito positivo e se sono stati riscontrati problemi relativi al contenuto.

Il tempo di scadenza rimasto per il rapporto di AEM Analyzer viene visualizzato sulla barra laterale. Si consiglia di eseguire Content Transformer con il report di AEM Analyzer più recente, per evitare di perdere risultati relativi al contenuto

![Apertura di Content Transformer 4](/help/sites-deploying/assets/opening-content-transformer-4.png)

1. Puoi filtrare i problemi in base a Codice pattern, Sottotipo, Importanza e Source

   ![Apertura di Content Transformer 5](/help/sites-deploying/assets/opening-content-transformer-5.png)

### Rimozione dei percorsi {#removing-paths}

1. Puoi selezionare tutti i problemi o solo quelli specifici e selezionare **Rimuovi** per risolverli

   ![Rimozione percorsi 1](/help/sites-deploying/assets/removing-paths-1.png)

   >[!NOTE]
   >Per impostazione predefinita, un&#39;operazione Remove crea un pacchetto di backup dei percorsi di origine in `/etc/packages/modernizer-content-transformation` prima della trasformazione. Anche se la finestra di dialogo per la rimozione dell’operazione dispone di un’opzione per disabilitare/abilitare la creazione del pacchetto di backup, si consiglia vivamente di selezionare sempre l’opzione per abilitare la creazione del pacchetto.

   ![Rimozione percorsi 2](/help/sites-deploying/assets/removing-paths-2.png)

1. Di seguito è riportato un esempio di pacchetto di backup creato per l’operazione di rimozione dei percorsi. Puoi fare clic su **Installa** per ripristinare i percorsi di origine

   ![Rimozione percorsi 3](/help/sites-deploying/assets/removing-paths-3.png)

   >[!CAUTION]
   >
   >Non eliminare `/etc/packages/modernizer-content-transformation`, poiché è il percorso in cui risiedono i pacchetti di backup. Puoi eliminare questo percorso per ridurre le dimensioni dell’archivio solo quando sei sicuro di non aver più bisogno di questi pacchetti.

1. In alternativa, è possibile creare un pacchetto dei risultati di contenuto selezionati per utilizzi futuri. A questo scopo, seleziona i risultati da includere, quindi fai clic su **Pacchetto** in alto a sinistra. Immettere il nome di un pacchetto, scegliere il percorso del pacchetto e fare clic sul pulsante **Pacchetto** per completare il processo.

   ![Rimozione percorsi 3](/help/sites-deploying/assets/removing-paths-4.png)

### Problemi noti {#known-issues}

* A volte, l&#39;operazione di rimozione potrebbe visualizzare la notifica: *&quot;Alcuni percorsi non sono stati rimossi correttamente. Controllare i registri e riprovare.*&quot;. Tuttavia, se i percorsi sono stati effettivamente rimossi, puoi tranquillamente ignorare questo messaggio
* Analogamente, l&#39;operazione del pacchetto potrebbe non riuscire con l&#39;errore: *&quot;Errore durante l&#39;esecuzione dell&#39;operazione desiderata. Controllare i registri e riprovare.*&quot;. Ciò è probabilmente dovuto alla scadenza della sessione. In questi casi, ritentare l’operazione per risolvere il problema.
