---
title: Interazione con i flussi di lavoro a livello di programmazione
description: Scopri come interagire con i flussi di lavoro a livello di programmazione in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7e14471e-8bb5-4cce-9175-3bbff9d803a9
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 0%

---

# Interazione con i flussi di lavoro a livello di programmazione{#interacting-with-workflows-programmatically}

Quando [personalizzi ed estendi i flussi di lavoro](/help/sites-developing/workflows-customizing-extending.md) puoi accedere agli oggetti del flusso di lavoro:

* [Utilizzo dell’API Java del flusso di lavoro](#using-the-workflow-java-api)
* [Ottenimento di oggetti del flusso di lavoro negli script ECMA](#obtaining-workflow-objects-in-ecma-scripts)
* [Utilizzo dell’API REST del flusso di lavoro](#using-the-workflow-rest-api)

## Utilizzo dell’API Java del flusso di lavoro {#using-the-workflow-java-api}

L&#39;API Java del flusso di lavoro è costituita dal pacchetto [`com.adobe.granite.workflow`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/package-summary.html) e da diversi pacchetti secondari. Il membro più significativo dell&#39;API è la classe `com.adobe.granite.workflow.WorkflowSession`. La classe `WorkflowSession` consente di accedere sia agli oggetti del flusso di lavoro in fase di progettazione che a quelli di runtime:

* modelli di workflow
* elementi di lavoro
* istanze del flusso di lavoro
* dati del flusso di lavoro
* elementi casella in entrata

La classe fornisce anche diversi metodi per intervenire nei cicli di vita del flusso di lavoro.

La tabella seguente fornisce collegamenti alla documentazione di riferimento di diversi oggetti Java chiave da utilizzare durante l’interazione a livello di programmazione con i flussi di lavoro. Negli esempi seguenti viene illustrato come ottenere e utilizzare gli oggetti class nel codice.

| Funzioni | Oggetti |
|---|---|
| Accesso a un flusso di lavoro | [`WorkflowSession`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| Esecuzione e query di un’istanza di flusso di lavoro | [`Workflow`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| Gestione di un modello di flusso di lavoro | [`WorkflowModel`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| Informazioni per un nodo presente o meno nel flusso di lavoro | [`WorkflowStatus`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## Ottenimento di oggetti del flusso di lavoro negli script ECMA {#obtaining-workflow-objects-in-ecma-scripts}

Come descritto in [Individuazione dello script](/help/sites-developing/the-basics.md#locating-the-script), AEM (tramite Apache Sling) fornisce un motore di script ECMA che esegue script ECMA lato server. La classe [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) è immediatamente disponibile per gli script come variabile `sling`.

La classe `ScriptHelper` fornisce l&#39;accesso a `SlingHttpServletRequest` che è possibile utilizzare per ottenere l&#39;oggetto `WorkflowSession`, ad esempio:

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## Utilizzo dell’API REST del flusso di lavoro {#using-the-workflow-rest-api}

La console Flusso di lavoro fa un uso intensivo dell’API REST; pertanto questa pagina descrive l’API REST per i flussi di lavoro.

>[!NOTE]
>
>Lo strumento per riga di comando cURL consente di utilizzare l’API REST di Workflow per accedere agli oggetti del flusso di lavoro e gestire i cicli di vita delle istanze. Gli esempi in questa pagina illustrano l’utilizzo dell’API REST tramite lo strumento per riga di comando cURL.

Con l’API REST sono supportate le seguenti azioni:

* avviare o arrestare un servizio del flusso di lavoro
* creare, aggiornare o eliminare modelli di flusso di lavoro
* [avviare, sospendere, riprendere o terminare istanze del flusso di lavoro](/help/sites-administering/workflows.md#workflow-status-and-actions)
* completare o delegare elementi di lavoro

>[!NOTE]
>
>Utilizzando Firebug, un’estensione Firefox per lo sviluppo web, è possibile seguire il traffico HTTP quando viene utilizzata la console. Ad esempio, è possibile controllare i parametri e i valori inviati al server AEM con una richiesta `POST`.

In questa pagina si presume che AEM venga eseguito su localhost alla porta `4502` e che il contesto di installazione sia &quot; `/`&quot; (radice). In caso contrario, è necessario adattare di conseguenza gli URI a cui si applicano le richieste HTTP.

Il rendering supportato per `GET` richieste è il rendering JSON. Gli URL per `GET` devono avere l&#39;estensione `.json`, ad esempio:

`http://localhost:4502/etc/workflow.json`

### Gestione delle istanze dei flussi di lavoro {#managing-workflow-instances}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>metodo di richiesta HTTP</td>
   <td>Azioni</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Elenca le istanze di flusso di lavoro disponibili.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>Crea una nuova istanza di flusso di lavoro. I parametri sono:<br /> - <code>model</code>: l'ID (URI) del rispettivo modello di flusso di lavoro<br /> - <code>payloadType</code>: contenente il tipo di payload (ad esempio, <code>JCR_PATH</code> o URL).<br /> Il payload viene inviato come parametro <code>payload</code>. Viene inviata nuovamente una risposta <code>201</code> (<code>CREATED</code>) con un'intestazione di posizione contenente l'URL della nuova risorsa istanza del flusso di lavoro.</p> </td>
  </tr>
 </tbody>
</table>

#### Gestione di un’istanza di flusso di lavoro in base al suo stato {#managing-a-workflow-instance-by-its-state}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/etc/workflow/instances.{state}`

| metodo di richiesta HTTP | Azioni |
|---|---|
| `GET` | Elenca le istanze di flusso di lavoro disponibili e i relativi stati ( `RUNNING`, `SUSPENDED`, `ABORTED` o `COMPLETED`) |

#### Gestione di un’istanza di flusso di lavoro per il relativo ID {#managing-a-workflow-instance-by-its-id}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>metodo di richiesta HTTP</td>
   <td>Azioni</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Ottiene i dati delle istanze (definizione e metadati), incluso il collegamento al rispettivo modello di flusso di lavoro.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Modifica lo stato dell’istanza. Il nuovo stato viene inviato come parametro <code>state</code> e deve avere uno dei seguenti valori: <code>RUNNING</code>, <code>SUSPENDED</code> o <code>ABORTED</code>.<br /> Se il nuovo stato non è raggiungibile (ad esempio, quando si sospende un'istanza terminata), viene inviata nuovamente al client una risposta <code>409</code> (<code>CONFLICT</code>).</td>
  </tr>
 </tbody>
</table>

### Gestione dei modelli di flussi di lavoro {#managing-workflow-models}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>metodo di richiesta HTTP</td>
   <td>Azioni</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Elenca i modelli di workflow disponibili.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Crea un nuovo modello di workflow. Se il parametro <code>title</code> viene inviato, viene creato un nuovo modello con il titolo specificato. Quando si allega una definizione di modello JSON come parametro <code>model</code>, viene creato un nuovo modello di flusso di lavoro in base alla definizione fornita.<br /> Viene inviata una risposta <code>201</code> (<code>CREATED</code>) con un'intestazione di posizione contenente l'URL della nuova risorsa modello flusso di lavoro.<br /> Lo stesso accade quando una definizione di modello viene allegata come parametro di file denominato <code>modelfile</code>.<br /> In entrambi i casi dei parametri <code>model</code> e <code>modelfile</code>, è necessario un parametro aggiuntivo denominato <code>type</code> per definire il formato di serializzazione. È possibile integrare nuovi formati di serializzazione utilizzando l’API OSGI. Con il motore del flusso di lavoro viene fornito un serializzatore JSON standard. Il tipo è JSON. Di seguito è riportato un esempio del formato.</td>
  </tr>
 </tbody>
</table>

Esempio: nel browser, una richiesta a `http://localhost:4502/etc/workflow/models.json` genera una risposta JSON simile alla seguente:

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### Gestione di un modello di flusso di lavoro specifico {#managing-a-specific-workflow-model}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502*{uri}*`

Dove `*{uri}*` è il percorso del nodo del modello nell&#39;archivio.

<table>
 <tbody>
  <tr>
   <td>metodo di richiesta HTTP</td>
   <td>Azioni</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Ottiene la versione <code>HEAD</code> del modello (definizione e metadati).</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>Aggiorna la versione <code>HEAD</code> del modello (crea una nuova versione).<br /> La definizione completa del modello per la nuova versione del modello deve essere aggiunta come parametro denominato <code>model</code>. Inoltre, è necessario un parametro <code>type</code> come durante la creazione di nuovi modelli e deve avere il valore <code>JSON</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Stesso comportamento di PUT. Necessario perché i widget AEM non supportano le operazioni <code>PUT</code>.</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>Elimina il modello. Per risolvere i problemi firewall/proxy, una <code>POST</code> contenente una voce di intestazione <code>X-HTTP-Method-Override</code> con valore <code>DELETE</code> verrà accettata anche come richiesta <code>DELETE</code>.</td>
  </tr>
 </tbody>
</table>

Esempio: nel browser, una richiesta a `http://localhost:4502/var/workflow/models/publish_example.json` restituisce una risposta `json` simile al seguente codice:

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData":
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### Gestione di un modello di flusso di lavoro in base alla sua versione {#managing-a-workflow-model-by-its-version}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| metodo di richiesta HTTP | Azioni |
|---|---|
| `GET` | Ottiene i dati del modello nella versione specificata (se esiste). |

### Gestione delle caselle in entrata (degli utenti) {#managing-user-inboxes}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>metodo di richiesta HTTP</td>
   <td>Azioni</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>Elenca gli elementi di lavoro presenti nella casella in entrata dell’utente, identificata dalle intestazioni di autenticazione HTTP.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>Completa l'elemento di lavoro il cui URI viene inviato come parametro <code>item</code> e avanza l'istanza del flusso di lavoro corrispondente ai nodi successivi, definita dal parametro <code>route</code> o <code>backroute</code> se si torna indietro di un passaggio.<br /> Se il parametro <code>delegatee</code> viene inviato, l'elemento di lavoro identificato dal parametro <code>item</code> viene delegato al partecipante specificato.</td>
  </tr>
 </tbody>
</table>

#### Gestione di una casella in entrata (utente) tramite l’ID elemento di lavoro {#managing-a-user-inbox-by-the-workitem-id}

I seguenti metodi di richiesta HTTP si applicano a:

`http://localhost:4502/bin/workflow/inbox/{id}`

| metodo di richiesta HTTP | Azioni |
|---|---|
| `GET` | Ottiene i dati (definizione e metadati) della casella in entrata `WorkItem` identificata dal relativo ID. |

## Esempi {#examples}

### Ottenere un elenco di tutti i flussi di lavoro in esecuzione con i relativi ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

Per ottenere un elenco di tutti i flussi di lavoro in esecuzione, eseguire un&#39;operazione GET per:

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### Come ottenere un elenco di tutti i flussi di lavoro in esecuzione con i relativi ID - REST utilizzando CURL {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

Esempio utilizzando curl:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

Il `uri` visualizzato nei risultati può essere utilizzato come istanza `id` in altri comandi, ad esempio:

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>Questo comando `curl` può essere utilizzato con qualsiasi stato del [flusso di lavoro](/help/sites-administering/workflows.md#workflow-status-and-actions) al posto di `RUNNING`.

### Come modificare il titolo del flusso di lavoro {#how-to-change-the-workflow-title}

Per modificare il **Titolo flusso di lavoro** visualizzato nella scheda **Istanze** della console del flusso di lavoro, invia un comando `POST`:

* a: `http://localhost:4502/etc/workflow/instances/{id}`

* con i seguenti parametri:

   * `action`: il valore deve essere: `UPDATE`
   * `workflowTitle`: titolo del flusso di lavoro

#### Come modificare il Titolo del flusso di lavoro - REST utilizzando CURL {#how-to-change-the-workflow-title-rest-using-curl}

Esempio utilizzando curl:

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### Come elencare tutti i modelli di flussi di lavoro {#how-to-list-all-workflow-models}

Per ottenere un elenco di tutti i modelli di flusso di lavoro disponibili, eseguire una GET per:

`http://localhost:4502/etc/workflow/models.json`

#### Come elencare tutti i modelli di flussi di lavoro - REST utilizzando CURL {#how-to-list-all-workflow-models-rest-using-curl}

Esempio utilizzando curl:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>Vedi anche [Gestione dei modelli di flusso di lavoro](#managing-workflow-models).

### Ottenimento di un oggetto WorkflowSession {#obtaining-a-workflowsession-object}

La classe `com.adobe.granite.workflow.WorkflowSession` è adattabile da un oggetto `javax.jcr.Session` o `org.apache.sling.api.resource.ResourceResolver`.

#### Ottenimento di un oggetto WorkflowSession: Java {#obtaining-a-workflowsession-object-java}

In uno script JSP (o codice Java per una classe servlet), utilizzare l&#39;oggetto richiesta HTTP per ottenere un oggetto `SlingHttpServletRequest`, che fornisce accesso a un oggetto `ResourceResolver`. Adattare l&#39;oggetto `ResourceResolver` a `WorkflowSession`.

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### Ottenimento di un oggetto WorkflowSession: script ECMA {#obtaining-a-workflowsession-object-ecma-script}

Utilizzare la variabile `sling` per ottenere l&#39;oggetto `SlingHttpServletRequest` utilizzato per ottenere un oggetto `ResourceResolver`. Adattare l&#39;oggetto `ResourceResolver` all&#39;oggetto `WorkflowSession`.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### Creazione, lettura o eliminazione di modelli di flussi di lavoro {#creating-reading-or-deleting-workflow-models}

Gli esempi seguenti mostrano come accedere ai modelli di flusso di lavoro:

* Il codice per lo script Java ed ECMA utilizza il metodo `WorkflowSession.createNewModel`.
* Il comando curl accede al modello direttamente dal relativo URL.

Gli esempi utilizzati:

1. Creare un modello (con ID `/var/workflow/models/mymodel/jcr:content/model`).
1. Elimina il modello.

>[!NOTE]
>
>L&#39;eliminazione del modello imposta la proprietà `deleted` del nodo figlio `metaData` del modello su `true`.
>
>L’eliminazione non rimuove il nodo del modello.

Durante la creazione di un modello:

* L&#39;editor modelli di flusso di lavoro richiede che i modelli utilizzino una struttura di nodo specifica sotto `/var/workflow/models`. Il nodo padre del modello deve essere di tipo `cq:Page` con un nodo `jcr:content` con i seguenti valori di proprietà:

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

  Quando si crea un modello, è innanzitutto necessario creare il nodo `cq:Page` e utilizzare il relativo nodo `jcr:content` come nodo principale del nodo del modello.

* L&#39;argomento `id` richiesto da alcuni metodi per identificare il modello è il percorso assoluto del nodo del modello nell&#39;archivio:

  `/var/workflow/models/<*model_name>*/jcr:content/model`

  >[!NOTE]
  >
  >Vedi [Come elencare tutti i modelli di flusso di lavoro](#how-to-list-all-workflow-models).

#### Creazione, lettura o eliminazione di modelli di flussi di lavoro - Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### Creazione, lettura o eliminazione di modelli di flussi di lavoro - Script ECMA {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### Eliminazione di un modello di flusso di lavoro - REST mediante curl {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>A causa del livello di dettaglio richiesto, curl non è considerato pratico per la creazione e/o la lettura di un modello.

### Filtraggio dei flussi di lavoro di sistema durante la verifica dello stato del flusso di lavoro {#filtering-out-system-workflows-when-checking-workflow-status}

È possibile utilizzare l&#39;API [WorkflowStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) per recuperare informazioni sullo stato del flusso di lavoro di un nodo.

Diversi metodi hanno il parametro:

`excludeSystemWorkflows`

Questo parametro può essere impostato su `true` per indicare che i flussi di lavoro di sistema devono essere esclusi dai risultati rilevanti.

[È possibile aggiornare la configurazione OSGi](/help/sites-deploying/configuring-osgi.md) **PayloadMapCache del flusso di lavoro di Adobe Granite** che specifica il flusso di lavoro `Models` da considerare come flussi di lavoro di sistema. I modelli di flusso di lavoro predefiniti (runtime) sono:

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### Avanzamento automatico passaggio partecipante dopo un timeout {#auto-advance-participant-step-after-a-timeout}

Se devi far avanzare automaticamente un passaggio **Partecipante** che non è stato completato entro un tempo predefinito, puoi:

1. Implementa un listener di eventi OSGI per l’ascolto durante la creazione e la modifica delle attività.
1. Specifica un timeout (scadenza), quindi crea un processo sling pianificato da attivare in tale momento.
1. Scrivi un gestore di processi che riceve una notifica alla scadenza del timeout e attiva il processo.

   Questo gestore esegue l&#39;azione richiesta sull&#39;attività se questa non è ancora completata

>[!NOTE]
>
>Per poter utilizzare questo approccio, le azioni da intraprendere devono essere chiaramente definite.

### Interazione con le istanze del flusso di lavoro {#interacting-with-workflow-instances}

Di seguito sono riportati alcuni esempi di base su come interagire (in modo programmatico) con le istanze del flusso di lavoro.

#### Interazione con le istanze del flusso di lavoro - Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interazione con le istanze del flusso di lavoro - Script ECMA {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows("RUNNING");
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### Interazione con le istanze del flusso di lavoro - REST tramite curl {#interacting-with-workflow-instances-rest-using-curl}

* **Avvio di un flusso di lavoro**

  ```shell
  # starting a workflow
  curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
  
  # for example:
  curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
  ```

* **Elenco delle istanze**

  ```shell
  # listing the instances
  curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
  ```

  Elencherà tutte le istanze; ad esempio:

  ```shell
  [
      {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
      ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
  ]
  ```

  >[!NOTE]
  >
  >Consulta [Come ottenere un elenco di tutti i flussi di lavoro in esecuzione](#how-to-get-a-list-of-all-running-workflows-with-their-ids) con i relativi ID per elencare le istanze con uno stato specifico.

* **Sospensione di un flusso di lavoro**

  ```shell
  # suspending a workflow
  curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

* **Ripresa di un flusso di lavoro**

  ```shell
  # resuming a workflow
  curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

* **Chiusura di un&#39;istanza del flusso di lavoro**

  ```shell
  # terminating a workflow
  curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

### Interazione con gli elementi di lavoro {#interacting-with-work-items}

Di seguito sono riportati alcuni esempi di base su come interagire (in modo programmatico) con gli elementi di lavoro.

#### Interazione con gli elementi di lavoro - Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### Interazione con gli elementi di lavoro - Script ECMA {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### Interazione con gli elementi di lavoro - REST mediante curl {#interacting-with-work-items-rest-using-curl}

* **Elencazione di elementi di lavoro dalla cartella Posta in arrivo**

  ```shell
  # listing the work items
  curl -u admin:admin http://localhost:4502/bin/workflow/inbox
  ```

  Verranno elencati i dettagli degli elementi di lavoro attualmente presenti nella casella in entrata, ad esempio:

  ```shell
  [{
      "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
      "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
      "currentAssignee_xss": "workflow-administrators",
      "currentAssignee": "workflow-administrators",
      "startTime": 1519656289274,
      "payloadType_xss": "JCR_PATH",
      "payloadType": "JCR_PATH",
      "payload_xss": "/content/we-retail/es/es",
      "payload": "/content/we-retail/es/es",
      "comment_xss": "Process resource is null",
      "comment": "Process resource is null",
      "type_xss": "WorkItem",
      "type": "WorkItem"
    },{
      "uri_xss": "configuration/configure_analyticstargeting",
      "uri": "configuration/configure_analyticstargeting",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/securitychecklist",
      "uri": "configuration/securitychecklist",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/enable_collectionofanonymoususagedata",
      "uri": "configuration/enable_collectionofanonymoususagedata",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    },{
      "uri_xss": "configuration/configuressl",
      "uri": "configuration/configuressl",
      "currentAssignee_xss": "administrators",
      "currentAssignee": "administrators",
      "type_xss": "Task",
      "type": "Task"
    }
  ```

* **Delega di elementi di lavoro**

  ```xml
  # delegating
  curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
  ```

  >[!NOTE]
  >
  >`delegatee` deve essere un&#39;opzione valida per il passaggio del flusso di lavoro.

* **Completamento o avanzamento degli elementi di lavoro al passaggio successivo**

  ```xml
  # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
  http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
  
  # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
  curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
  ```

### Ascolto degli eventi dei flussi di lavoro {#listening-for-workflow-events}

Utilizzare il framework eventi OSGi per rilevare gli eventi definiti dalla classe [`com.adobe.granite.workflow.event.WorkflowEvent`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html). Questa classe fornisce anche diversi metodi utili per ottenere informazioni sull&#39;oggetto dell&#39;evento. Il metodo `getWorkItem`, ad esempio, restituisce l&#39;oggetto `WorkItem` per l&#39;elemento di lavoro coinvolto nell&#39;evento.

Il codice di esempio seguente definisce un servizio che ascolta gli eventi del flusso di lavoro ed esegue le attività in base al tipo di evento.

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events.
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```
