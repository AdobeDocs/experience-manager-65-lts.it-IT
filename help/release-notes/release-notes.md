---
title: Note sulla versione corrente per Adobe Experience Manager 6.5 LTS
description: Trova informazioni sulla versione corrente di Adobe Experience Manager 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 2c2e8defbaab13a31beeb7c6978af5da19535e70
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 18%

---

# Note sulla versione corrente per Adobe Experience Manager 6.5 LTS {#release-notes}

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] |
|---|---|
| Versione | 6,5 LTS |
| Tipo | Versione principale |
| Data di disponibilità generale | sabato 7 marzo 2025 |

## Novità {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS è una versione di aggiornamento della base di codice di [!DNL Adobe Experience Manager] 6.5. Fornisce correzioni di problemi fondamentali per i clienti, miglioramenti con priorità elevata per i clienti e correzioni di bug generali per la stabilizzazione del prodotto. Include anche [!DNL Adobe Experience Manager] versioni di Service Pack 6.5 fino a SP22.

L’elenco seguente fornisce una panoramica, mentre le pagine successive elencano tutti i dettagli.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La piattaforma di [!DNL Adobe Experience Manager] 6.5 LTS si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del Content Repository Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x è usato come motore servlet per Quickstart.

#### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituire i valori predefiniti del catalogo globale con altri valori. Per ulteriori informazioni, vedere la sezione [installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuisce gli aggiornamenti di manutenzione Java™ 17 e Java™ 21 per l’utilizzo da parte del cliente nei progetti correlati ad AEM, se non disponibili pubblicamente da Oracle.

#### Packaging Uberjar {#uber-jar-packaging}

* C&#39;è una leggera differenza nel packaging Uberjar di AEM 6.5 LTS. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR AEM Uber](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

#### Aggiorna {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, vedere la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md).

## Installazione e aggiornamento {#install-update}

Per i requisiti di installazione, vedere [istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

Per istruzioni dettagliate, consulta la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Per le nuove installazioni di AEM 6.5 LTS, le definizioni degli indici devono essere installate separatamente. Per ulteriori informazioni, fare riferimento a [questo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, sui [requisiti tecnici AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Si consiglia di utilizzare Java™ 17/Java™ 21 con AEM 6.5 LTS.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe esamina continuamente le funzionalità dei prodotti per migliorare il valore del cliente modernizzando o sostituendo le funzioni meno recenti. Queste modifiche vengono apportate prestando particolare attenzione alla compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità di Adobe Experience Manager (AEM), si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Anche se obsolete, le funzionalità sono ancora disponibili ma non vengono ulteriormente migliorate.
1. La rimozione delle funzionalità obsolete avviene non prima della versione principale successiva. La data effettiva di rimozione è pianificata per essere annunciata in un secondo momento.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

### Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità che Adobe ha dichiarato obsolete in AEM 6.5 LTS. In genere, Adobe depreca le funzioni prima di rimuoverle in una versione futura e fornisce un’alternativa.


Consigliamo ai clienti di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|---|---|---|---|
| Sites | [Editor SPA](/help/sites-developing/spa-overview.md) | Gli editor preferiti per la gestione dei contenuti headless in AEM sono:<br>- [l’editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.<br>- [Editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo. | 6.5 LTS GA |

### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic non è supportato. | Esegui la migrazione a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluzioni | Social network/Communities non supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Screens | Screens non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Risorse | `dam-pim` e `dam-rating` non sono supportati perché i bundle dipendono dal social network. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Risorse | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` è stato rimosso. | Utilizzare l&#39;API alternativa `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` che è stata aggiunta. | 6.5 LTS GA |
| Portale | AEM Portal Director non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | Il bundle `com.adobe.granite.socketio` è stato rimosso. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Granite | `crx2oak` non è supportato. | Scegli la versione rilevante di [oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Guava | Tutte le dipendenze guava ora vengono rimosse in AEM e pertanto il bundle `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` non fa parte di AEM. | Se possibile, i clienti possono aggiungere guava autonomamente se dipendono da guava o sostituire il codice guava con raccolte java o altre alternative. | 6.5 LTS GA |
| We.Retail | Il sito di esempio We-retail non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | Il bundle `oak-solr-osgi` non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` e `org.apache.sling.atom.taglib` non sono supportati. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Open source | `org.apache.commons.io` pacchetti ora esportati da `org.apache.commons.commons-io`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | Esportazione di `javax.mail` pacchetti dal bundle `com.sun.javax.mail`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | `org.apache.jackrabbit.api` pacchetti ora sono esportati dal bundle `org.apache.jackrabbit.oak-jackrabbit-api`. | Nessuna modifica richiesta. | 6.5 LTS GA |
| Open source | `com.github.jknack.handlebars` non è supportato | Scegli la [versione](https://mvnrepository.com/artifact/com.github.jknack/handlebars) pertinente | 6.5 LTS GA |

## Problemi noti {#known-issues}

### Problema con il bundle di script JSP in AEM 6.5.21-6.5.23 e AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23 e AEM 6.5 LTS GA vengono forniti con il bundle `org.apache.sling.scripting.jsp:2.6.0`, che contiene un problema noto. Il problema si verifica in genere con un carico elevato quando l’istanza AEM gestisce molte richieste simultanee.

Quando si verifica questo problema, è possibile che nei registri errori venga visualizzata una delle eccezioni seguenti insieme ai riferimenti a `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip).

### Errore di connessione Dispatcher con funzione solo SSL {#ssl-only-feature}

Quando si abilita la funzione solo SSL nelle distribuzioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze Dispatcher e AEM. Dopo aver abilitato questa funzione, i controlli di integrità potrebbero non riuscire e la comunicazione tra le istanze Dispatcher e AEM potrebbe essere interrotta. Questo problema si verifica in modo specifico quando i clienti tentano di connettersi tramite `https + IP` dalle istanze di Dispatcher alle istanze di AEM ed è relativo a problemi di convalida SNI (Server Name Indication).

**Impatto:**

* Errori di verifica stato con codici di risposta HTTP 400
* Traffico interrotto tra istanze Dispatcher e AEM
* Il contenuto non può essere gestito correttamente tramite Dispatcher
* Errori di connessione durante l’utilizzo di HTTPS con indirizzi IP nella configurazione di Dispatcher
* HTTP 400 - Errori &quot;SNI non valido&quot; durante la connessione tramite HTTPS + IP

**Ambienti interessati:**

* Distribuzioni di AEM con configurazioni Dispatcher
* Sistemi in cui è stata abilitata la funzione solo SSL
* Configurazioni Dispatcher che utilizzano il metodo di connessione `https + IP` alle istanze AEM

**Soluzione:**
Se riscontri questo problema, contatta l’Assistenza clienti Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip). Non tentare di abilitare le funzionalità solo SSL finché non viene applicato l’hotfix necessario.

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto all&#39;indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta L&#39;Assistenza Clienti Adobe](https://experienceleague.adobe.com/it/docs/customer-one/using/home).

