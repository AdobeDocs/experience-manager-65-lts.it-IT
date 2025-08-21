---
title: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5 LTS
description: Informazioni sulla versione corrente di Adobe Experience Manager 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 70436606-d95c-4208-94f6-e33f3eefdf66
source-git-commit: 160b27c188f8bcd3f3a668b50d3a824598909688
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 95%

---

# Note sulla versione corrente di Adobe Experience Manager 6.5 LTS {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] |
|---|---|
| Versione | 6.5 LTS |
| Tipo | Versione principale |
| Data di disponibilità generale | 7 marzo 2025 |

## Novità {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS è una versione di aggiornamento della base di codice di [!DNL Adobe Experience Manager] 6.5. Fornisce importanti correzioni di casi segnalati dai clienti, miglioramenti ad alta priorità e correzioni generali di bug orientate al consolidamento del prodotto. Include anche [!DNL Adobe Experience Manager] versioni di Service Pack 6.5 fino a SP22.

L’elenco seguente fornisce una panoramica, mentre le pagine successive elencano tutti i dettagli.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 LTS si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e dell’archivio dei contenuti Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x è utilizzato come motore servlet per Quickstart.

#### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituisci i valori predefiniti del GC (catalogo globale) con altri valori. Per ulteriori informazioni, consulta la sezione [Installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuisce gli aggiornamenti di manutenzione Java™ 17 e Java™ 21 per l’utilizzo da parte del cliente nei progetti correlati ad AEM, se non disponibili pubblicamente da Oracle.

#### Pacchetto Uberjar {#uber-jar-packaging}

* Il pacchetto Uberjar di AEM 6.5 LTS presenta una leggera differenza. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

#### Aggiornamento {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).

## Installare e aggiornare {#install-update}

Per i requisiti di configurazione, consulta [Istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

Per istruzioni dettagliate, consulta la [documentazione relativa all’aggiornamento](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Per le nuove installazioni di AEM 6.5 LTS, le definizioni degli indici devono essere installate separatamente. Per ulteriori informazioni, vedere [questo articolo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, sui [requisiti tecnici AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Si consiglia di utilizzare le versioni Java™ 17/Java™ 21 con AEM 6.5 LTS.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe rivede continuamente le funzionalità del prodotto per migliorare il valore del cliente modernizzando o sostituendo le funzioni meno recenti. Queste modifiche vengono apportate prestando particolare attenzione alla compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità di Adobe Experience Manager (AEM), si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una specifica funzione diventerà obsoleta. Anche se obsolete, le funzionalità sono ancora disponibili ma non vengono migliorate ulteriormente.
1. La rimozione delle funzionalità obsolete avviene non prima della versione principale successiva. La data effettiva di destinazione per la rimozione è pianificata per essere annunciata in un secondo momento.

Questo processo offre alla clientela almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

### Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità che Adobe ha dichiarato obsolete in AEM 6.5 LTS. In genere, Adobe depreca le funzioni prima di rimuoverle in una versione futura e fornisce un’alternativa.


Consigliamo alla clientela di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|---|---|---|---|
| Sites | [Editor SPA](/help/sites-developing/spa-overview.md) | Gli editor preferiti per la gestione dei contenuti headless in AEM sono:<br>- [l’editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.<br>- [Editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo. | 6.5 LTS GA |

### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità e le funzioni che sono state rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic non è supportato. | Esegui la migrazione a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluzioni | Social/Communities non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Screens | Gli Screens non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Risorse | `dam-pim` e `dam-rating` non sono supportati perché i bundle dipendono dal social. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Risorse | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` è stato rimosso. | Utilizza l’API alternativa `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` che è stata aggiunta. | 6.5 LTS GA |
| Portale | AEM Portal Director non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | Il bundle `com.adobe.granite.socketio` è stato rimosso. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | `crx2oak` non è supportato. | Scegli la versione rilevante di [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Guava | Tutte le dipendenze guava ora vengono rimosse in AEM e pertanto il bundle `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` non fa parte di AEM. | Se possibile, la clientela può aggiungere guava autonomamente se dipende da guava o sostituire il codice guava con raccolte java o altre alternative. | 6.5 LTS GA |
| `We.Retail` | `We-retail` sito di esempio non supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | Il bundle `oak-solr-osgi` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` e `org.apache.sling.atom.taglib` non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | I pacchetti `org.apache.commons.io` ora vengono esportati da `org.apache.commons.commons-io`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | Esportazione dei pacchetti `javax.mail` dal bundle `com.sun.javax.mail`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | I pacchetti `org.apache.jackrabbit.api` ora vengono esportati dal bundle `org.apache.jackrabbit.oak-jackrabbit-api`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | `com.github.jknack.handlebars` non è supportato | Scegli la [versione](https://mvnrepository.com/artifact/com.github.jknack/handlebars) pertinente | 6.5 LTS GA |

## Problemi noti {#known-issues}

### Problema con il bundle dello script JSP in AEM 6.5.21-6.5.23 e AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23 e AEM 6.5 LTS GA vengono forniti con il bundle `org.apache.sling.scripting.jsp:2.6.0`, che contiene un problema noto. Il problema si verifica in genere con un carico elevato quando l’istanza AEM gestisce molte richieste simultanee.

Quando si verifica questo problema, è possibile che nei registri errori venga visualizzata una delle eccezioni seguenti insieme ai riferimenti a `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip).

### Errore di connessione di Dispatcher con la funzione solo SSL {#ssl-only-feature}

Quando si abilita la funzione solo SSL nelle implementazioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze Dispatcher e AEM. Dopo aver abilitato questa funzione, le verifiche stato potrebbero non riuscire e la comunicazione tra le istanze Dispatcher e AEM potrebbe essere interrotta. Questo problema si verifica in modo specifico quando i clienti tentano di connettersi tramite `https + IP` dalle istanze Dispatcher ad AEM. È correlato a problemi di convalida SNI (Server Name Indication).

**Impatto:**

* Errori di verifica stato con codici di risposta HTTP 400
* Traffico interrotto tra istanze Dispatcher e AEM
* Il contenuto non può essere gestito correttamente tramite Dispatcher
* Errori di connessione durante l’utilizzo di HTTPS con indirizzi IP nella configurazione di Dispatcher
* HTTP 400: errori “SNI non valida” durante la connessione tramite HTTPS + IP

**Ambienti interessati:**

* Implementazioni di AEM con configurazioni Dispatcher
* Sistemi in cui è stata abilitata la funzione solo SSL
* Configurazioni di Dispatcher che utilizzano il metodo di connessione `https + IP` alle istanze AEM

**Soluzione:**
se riscontri questo problema, contatta l’Assistenza Clienti di Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip). Non tentare di abilitare le funzioni solo SSL finché non viene applicato l’hotfix necessario.

## Siti web con restrizioni{#restricted-sites}

Questi siti web sono disponibili solo per la clientela. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/it/docs/customer-one/using/home).