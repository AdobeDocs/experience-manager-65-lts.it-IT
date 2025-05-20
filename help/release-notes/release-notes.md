---
title: Note sulla versione corrente per Adobe Experience Manager 6.5 LTS
description: Queste sono le note sulla versione corrente di Adobe Experience Manager 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: 8f6d152ceeae12cdadd0096e114584ce2a63a2ac
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 24%

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

Quickstart utilizza Eclipse Jetty 11.0.x come servlet engine.

#### Supporto Java™  {#java-support}

* Supporto per Java™ 17 e Java™ 21.
* Per ottenere prestazioni ottimali, sostituire i valori GC predefiniti con altri valori. Per ulteriori informazioni, vedere la sezione [installare e aggiornare](/help/sites-deploying/custom-standalone-install.md).
* Gli aggiornamenti di manutenzione di Java™ 17 e Java™ 21 vengono distribuiti da Adobe per l’utilizzo da parte dei clienti nei progetti correlati ad AEM, quando non sono disponibili al pubblico da Oracle.

#### Packaging Uberjar {#uber-jar-packaging}

* C&#39;è una leggera differenza nel packaging Uberjar di AEM 6.5 LTS. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR AEM Uber](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

#### Aggiorna {#upgrade}

* Per informazioni dettagliate sulla procedura di aggiornamento, vedere la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md).

## Installazione e aggiornamento {#install-update}

Per i requisiti di installazione, vedere [istruzioni di installazione](/help/sites-deploying/custom-standalone-install.md).

Per istruzioni dettagliate, consulta [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md).

## Piattaforme supportate {#supported-platforms}

Trova la matrice completa delle piattaforme supportate, incluso il livello di supporto, sui [requisiti tecnici AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Si consiglia di utilizzare Java™ 17/Java™ 21 con AEM 6.5 LTS.

## Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità di Adobe Experience Manager (AEM), si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Anche se obsolete, le funzionalità sono ancora disponibili ma non vengono ulteriormente migliorate.
1. La rimozione delle funzionalità obsolete avviene non prima della versione principale successiva. La data effettiva di rimozione verrà annunciata in seguito.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

### Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete con AEM 6.5 LTS. In genere, le funzioni pianificate per la rimozione in una versione futura vengono inizialmente impostate come obsolete e ne viene indicata un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|---|---|---|---|
| Sites | [Editor SPA](/help/sites-developing/spa-overview.md) | Gli editor preferiti per la gestione dei contenuti headless in AEM sono:<br>- [l’editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.<br>- [Editor frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) per la modifica basata su modulo. | 6.5 LTS GA |

### Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da AEM 6.5 LTS. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic non è supportato. | Eseguire la migrazione a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluzioni | Social network/Communities non supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
| Screens | Screens non è supportato. | Nessuna sostituzione disponibile. | 6.5 LTS GA |
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

### Errore di connessione Dispatcher con funzione solo SSL {#ssl-only-feature}

Quando si abilita la funzione solo SSL nelle distribuzioni di AEM, si verifica un problema noto che influisce sulla connettività tra le istanze di Dispatcher e AEM. Dopo aver abilitato questa funzione, i controlli di integrità potrebbero non riuscire e la comunicazione tra le istanze di Dispatcher e AEM potrebbe essere interrotta.

**Impatto:**
* Errori di verifica stato con codici di risposta HTTP 500
* Traffico interrotto tra istanze di Dispatcher e AEM
* Il contenuto non può essere gestito correttamente tramite Dispatcher

**Ambienti interessati:**
* Distribuzioni di AEM con configurazioni del dispatcher
* Sistemi in cui è stata abilitata la funzione solo SSL

**Soluzione:**
Se riscontri questo problema, contatta l’Assistenza clienti Adobe. Per risolvere il problema è disponibile un hotfix [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.0.zip). Non tentare di abilitare le funzionalità solo SSL finché non viene applicato l’hotfix necessario.

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto all&#39;indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta L&#39;Assistenza Clienti Adobe](https://experienceleague.adobe.com/it/docs/customer-one/using/home).

