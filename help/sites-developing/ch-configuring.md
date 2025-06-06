---
title: Configurazione di ContextHub
description: Scopri come configurare Context Hub di Adobe Experience Manager per personalizzare le esperienze.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: 00dfc10f-6cdf-4c79-b11e-85c801425858
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 1%

---

# Configurazione di ContextHub {#configuring-contexthub}

ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali. Per ulteriori dettagli su ContextHub, consulta la [documentazione per gli sviluppatori](/help/sites-developing/contexthub.md). ContextHub sostituisce [ClientContext](/help/sites-administering/client-context.md) nell&#39;interfaccia utente touch.

Configura la barra degli strumenti [ContextHub](/help/sites-developing/contexthub.md) per controllare se viene visualizzata in modalità Anteprima, per creare archivi ContextHub e aggiungere moduli di interfaccia utente tramite l&#39;interfaccia utente ottimizzata per il tocco.

## Disabilitazione di ContextHub {#disabling-contexthub}

Per impostazione predefinita, ContextHub è abilitato in un’installazione di AEM. ContextHub può essere disabilitato per impedirgli di caricare js/css e di inizializzare.

<!--
There are two options to disable ContextHub:

* Edit the ContextHub's configuration and check the option **Disable ContextHub**

    1. In the rail click **Tools &gt; Sites &gt; ContextHub**
    1. Click the appropriate **Configuration Container**
    1. Select the **ContextHub Configuration** and click **Edit Selected Element**
    1. Click **Disable ContextHub** and click **Save**

or
-->

* Utilizzare CRXDE Lite per impostare la proprietà `disabled` su **true** in `/libs/settings/cloudsettings/legacy/contexthub`

## Visualizzazione e nascondere l’interfaccia utente di ContextHub {#showing-and-hiding-the-contexthub-ui}

Configura il servizio OSGi ContextHub Adobe Granite per mostrare o nascondere la [interfaccia utente ContextHub](/help/sites-authoring/ch-previewing.md) nelle tue pagine. Il PID di questo servizio è `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Per configurare il servizio è possibile utilizzare la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un nodo [JCR nell&#39;archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Console Web:** Per visualizzare l&#39;interfaccia utente, selezionare la proprietà Mostra interfaccia utente. Per nascondere l’interfaccia utente, cancella la proprietà Nascondi interfaccia utente.
* **Nodo JCR:** Per visualizzare l&#39;interfaccia utente, impostare la proprietà booleana `com.adobe.granite.contexthub.show_ui` su `true`. Per nascondere l&#39;interfaccia utente, impostare la proprietà su `false`.

Quando viene visualizzata l’interfaccia utente di ContextHub, viene visualizzata solo sulle pagine delle istanze di authoring di AEM. L’interfaccia utente non viene visualizzata nelle pagine delle istanze di pubblicazione.

## Aggiunta di modalità e moduli dell’interfaccia utente ContextHub {#adding-contexthub-ui-modes-and-modules}

Configura le modalità e i moduli dell’interfaccia utente visualizzati nella barra degli strumenti di ContextHub in modalità Anteprima:

* Modalità interfaccia utente: gruppi di moduli correlati
* Moduli: widget che espongono i dati contestuali da un archivio e consentono agli autori di manipolare il contesto

Le modalità dell’interfaccia utente vengono visualizzate sotto forma di una serie di icone sul lato sinistro della barra degli strumenti. Se selezionata, i moduli di una modalità interfaccia utente vengono visualizzati a destra.

![chlimage_1-319](assets/chlimage_1-319.png)

Le icone sono riferimenti dalla [libreria di icone dell&#39;interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Aggiunta di una modalità interfaccia utente {#adding-a-ui-mode}

Aggiungi una modalità interfaccia utente per raggruppare i moduli ContextHub correlati. Quando crei la modalità interfaccia utente, fornisci il titolo e l’icona visualizzati nella barra degli strumenti di ContextHub.

1. Nella barra di Experience Manager, fai clic su Strumenti > Siti > Context Hub.
1. Fai clic sul Contenitore di configurazione predefinito.
1. Fai clic sulla configurazione Context Hub.
1. Fai clic sul pulsante Crea, quindi fai clic su Modalità interfaccia utente Context Hub.

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. Immetti i valori per le seguenti proprietà:

   * Titolo modalità interfaccia utente: titolo che identifica la modalità interfaccia utente
   * Icona modalità: selettore dell&#39;[icona dell&#39;interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) da utilizzare, ad esempio `coral-Icon--user`
   * Abilitato: seleziona per visualizzare la modalità interfaccia utente nella barra degli strumenti di ContextHub

1. Fai clic su Salva.

### Aggiunta di un modulo interfaccia utente {#adding-a-ui-module}

Aggiungi un modulo dell’interfaccia utente ContextHub a una modalità interfaccia utente in modo che venga visualizzato nella barra degli strumenti di ContextHub per l’anteprima del contenuto della pagina. Quando aggiungi un modulo di interfaccia utente, stai creando un’istanza di un tipo di modulo registrato con ContextHub. Per aggiungere un modulo di interfaccia utente, è necessario conoscere il nome del tipo di modulo associato.

AEM fornisce un tipo di modulo dell’interfaccia utente di base e diversi tipi di modulo dell’interfaccia utente di esempio su cui puoi basare un modulo dell’interfaccia utente. La tabella seguente fornisce una breve descrizione di ciascuno di essi. Per informazioni sullo sviluppo di un modulo interfaccia utente personalizzato, vedi [Creazione di moduli interfaccia utente ContextHub](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Le proprietà del modulo UI includono una configurazione dettagliata in cui puoi fornire valori per le proprietà specifiche del modulo. Fornisci la configurazione dei dettagli in formato JSON. La colonna Tipo modulo nella tabella fornisce collegamenti a informazioni sul codice JSON necessario per ogni tipo di modulo dell’interfaccia utente.

| Tipo modulo | Descrizione | Store |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | Un tipo di modulo interfaccia utente generico | Configurato nelle proprietà del modulo interfaccia utente |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | Visualizza informazioni sul browser | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | Visualizza informazioni su data e ora | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | Visualizza il dispositivo client | emulatori |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | Visualizza la latitudine e la longitudine del client e la posizione su una mappa. Consente di modificare la posizione. | geolocalizzazione |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | Visualizza l&#39;orientamento dello schermo del dispositivo (orizzontale o verticale) | emulatori |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | Visualizza le statistiche sui tag pagina | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | Visualizza le informazioni di profilo per l&#39;utente corrente, inclusi authorizableID, displayName e familyName. È possibile modificare il valore di displayName e familyName. | profilo |

1. Nella barra di Experience Manager, fai clic su Strumenti > Siti > ContextHub.
1. Fai clic sul Contenitore di configurazione a cui desideri aggiungere un modulo di interfaccia utente.
1. Fai clic o digita la configurazione ContextHub a cui desideri aggiungere il modulo di interfaccia utente.
1. Fai clic sulla modalità dell’interfaccia utente a cui stai aggiungendo il modulo dell’interfaccia utente.
1. Fai clic sul pulsante Crea, quindi fai clic su Modulo interfaccia utente ContextHub (generico).

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. Immetti i valori per le seguenti proprietà:

   * Titolo modulo interfaccia utente: titolo che identifica il modulo interfaccia utente
   * Tipo di modulo: il tipo di modulo
   * Abilitato: seleziona per mostrare il modulo interfaccia utente nella barra degli strumenti di ContextHub

1. (Facoltativo) Per ignorare la configurazione predefinita dell’archivio, immetti un oggetto JSON per configurare il modulo interfaccia utente.
1. Fai clic su Salva.

## Creazione di un archivio ContextHub {#creating-a-contexthub-store}

Crea un archivio Context Hub per rendere persistenti i dati utente e accedere ai dati in base alle esigenze. Gli store ContextHub si basano sui candidati di store registrati. Quando si crea lo store, è necessario il valore dello storeType con cui è stato registrato il candidato dello store. (Vedi [Creazione di candidati per store personalizzati](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).)

### Configurazione archivio dettagliata {#detailed-store-configuration}

Quando si configura un archivio, la proprietà Configurazione dettagli consente di fornire valori per le proprietà specifiche del negozio. Il valore è basato sul parametro `config` della funzione `init` dell&#39;archivio. Pertanto, l’eventuale necessità di fornire questo valore e il formato del valore dipendono dall’archivio.

Il valore della proprietà Configurazione dettagli è un oggetto `config` in formato JSON.

### Candidati dell’archivio esempi {#sample-store-candidates}

AEM fornisce i seguenti esempi di store candidati su cui puoi basare uno store.

| Tipo di archivio | Descrizione |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | Archivia per segmenti ContextHub risolti e non risolti. Recupera automaticamente i segmenti da ContextHub SegmentManager |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | Memorizza i segmenti attualmente risolti. Ascolta il servizio SegmentManager di ContextHub per aggiornare automaticamente lo store |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | Memorizza la latitudine e la longitudine della posizione del browser. |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | Memorizza la data, l’ora e la stagione correnti per la posizione del browser |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | Definisce proprietà e funzionalità per diversi dispositivi e rileva il dispositivo client corrente |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | Recupera e memorizza i dati da un servizio JSONP |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | Memorizza i dati profilo per l&#39;utente corrente |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | Memorizza informazioni sul client, ad esempio informazioni sul dispositivo, il tipo di browser e l&#39;orientamento della finestra |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | Memorizza i tag di pagina e i conteggi dei tag |

1. Nella barra di Experience Manager, fai clic su Strumenti > Siti > ContextHub.
1. Fai clic sul contenitore di configurazione predefinito.
1. Fai clic su Configurazione Contexthub
1. Per aggiungere un archivio, fai clic sull’icona Crea, quindi fai clic su Configurazione archivio ContexHub.

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. Immetti i valori per le proprietà di configurazione di base, quindi fai clic su Avanti:

   * **Titolo configurazione:** Titolo che identifica l&#39;archivio
   * **Tipo archivio:** il valore della proprietà storeType del candidato archivio su cui basare l&#39;archivio
   * **Obbligatorio:** Seleziona
   * **Abilitato:** Selezionare per abilitare l&#39;archivio

1. (Facoltativo) Per ignorare la configurazione predefinita dell’archivio, immetti un oggetto JSON nella casella Configurazione dettaglio (JSON).
1. Fai clic su Salva.

## Esempio: utilizzo di un servizio JSONP  {#example-using-a-jsonp-service}

Questo esempio illustra come configurare un archivio e visualizzare i dati in un modulo dell’interfaccia utente. In questo esempio, il servizio MD5 del sito jsontest.com viene utilizzato come origine dati per un archivio. Il servizio restituisce il codice hash MD5 di una determinata stringa, in formato JSON.

Un archivio contexthub.generic-jsonp è configurato in modo da memorizzare i dati per la chiamata al servizio `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. Il servizio restituisce i seguenti dati visualizzati in un modulo dell’interfaccia utente:

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Creazione di un archivio contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

Il candidato per l’archivio di campioni contexthub.generic-jsonp consente di recuperare dati da un servizio JSONP o da un servizio web che restituisce dati JSON. Per questo candidato all&#39;archivio, utilizza la configurazione dell&#39;archivio per fornire dettagli sul servizio JSONP da utilizzare.

La funzione [init](/help/sites-developing/contexthub-api.md#init-name-config) della classe JavaScript `ContextHub.Store.JSONPStore` definisce un oggetto `config` che inizializza il candidato dell&#39;archivio. L&#39;oggetto `config` contiene un oggetto `service` che include dettagli sul servizio JSONP. Per configurare l&#39;archivio, specificare l&#39;oggetto `service` in formato JSON come valore per la proprietà Configurazione dettagli.

Per salvare i dati dal servizio MD5 del sito jsontest.com, utilizzare la procedura in [Creazione di un archivio ContextHub](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) utilizzando le proprietà seguenti:

* **Titolo configurazione:** md5
* **Tipo di archivio:** contexthub.generic-jsonp
* **Obbligatorio:** Seleziona
* **Abilitato:** Seleziona
* **Configurazione dettagli (JSON):**

  ```xml
  {
   "service": {
   "jsonp": false,
   "timeout": 1000,
   "ttl": 1800000,
   "secure": false,
   "host": "md5.jsontest.com",
   "port": 80,
   "params":{
   "text":"text to md5"
       }
     }
   }
  ```

### Aggiunta di un modulo interfaccia utente per i dati md5 {#adding-a-ui-module-for-the-md-data}

Aggiungi un modulo di interfaccia utente alla barra degli strumenti di ContextHub per visualizzare i dati memorizzati nell’archivio md5 di esempio. In questo esempio, il modulo contexthub.base viene utilizzato per produrre il seguente modulo di interfaccia utente:

![chlimage_1-323](assets/chlimage_1-323.png)

Segui la procedura descritta in [Aggiunta di un modulo interfaccia utente](#adding-a-ui-module) per aggiungere il modulo a una modalità interfaccia utente esistente, ad esempio la modalità interfaccia utente personale di esempio. Per il modulo UI, utilizza i seguenti valori delle proprietà:

* **Titolo modulo interfaccia utente:** MD5
* **Tipo modulo:** contexthub.base
* **Configurazione dettagli (JSON):**

  ```xml
  {
   "icon": "coral-Icon--data",
   "title": "MD5 Converstion",
   "storeMapping": { "md5": "md5" },
   "template": "<p> {{md5.original}}</p>;
                <p>{{md5.md5}}</p>"
  }
  ```

## Debug di ContextHub {#debugging-contexthub}

È possibile abilitare una modalità di debug per ContextHub per consentire la risoluzione dei problemi. La modalità di debug può essere abilitata tramite la configurazione ContextHub o tramite CRXDE.

### Tramite la configurazione {#via-the-configuration}

Modifica la configurazione di ContextHub e seleziona l&#39;opzione **Debug**

1. Nella barra fai clic su **Strumenti > Siti > ContextHub**
1. Fai clic sul **contenitore configurazione** predefinito
1. Seleziona la **configurazione ContextHub** e fai clic su **Modifica elemento selezionato**
1. Fai clic su **Debug** e fai clic su **Salva**

### Via CRXDE {#via-crxde}

Utilizzare CRXDE Lite per impostare la proprietà `debug` su **true** in:

* `/conf/global/settings/cloudsettings` o
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>Per le configurazioni ContextHub ancora presenti nei percorsi legacy, la posizione per impostare `debug property` è `/libs/settings/cloudsettings/legacy/contexthub`.

### Modalità silenziosa {#silent-mode}

La modalità silenziosa sopprime tutte le informazioni di debug. A differenza della normale opzione di debug, che può essere impostata in modo indipendente per ogni configurazione ContextHub, la modalità silenziosa è un’impostazione globale che ha la precedenza su qualsiasi impostazione di debug a livello di configurazione ContextHub.

Questa funzione è utile per l’istanza Publish, in cui non desideri ricevere informazioni di debug. Poiché si tratta di un’impostazione globale, viene abilitata tramite OSGi.

1. Apri la **configurazione console Web Adobe Experience Manager** in `http://<host>:<port>/system/console/configMgr`
1. Cerca **Adobe Granite ContextHub**
1. Fai clic sulla configurazione **Adobe Granite ContextHub** per modificarne le proprietà
1. Seleziona l&#39;opzione **Modalità silenziosa** e fai clic su **Salva**

## Ripristino delle configurazioni ContextHub dopo l&#39;aggiornamento {#recovering-contexthub-configurations-after-upgrading}

Quando viene eseguito un aggiornamento [ad AEM](/help/sites-deploying/upgrade.md), le configurazioni ContextHub vengono sottoposte a backup e archiviate in un percorso sicuro. Durante l’aggiornamento, vengono installate le configurazioni ContextHub predefinite, che sostituiscono quelle esistenti. Il backup è necessario per conservare le modifiche o le aggiunte apportate.

Le configurazioni ContextHub sono archiviate in una cartella denominata `contexthub` nei seguenti nodi:

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

Dopo un aggiornamento, il backup viene archiviato in una cartella denominata `contexthub` sotto un nodo denominato:

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` o
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

La parte `yyyymmdd` del nome del nodo è la data in cui è stato eseguito l&#39;aggiornamento.

Per recuperare le configurazioni ContextHub, utilizza CRXDE Lite per copiare i nodi che rappresentano i tuoi store, le modalità dell’interfaccia utente e i moduli dell’interfaccia utente da sotto il nodo `default-pre-upgrade_yyyymmdd_xxxxxx` a sotto:

* `/conf/global/settings/cloudsettings` o
* `/conf/<tenant>/settings/cloudsettings`
