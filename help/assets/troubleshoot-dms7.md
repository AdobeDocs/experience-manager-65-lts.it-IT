---
title: Risoluzione dei problemi di Dynamic Media - Modalità Scene7
description: Scopri come risolvere i problemi di configurazione e configurazione e i problemi generali in Dynamic Media quando è in esecuzione in modalità Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Troubleshooting
mini-toc-levels: 3
solution: Experience Manager, Experience Manager Assets
exl-id: 469495f2-b6d3-490d-a5df-ffa07b30cc1e
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 0%

---

# Risoluzione dei problemi di Dynamic Media - Modalità Scene7{#troubleshooting-dynamic-media-scene-mode}

Nel documento seguente viene descritta la risoluzione dei problemi per Dynamic Media che esegue la modalità di esecuzione **dynamicmedia_scene7**.

## Configurazione e configurazione {#setup-and-configuration}

Assicurati che Dynamic Media sia stato configurato correttamente eseguendo le seguenti operazioni:

* Il comando Start up contiene l&#39;argomento della modalità di esecuzione `-r dynamicmedia_scene7`.
* Tutti i pacchetti di correzione cumulativi (CFP, Cumulative Fix Pack) di Adobe Experience Manager 6.4 sono stati installati *prima* dei pacchetti di funzionalità Dynamic Media disponibili.
* È installato l&#39;18912 opzionale Feature Pack.

  Questo feature pack opzionale è per il supporto FTP o se stai eseguendo la migrazione di risorse a Dynamic Media da Dynamic Media Classic.

* Passa all&#39;interfaccia utente di Cloud Services e verifica che l&#39;account con provisioning sia visualizzato in **[!UICONTROL Configurazioni disponibili]**.
* Verificare che l&#39;agente di replica `Dynamic Media Asset Activation (scene7)` sia abilitato.

  Questo agente di replica si trova in Agenti sull’autore.

## Generale (tutte le Assets) {#general-all-assets}

Di seguito sono riportati alcuni suggerimenti di carattere generale per tutte le risorse.

### Proprietà stato sincronizzazione risorse {#asset-synchronization-status-properties}

Per confermare la corretta sincronizzazione della risorsa da Experience Manager a Dynamic Media, in CRXDE Lite è possibile rivedere le seguenti proprietà della risorsa:

| **Proprietà** | **Esempio** | **Descrizione** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | Indicatore generale che il nodo è collegato a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** o testo di errore | Stato del caricamento della risorsa in Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve essere compilata per generare gli URL della risorsa remota di Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **operazione riuscita** o **non riuscita:`<error text>`** | Stato di sincronizzazione di set (set 360 gradi, set di immagini e così via), predefiniti immagine, predefiniti visualizzatore, aggiornamenti mappa immagine per una risorsa o immagini modificate. |

### Registrazione sincronizzazione {#synchronization-logging}

Errori e problemi di sincronizzazione registrati in `error.log` (directory server Experience Manager `/crx-quickstart/logs/`). È disponibile una registrazione sufficiente per determinare la causa principale della maggior parte dei problemi, tuttavia è possibile aumentare la registrazione a DEBUG sul pacchetto `com.adobe.cq.dam.ips` tramite la console Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) per raccogliere ulteriori informazioni.

### Sposta, Copia, Elimina {#move-copy-delete}

Prima di eseguire un&#39;operazione di spostamento, copia o eliminazione, effettuare le seguenti operazioni:

* Per immagini e video, verificare che esista un valore `<object_node>/jcr:content/metadata/dam:scene7ID` prima di eseguire operazioni di spostamento, copia o eliminazione.
* Per i predefiniti immagine e visualizzatore, verificare che esista un valore `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` prima di eseguire operazioni di spostamento, copia o eliminazione.
* Se manca il valore dei metadati precedente, devi ricaricare le risorse prima delle operazioni di spostamento, copia o eliminazione.

### Controllo della versione {#version-control}

Quando sostituisci una risorsa Dynamic Media esistente (con lo stesso nome e la stessa posizione), puoi mantenere entrambe le risorse o sostituirle o crearne una versione:

* Mantenendo entrambe, viene creata una risorsa con un nome univoco per l’URL della risorsa pubblicata. Ad esempio, `image.jpg` è la risorsa originale e `image1.jpg` è la risorsa appena caricata.

* La creazione di una versione non è supportata nella consegna in modalità Dynamic Media - Scene7. La nuova versione sostituisce la risorsa esistente nella consegna.

## Immagini e set {#images-and-sets}

In caso di problemi con immagini e set, vedere le seguenti indicazioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema  </strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile accedere al pulsante Copia URL/Incorpora nella vista dei dettagli della risorsa</td>
   <td>
    <ol>
     <li><p>Vai a CRX/DE:</p>
      <ul>
       <li>Verifica se il predefinito nel JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> è definito. Questa posizione si applica se hai effettuato l’aggiornamento da Experience Manager 6.x a 6.4 e hai rinunciato alla migrazione. In caso contrario, il percorso è <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifica che la risorsa nel JCR contenga <code>dam:scene7FileStatus</code><strong> </strong>in Metadati che sia visualizzato come <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Aggiorna pagina/passa a un'altra pagina e torna indietro (la barra laterale JSP deve essere ricompilata)</p> <p>Se non funziona:</p>
    <ul>
     <li>Pubblica risorsa.</li>
     <li>Ricarica la risorsa e pubblicala.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Il selettore delle risorse nell’editor dei set è bloccato nel caricamento permanente</td>
   <td><p>Problema noto da risolvere nella versione 6.4</p> </td>
   <td><p>Chiudere il selettore e riaprirlo.</p> </td>
  </tr>
  <tr>
   <td>Il pulsante <strong>Seleziona</strong> non è attivo dopo aver selezionato una risorsa come parte della modifica di un set</td>
   <td><p> </p> <p>Problema noto da risolvere nella versione 6.4</p> <p> </p> </td>
   <td><p>Seleziona prima un’altra cartella nel Selettore risorse, quindi torna indietro per selezionare la risorsa.</p> </td>
  </tr>
  <tr>
   <td>L’hotspot carosello si sposta dopo il passaggio tra le diapositive</td>
   <td><p>Verificare che tutte le diapositive abbiano le stesse dimensioni.</p> </td>
   <td><p>Per il carosello utilizzare solo immagini della stessa dimensione.</p> </td>
  </tr>
  <tr>
   <td>L’immagine non viene visualizzata in anteprima con il visualizzatore Dynamic Media</td>
   <td><p>Verifica che la risorsa contenga <code>dam:scene7File</code> nelle proprietà dei metadati (CRXDE Lite)</p> </td>
   <td><p>Verifica che l'elaborazione di tutte le risorse sia stata completata.</p> </td>
  </tr>
  <tr>
   <td>La risorsa caricata non viene visualizzata nel selettore risorse</td>
   <td><p>Verifica che la risorsa abbia la proprietà <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifica che l'elaborazione di tutte le risorse sia stata completata.</p> </td>
  </tr>
  <tr>
   <td>Il banner nella vista a schede mostra <strong>Nuovo</strong> quando la risorsa non ha iniziato l'elaborazione</td>
   <td>Controlla risorsa <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code>, non è stata selezionata dal flusso di lavoro.</td>
   <td>Attendi che la risorsa venga selezionata dal flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Le immagini o i set non visualizzano l’URL del visualizzatore o il codice da incorporare</td>
   <td>Controlla se il predefinito visualizzatore è stato pubblicato.</td>
   <td><p>Vai a <strong>Strumenti</strong> &gt; <strong>Assets</strong> &gt; <strong>Predefiniti visualizzatore</strong> e pubblica il predefinito visualizzatore.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

In caso di problemi con il video, consulta le seguenti linee guida per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema  </strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile visualizzare il video in anteprima</td>
   <td>
    <ul>
     <li>Verifica che alla cartella sia assegnato un profilo video (se il formato di file non è supportato). Se non è supportato, viene visualizzata solo un’immagine.</li>
     <li>Il profilo video deve contenere più di un predefinito di codifica per generare un set AVS (le codifiche singole vengono trattate come contenuto video per i file MP4; per i file non supportati, trattate come non elaborate).</li>
     <li>Verificare che l'elaborazione del video sia stata completata confermando <code>dam:scene7FileAvs</code> di <code>dam:scene7File</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegna un profilo video alla cartella.</li>
     <li>Modifica il profilo video in modo da includere più predefiniti di codifica.</li>
     <li>Attendi che il video finisca l’elaborazione.</li>
     <li>Ricaricare il video, verificare che il flusso di lavoro Codifica video elementi multimediali dinamici non sia in esecuzione.<br /> </li>
     <li>Ricarica il video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Video non codificato</td>
   <td>
    <ul>
     <li>Verificare che la modalità di esecuzione sia <code>dynamicmedia_scene7</code>.</li>
     <li>Verifica se il servizio cloud Dynamic Media è configurato.</li>
     <li>Verifica se un profilo video è associato alla cartella di caricamento.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Controlla l’istanza di Experience Manager con <code>-r dynamicmedia_scene7</code></li>
     <li>Verifica che la configurazione di Dynamic Media in Cloud Services sia impostata correttamente.</li>
     <li>Verifica che la cartella disponga di un profilo video. Inoltre, controlla il profilo video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L'elaborazione video richiede troppo tempo</td>
   <td><p>Per determinare se la codifica video è ancora in corso o se è entrata in uno stato di errore:</p>
    <ul>
     <li>Controlla lo stato del video <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitorare il video dalla console del flusso di lavoro <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; schede Istanze, Archivio ed Errori.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rappresentazione video mancante</td>
   <td><p>Quando il video viene caricato, ma non sono presenti rappresentazioni codificate:</p>
    <ul>
     <li>Verifica che alla cartella sia assegnato un profilo video.</li>
     <li>Verificare che l'elaborazione del video sia stata completata confermando <code>dam:scene7FileAvs</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegna un profilo video alla cartella.</li>
     <li>Attendere il completamento dell'elaborazione del video.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visualizzatori {#viewers}

In caso di problemi con i visualizzatori, consulta le seguenti linee guida per la risoluzione dei problemi.

### Problema: i predefiniti del visualizzatore non sono pubblicati {#viewers-not-published}

**Eseguire il debug**

1. Passare alla pagina di diagnostica del manager di esempio: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Osserva i valori calcolati. Se funziona correttamente, vengono visualizzati i seguenti elementi: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >La sincronizzazione delle risorse visualizzatore può richiedere circa 10 minuti dopo la configurazione delle impostazioni cloud di Dynamic Media.

1. Se le risorse non attivate rimangono, selezionare uno dei pulsanti **Elenca tutti i pulsanti Assets** non attivati per visualizzare i dettagli.

**Soluzione**

1. Passare all&#39;elenco dei predefiniti visualizzatore negli strumenti di amministrazione: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Seleziona tutti i predefiniti visualizzatore, quindi seleziona **Pubblica**.
1. Torna a Gestione campioni e osserva che il conteggio delle risorse non attivate è ora zero.

### Problema: la grafica del predefinito del visualizzatore restituisce 404 dall’anteprima nei dettagli della risorsa o copia URL/codice di incorporamento {#viewer-preset-404}

**Eseguire il debug**

In CRXDE Lite eseguire le operazioni seguenti:

1. Passa alla cartella `<sync-folder>/_CSS/_OOTB` all&#39;interno della cartella di sincronizzazione di Dynamic Media (ad esempio, `/content/dam/_CSS/_OOTB`).
1. Trovare il nodo metadati della risorsa problematica (ad esempio, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Verificare la presenza di `dam:scene7*` proprietà. Se la risorsa è stata sincronizzata e pubblicata correttamente, il set `dam:scene7FileStatus` è **PublishComplete**.
1. Tentativo di richiedere il disegno direttamente da Dynamic Media concatenando i valori delle seguenti proprietà e stringhe letterali:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Esempio: `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Soluzione**

Se le risorse di esempio o il disegno del predefinito visualizzatore non è stato sincronizzato o pubblicato, riavvia l’intero processo di copia/sincronizzazione:

1. Passa a CRXDE Lite.
1. Elimina `<sync-folder>/_CSS/_OOTB`.
1. Passare a Gestione pacchetti CRX: `https://localhost:4502/crx/packmgr/`.
1. Cercare il pacchetto visualizzatore nell&#39;elenco; inizia con `cq-dam-scene7-viewers-content`.
1. Selezionare **Reinstalla**.
1. In Cloud Services, passa alla pagina Configurazione di Dynamic Media, quindi apri la finestra di dialogo di configurazione per la configurazione di Dynamic Media - S7.
1. Non apportare modifiche, selezionare **Salva**.
Questa azione di salvataggio attiva nuovamente la logica per creare e sincronizzare le risorse di esempio, il CSS del predefinito visualizzatore e il disegno.

### Problema: l’anteprima dell’immagine non viene caricata nella creazione dei predefiniti del visualizzatore {#image-preview-not-loading}

**Soluzione**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Nella barra a sinistra, passa alla cartella del contenuto di esempio nel percorso seguente:

   `/content/dam/_DMSAMPLE`

1. Eliminare la cartella `_DMSAMPLE`.
1. Nella barra a sinistra, accedi alla cartella dei predefiniti nella posizione seguente:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Eliminare la cartella `viewer`.
1. Selezionare **[!UICONTROL Salva tutto]** nell&#39;angolo superiore sinistro della pagina CRXDE Lite.
1. Nell&#39;angolo in alto a sinistra della pagina CRXDE Lite, seleziona l&#39;icona **Torna alla Home**.
1. Ricreare una [configurazione Dynamic Media in Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
