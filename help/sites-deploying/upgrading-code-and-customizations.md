---
title: Aggiornamento del codice e delle personalizzazioni
description: Ulteriori informazioni sull’aggiornamento del codice e sulle personalizzazioni in AEM.
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 6b94caf1-97b7-4430-92f1-4f4d0415aef3
source-git-commit: c1935b95d4e9e8e3773f2ff9825c759f97738304
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---

# Aggiornamento del codice e delle personalizzazioni{#upgrading-code-and-customizations}

Durante la pianificazione di un aggiornamento, è necessario esaminare e risolvere le seguenti aree di un’implementazione.

* [Aggiorna base codice](#upgrade-code-base)
* [Procedura di prova](#testing-procedure)

## Panoramica {#overview}

1. **AEM Analyzer** - Eseguire AEM Analyzer come descritto nella pianificazione dell&#39;aggiornamento e descritto in dettaglio nella pagina [Valutazione della complessità dell&#39;aggiornamento con AEM Analyzer](/help/sites-deploying/aem-analyzer.md). Ricevi un rapporto di AEM Analyzer che contiene ulteriori dettagli sulle aree che devono essere affrontate, oltre alle API/bundle non disponibili nella versione Target di AEM. Il rapporto di AEM Analyzer fornisce un’indicazione di eventuali incompatibilità nel codice. Se non ne esiste alcuna, la distribuzione è già compatibile con 6,5 LTS. È comunque possibile scegliere di eseguire un nuovo sviluppo per l&#39;utilizzo della funzionalità 6.5 LTS, ma non è necessario solo per mantenere la compatibilità.
1. **Sviluppo base codice per 6.5 LTS**- Creazione di un ramo o repository dedicato per la base codice per la versione di destinazione. Utilizza le informazioni di Compatibilità pre-aggiornamento per pianificare le aree di codice da aggiornare.
1. **Compilare con 6.5 LTS Uber jar**- Aggiornare i POM della base di codice in modo che puntino a 6.5 LTS Uber jar e compilare il codice in base a esso.
1. **Implementa nell&#39;ambiente LTS 6.5** - Un&#39;istanza pulita di AEM 6.5 LTS (Author + Publish) deve trovarsi in un ambiente di sviluppo/controllo qualità. È necessario distribuire una base di codice aggiornata e un campione rappresentativo di contenuti (dalla produzione corrente).
1. **Convalida QA e correzione bug** - Il controllo qualità deve convalidare l&#39;applicazione sia nelle istanze Author che Publish di 6.5 LTS. Eventuali bug rilevati devono essere corretti e inseriti nella base di codice 6.5 LTS. Ripeti Dev-Cycle secondo necessità fino a quando tutti i bug non vengono risolti.

Prima di procedere con un aggiornamento, è necessario disporre di una base di codice dell&#39;applicazione stabile che sia stata testata accuratamente rispetto a AEM 6.5 LTS.

## Aggiorna base codice {#upgrade-code-base}

### Creazione di un ramo dedicato per il codice LTS 6.5 nel controllo della versione {#create-a-dedicated-branch-for-6.5-lts-code-in-version-control}

Tutto il codice e le configurazioni necessari per l’implementazione di AEM devono essere gestiti utilizzando una qualche forma di controllo della versione. È necessario creare un ramo dedicato nel controllo della versione per gestire tutte le modifiche necessarie per la base di codice nella versione di destinazione di AEM. In questo ramo vengono gestiti i test iterativi della base di codice rispetto alla versione di destinazione di AEM e le successive correzioni di bug.

### Aggiornare la versione di AEM Uber Jar {#update-the-aem-uber-jar-version}

Il file jar di AEM Uber include tutte le API di AEM come una singola dipendenza in `pom.xml` del progetto Maven. È sempre consigliabile includere il file JAR Uber come una singola dipendenza invece di includere singole dipendenze API di AEM. Durante l’aggiornamento della base di codice, modifica la versione del Jar Uber in modo che punti alla versione 6.5 LTS di AEM. Aggiorna eventuali API o metodi obsoleti in modo che siano compatibili con la versione di destinazione di AEM. Ricompila la base di codice rispetto alla nuova versione del file JAR Uber.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>C’è una leggera differenza nel modo in cui i file JAR Uber di AEM 6.5 e AEM 6.5 LTS sono confezionati. Consulta la sezione seguente:

**JAR Uber per AEM 6.5**

1. `uber-jar-6.5.x.jar` - Contiene tutte le API pubbliche di AEM 6.5.
1. `uber-jar-6.5.x-apis-with-deprecations.jar` - Include sia API pubbliche che API obsolete da AEM 6.5.

**JAR Uber per AEM 6.5 LTS**

Per AEM 6.5 LTS, esistono ancora due tipi di file JAR Uber:

1. `uber-jar-6.6.x-apis.jar` - Contiene tutte le API pubbliche di AEM 6.5 LTS.
1. `uber-jar-6.6.x-deprecated-apis.jar` - Include solo API obsolete da AEM 6.5 LTS.

**Differenza chiave: AEM 6.5 rispetto ad AEM 6.5 LTS Uber Jars**

* In AEM 6.5, se sono necessarie entrambe le API pubbliche e obsolete, puoi utilizzare include single jar, `uber-jar-6.5.x-apis-with-deprecations.jar` nel file `pom.xml`.
* In AEM 6.5 LTS, se hai bisogno sia di API pubbliche che di API obsolete, devi includere due file jar separati, `uber-jar-6.6.x-apis.jar` per le API pubbliche e `uber-jar-6.6.x-deprecated-apis.jar` per le API obsolete.

**Coordinate Maven per Jar API obsolete**

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Note per sviluppatori {#developer-notes}

* AEM 6.5 LTS non include la libreria guava di Google preconfigurata; è possibile installare la versione richiesta in base alle esigenze.
* Il bundle Sling XSS ora utilizza la libreria Java HTML Sanitizer e l&#39;utilizzo del metodo `XSSAPI#filterHTML()` deve essere utilizzato per il rendering del contenuto HTML in modo sicuro e non per la trasmissione di dati ad altre API.
* Aggiornamento alla configurazione del filtro SSL HTTP Apache Felix: in AEM 6.5 LTS, il bundle `org.apache.felix.http.sslfilter` è stato aggiornato dalla versione 1.2.6 alla versione 2.0.2. Durante questo aggiornamento, il PID di configurazione OSGi `org.apache.felix.http.sslfilter.SslFilter` è stato dichiarato obsoleto e sostituito con un nuovo PID: `org.apache.felix.http.sslfilter.Configuration`. Se nella distribuzione viene utilizzato il filtro SSL, le configurazioni esistenti devono essere migrate manualmente al nuovo PID utilizzando Gestione configurazione OSGi (`/system/console/configMgr`). La mancata migrazione della configurazione potrebbe impedire l’applicazione del filtro SSL prevista dopo l’aggiornamento.

## Procedura di prova {#testing-procedure}

Per testare gli aggiornamenti è necessario preparare un piano di test completo. Il test della base di codice e dell’applicazione aggiornate deve essere eseguito prima in ambienti inferiori. Eventuali bug trovati devono essere corretti in modo iterativo fino a quando la base di codice non è stabile, solo in questo caso gli ambienti di livello superiore dovrebbero essere aggiornati.

### Verifica della procedura di aggiornamento {#testing-upgrade-procedure}

La procedura di aggiornamento qui descritta deve essere testata in ambienti di sviluppo e controllo qualità come documentato nel manuale di esecuzione personalizzato (vedi [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md)). La procedura di aggiornamento deve essere ripetuta fino a quando tutti i passaggi non sono documentati nel registro di esecuzione dell&#39;aggiornamento e il processo di aggiornamento non è graduale.

### Aree di prova dell’implementazione  {#implementation-test-areas-}

Di seguito sono riportate le aree critiche di qualsiasi implementazione di AEM che devono essere coperte dal piano di test dopo l’aggiornamento dell’ambiente e la distribuzione della base di codice aggiornata.

<table>
 <tbody>
  <tr>
   <td><strong>Area di prova funzionale</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Siti pubblicati</td>
   <td>Verifica dell'implementazione di AEM e del codice associato sul livello di pubblicazione<br /> tramite Dispatcher. Deve includere i criteri per gli aggiornamenti delle pagine e <br /> l'annullamento della validità della cache.</td>
  </tr>
  <tr>
   <td>Authoring</td>
   <td>Verifica dell’implementazione di AEM e del codice associato sul livello di authoring. Deve includere la creazione di pagine, componenti e finestre di dialogo.</td>
  </tr>
  <tr>
   <td>Integrazioni con le soluzioni Experience Cloud</td>
   <td>Convalida delle integrazioni con prodotti come Analytics.</td>
  </tr>
  <tr>
   <td>Integrazioni con sistemi di terze parti</td>
   <td>Convalida qualsiasi integrazione di terze parti sia sul livello Author che Publish.</td>
  </tr>
  <tr>
   <td>Autenticazione, sicurezza e autorizzazioni</td>
   <td>Qualsiasi meccanismo di autenticazione come LDAP/SAML deve essere convalidato.<br /> Le autorizzazioni e i gruppi devono essere testati sui livelli Author e Publish<br />.</td>
  </tr>
  <tr>
   <td>Query</td>
   <td>Gli indici e le query personalizzati devono essere testati insieme alle prestazioni delle query.</td>
  </tr>
  <tr>
   <td>Personalizzazioni interfaccia utente</td>
   <td>Eventuali estensioni o personalizzazioni dell’interfaccia utente di AEM nell’ambiente di authoring.</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td>Flussi di lavoro e funzionalità personalizzati e/o predefiniti.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td>Il test di carico deve essere eseguito sui livelli Author e Publish che simulano scenari reali.</td>
  </tr>
 </tbody>
</table>

### Documenta piano di test e risultati {#document-test-plan-and-results}

È necessario creare un piano di test che copra le aree di test di implementazione di cui sopra. Spesso è utile separare il piano di test dagli elenchi delle attività Autore e Pubblica. Questo piano di test deve essere eseguito sugli ambienti di sviluppo, controllo qualità e staging prima dell’aggiornamento degli ambienti di produzione. I risultati dei test e le metriche delle prestazioni devono essere acquisiti in ambienti inferiori per fornire confronti durante l’aggiornamento degli ambienti di staging e produzione.
