---
title: Usa xtypes (interfaccia classica)
description: Scopri tutti gli xtype disponibili con Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4a78de53-33bf-4999-ba3c-7d0bc33196a4
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '3668'
ht-degree: 0%

---

# Usa xtypes (interfaccia classica){#using-xtypes-classic-ui}

Questa pagina descrive tutti gli xtype disponibili con Adobe Experience Manager (AEM).

Nel linguaggio ExtJS, xtype è un nome simbolico assegnato a una classe. È possibile leggere il paragrafo &quot;Component XTypes&quot; di [Panoramica di ExtJS 2](https://docs.sencha.com/) per una spiegazione dettagliata su cosa è un xtype e come può essere utilizzato.

Per ulteriori informazioni su tutti i widget disponibili in AEM, consulta la [documentazione API widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

Per individuare i componenti in cui un determinato xtype è utilizzato in AEM, è possibile utilizzare la seguente query `Xpath` in CRXDE. Sostituisci semplicemente &quot;checkbox&quot; con l’XTYPE che ti interessa:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Questa pagina descrive l’utilizzo di xtype ExtJS nell’interfaccia utente classica.
>
>Adobe consiglia di utilizzare la [interfaccia utente touch](/help/sites-developing/touch-ui-concepts.md) standard e moderna basata su [interfaccia utente Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Di seguito sono elencati gli xtype disponibili in Adobe Experience Manager:

* `annotation`

  [CQ.wcm.Annotation](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Annotation` è una finestra speciale. Il corpo contiene una maschera e il piè di pagina contiene un gruppo di pulsanti. In genere viene utilizzato per modificare il contenuto, ma può anche visualizzare solo le informazioni.

* `arraystore`

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Precedentemente noto come `SimpleStore`.

  Una piccola classe helper per semplificare la creazione di [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s da dati array. `ArrayStore` è configurato automaticamente con un [CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `asseteditor`

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Asset Editor` è utilizzato in Amministrazione DAM.

* `assetreferencesearchdialog`

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `AssetReferenceSearchDialog` è una finestra di dialogo che viene visualizzata se una pagina fa riferimento a risorse o tag.

* `blueprintconfig`

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BlueprintConfig` fornisce un pannello per visualizzare le Live Copy di una blueprint e modificarne le proprietà ( attivazione di sincronizzazione e azioni di sincronizzazione ).

* `blueprintstatus`

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BlueprintStatus fornisce un pannello per visualizzare e modificare una blueprint e le relative relazioni Live Copy. La navigazione viene eseguita tramite un [CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), un&#39;edizione tramite un [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e un [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `box`

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe base per qualsiasi [componente](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) che deve essere ridimensionato come una casella, utilizzando la larghezza e l&#39;altezza.

  BoxComponent fornisce regolazioni automatiche del modello di box per il dimensionamento e il posizionamento e funziona correttamente all&#39;interno del modello di rendering del componente.

* `browsedialog`

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La finestra di dialogo Sfoglia consente all&#39;utente di sfogliare il repository per selezionare un percorso. In genere viene utilizzato tramite un [BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `browsefield`

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: usa [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) invece**

* `bulkeditor`

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BulkEditor` fornisce un motore di ricerca e una griglia per modificare i risultati della ricerca.

  È necessario inserire `BulkEditor` in un modulo HTML (richiesto dalla funzionalità di importazione). Questo funziona perfettamente con un [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `bulkeditorform`

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BulkEditorForm fornisce [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) circondato da un modulo di HTML. Versione autonoma di [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Per il pulsante Importa è necessario un modulo di HTML.

* `button`

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe Simple Button

* `buttongroup`

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenitore per un gruppo di pulsanti.

* `chart`

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Il pacchetto CQ.Ext.chart fornisce la possibilità di visualizzare i dati con grafici basati su flash. Ogni grafico si associa direttamente a un CQ.Ext.data.Store abilitando gli aggiornamenti automatici del grafico. Per modificare l&#39;aspetto di un grafico, vedere le opzioni di configurazione [chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e [extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `checkbox`

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo casella di controllo singola. Può essere utilizzata come sostituzione diretta dei campi delle caselle di controllo tradizionali.

* `checkboxgroup`

  [CQ.Ext.form.CheckboxGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenitore di raggruppamento per i controlli [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `clearcombo`

  [CQ.form.ClearableComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ClearableComboBox è una casella combinata non modificabile con un trigger che ne cancella il valore.

* `colorfield`

  [CQ.form.ColorField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorField consente all&#39;utente di immettere un valore esadecimale colore direttamente o utilizzando un [CQ.Ext.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `colorlist`

  [CQ.form.ColorList](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorList consente all&#39;utente di scegliere un colore da un elenco modificabile.

* `colormenu`

  [CQ.Ext.menu.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un menu contenente un componente [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `colorpalette`

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe semplice della tavolozza dei colori per la scelta dei colori. È possibile eseguire il rendering della palette in qualsiasi contenitore.

* `combo`

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un controllo casella combinata con supporto per il completamento automatico, il caricamento remoto, il paging e molte altre funzioni.

  Un controllo ComboBox funziona in modo simile a un campo &lt;select> HTML tradizionale. La differenza sta nel fatto che per inviare il [valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), è necessario specificare un [hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per creare un input nascosto.

* `component`

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe base per tutti i componenti `Ext`. Tutte le sottoclassi di Component possono partecipare al ciclo di vita automatizzato del componente `Ext` di creazione, rendering e distruzione fornito dalla classe [Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). I componenti possono essere aggiunti a un contenitore tramite l&#39;opzione di configurazione [items](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) al momento della creazione del contenitore.

* `componentextractor`

  [CQ.wcm.ComponentExtractor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ComponentExtractor consente all&#39;utente di estrarre componenti da un sito Web o da una pagina.

* `componentselector`

  [CQ.form.ComponentSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una selezione raggruppata e ordinata dei Componenti disponibili.

* `componentstyles`

  [CQ.form.ComponentStyles](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `compositefield`

  [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe base per campi modulo complessi basati su pannello che includono un campo modulo o un gruppo di campi modulo.

* `container`

  [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe base per qualsiasi [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) che può contenere altri componenti. I contenitori gestiscono il comportamento di base degli elementi contenenti, ovvero l&#39;aggiunta, l&#39;inserimento e la rimozione di elementi.

  Le classi contenitore più comunemente utilizzate sono [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `contentfinder`

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinder è un [viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) specializzato a due colonne che contiene il Content Finder effettivo a sinistra e il Content Frame a destra.

* `contentfindertab`

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinderTab è un pannello specializzato che fornisce funzionalità utilizzate nei pannelli delle schede di [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). In genere sono disponibili un modulo di ricerca, ovvero la Casella di query, e una visualizzazione dati per visualizzare la ricerca.

* `cq.workflow.model.combo`

  [CQ.wcm.WorkflowModelCombo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelCombo è un [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) personalizzato che mostra un elenco di modelli di flusso di lavoro disponibili.

* `cq.workflow.model.selector`

  [CQ.wcm.WorkflowModelSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelSelector combina WorkflowModelCombo con un&#39;immagine in miniatura del flusso di lavoro e i pulsanti per creare e modificare modelli di flusso di lavoro.

* `createsitewizard`

  [CQ.wcm.CreateSiteWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateSiteWizard è una procedura guidata dettagliata per la creazione di siti (MSM).

* `createversiondialog`

  [CQ.wcm.CreateVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateVersionDialog è una finestra di dialogo che consente di creare una versione di una pagina.

* `customcontentpanel`

  [CQ.CustomContentPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CustomContentPanel è un pannello speciale da utilizzare in [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html): il suo contenuto viene recuperato da un URL diverso rispetto agli altri campi della finestra di dialogo.

* `cycle`

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SplitButton specializzato contenente un menu di [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) elementi. Il pulsante scorre automaticamente ogni voce di menu a ogni clic, generando l&#39;evento [change](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) del pulsante (o richiamando la funzione [changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) del pulsante, se fornita) per la voce di menu attiva.

* `dataview`

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un meccanismo per visualizzare i dati utilizzando modelli di layout e formattazione personalizzati. DataView utilizza un [CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) come meccanismo di modelli interno ed è associato a un [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) in modo che, quando i dati nell&#39;archivio cambiano, la visualizzazione venga automaticamente aggiornata per riflettere le modifiche.

* `datefield`

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Fornisce un campo di input della data con un elenco a discesa [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e una convalida automatica della data.

* `datemenu`

  [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un menu contenente un componente [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `datepicker`

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un selettore di data popup. Questa classe viene utilizzata dalla classe [DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per consentire l&#39;esplorazione e la selezione di date valide.

* `datetime`

  [CQ.form.DateTime](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DateTime consente all&#39;utente di immettere una data e un&#39;ora combinando [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `dialog`

  [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La finestra di dialogo è una finestra speciale. Il corpo contiene una maschera e il piè di pagina contiene un gruppo di pulsanti. In genere viene utilizzato per modificare il contenuto, ma può anche visualizzare solo le informazioni.

* `dialogfieldset`

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DialogFieldSet è un [FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) da utilizzare in [Dialogs](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `directstore`

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una piccola classe helper per creare un [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) configurato con un [CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e un [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per semplificare l&#39;interazione con un [CQ.Ext.Direct](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) lato server [Provider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `displayfield`

  [CQ.Ext.form.DisplayField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo di testo di sola visualizzazione non convalidato e non inviato.

* `editbar`

  [CQ.wcm.EditBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La barra di modifica consente all&#39;utente di modificare il contenuto utilizzando i pulsanti di una barra.

  Sebbene non sia elencato qui, EditBar ha tutti i membri di [CQ.wcm.EditBase](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `editor`

  [CQ.Ext.Editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo dell’editor di base che gestisce la visualizzazione o l’hiding on-demand e che dispone di alcune logiche integrate di dimensionamento e gestione degli eventi.

* `editorgrid`

  [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Questa classe estende la [classe GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per fornire la modifica delle celle nelle [colonne](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) selezionate. Le colonne modificabili vengono specificate fornendo un [editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) nella [configurazione colonna](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `editrollover`

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  L’oggetto EditRollover consente all’utente di modificare il contenuto con un doppio clic e fornisce ulteriori azioni di modifica tramite un menu di scelta rapida. L&#39;area modificabile viene indicata da una cornice quando si passa il mouse sul contenuto.

* `feedimporter`

  [CQ.wcm.FeedImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La funzione FeedImporter consente all&#39;utente di importare feed RSS o Atom e di creare pagine per ogni voce di feed.

* `field`

  [CQ.Ext.form.Field](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe di base per i campi modulo che fornisce la gestione degli eventi, il dimensionamento, la gestione dei valori e altre funzionalità predefinite.

* `fieldset`

  [CQ.Ext.form.FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenitore standard utilizzato per raggruppare elementi in un [modulo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `fileuploaddialogbutton`

  [CQ.form.FileUploadDialogButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadDialogButton crea un pulsante che apre una nuova finestra di dialogo per il caricamento di un file tramite FileUploadField. Può essere utilizzato all&#39;interno di finestre di dialogo di modifica in cui il caricamento deve avvenire in un modulo separato.

* `fileuploadfield`

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadField consente all’utente di selezionare un singolo file da caricare.

* `findreplacedialog`

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FindReplaceDialog è una finestra di dialogo per la ricerca e la sostituzione di token in una pagina e nelle relative pagine figlie.

* `flash`

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `grid`

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Questa classe rappresenta l&#39;interfaccia principale di un controllo griglia basato su componenti per rappresentare i dati in un formato tabulare di righe e colonne.

* `groupingstore`

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Implementazione di un negozio specializzato che consente di raggruppare i record in base a uno dei campi disponibili. Utilizzato con un [CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per dimostrare il modello dati per un GridPanel raggruppato.

* `heavymovedialog`

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HeavyMoveDialog è una finestra di dialogo per lo spostamento di una pagina e delle relative pagine figlie, che prende in considerazione anche la riattivazione di pagine attivate in precedenza (spostamento &quot;pesante&quot;).

* `hidden`

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo nascosto di base per la memorizzazione di valori nascosti nei moduli che devono essere passati nell’invio del modulo.

* `historybutton`

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HistoryButton è una piccola classe helper che fornisce pulsanti avanti e indietro in modo semplice. Di solito sono necessarie due istanze correlate: l’istanza del pulsante Avanti è un semplice pulsante collegato all’istanza del pulsante Indietro che gestisce la cronologia.

* `htmleditor`

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Offre un componente leggero HTML Editor. Poiché Safari non supporta alcune funzioni della barra degli strumenti, il sistema le nasconde automaticamente quando necessario. Nelle opzioni di configurazione, se necessario.

  I pulsanti della barra degli strumenti dell&#39;editor contengono descrizioni nella proprietà [buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `iframedialog`

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una finestra di dialogo semplice che mostra il contenuto di un iframe e consente l’utilizzo di moduli negli iframe.

* `iframepanel`

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Pannello contenente un iframe. Consente di creare facilmente gli iframe, un evento di caricamento iframe e un facile accesso ai contenuti dell’iframe.

* `inlinetextfield`

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  InlineField è un campo di testo che viene visualizzato come etichetta quando non è attivo.

* `jsonstore`

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una piccola classe helper per semplificare la creazione di [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) da dati JSON. Un JsonStore viene configurato automaticamente con un [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `label`

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo etichetta di base.

* `languagecopydialog`

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LanguageCopyDialog è una finestra di dialogo per la copia degli alberi del linguaggio.

* `linkchecker`

  [CQ.wcm.LinkChecker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LinkChecker è uno strumento che consente di controllare i collegamenti esterni in un sito.

* `listview`

  [CQ.Ext.list.ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.list.ListView è un&#39;implementazione rapida e leggera di una visualizzazione [simile a una griglia](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `livecopyproperties`

  [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LiveCopyProperties fornisce un pannello per visualizzare e modificare le proprietà Live Copy ( ereditarietà delle relazioni, trigger di sincronizzazione e azioni di sincronizzazione ).

* `lvbooleancolumn`

  [CQ.Ext.list.BooleanColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe di definizione della colonna che esegue il rendering dei campi dati booleani. Per ulteriori dettagli, vedi l&#39;opzione di configurazione [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) di [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `lvcolumn`

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Questa classe incapsula i dati di configurazione delle colonne da utilizzare nell&#39;inizializzazione di un [ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `lvdatecolumn`

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe Column definition che esegue il rendering di una data passata in base alle impostazioni locali predefinite o a un [formato](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) configurato. Per ulteriori dettagli, vedi l&#39;opzione di configurazione [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) di [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `lvnumbercolumn`

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe di definizione della colonna che esegue il rendering di un campo dati numerico in base a una stringa [format](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Per ulteriori dettagli, vedi l&#39;opzione di configurazione [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) di [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `mediabrowsedialog`

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: utilizza [Content Finder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per sfogliare i file multimediali.**

  MediaBrowseDialog è una finestra di dialogo che consente di esplorare il Catalogo multimediale.

* `menu`

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un oggetto menu. Contenitore a cui è possibile aggiungere voci di menu. Il menu può anche fungere da classe base quando si desidera un menu specializzato basato su un altro componente, ad esempio [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

  I menu possono contenere [voci di menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o [componenti](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) generali.

* `menubaseitem`

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe di base per tutti gli elementi che vengono visualizzati nei menu. BaseItem fornisce il rendering predefinito, la gestione dello stato attivato e le opzioni di configurazione di base condivise da tutti i componenti del menu.

* `menucheckitem`

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Aggiunge una voce di menu che contiene una casella di controllo per impostazione predefinita, ma che può anche far parte di un gruppo di opzioni.

* `menuitem`

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe di base per tutte le voci di menu che richiedono funzionalità relative ai menu (come i sottomenu) e non sono elementi di visualizzazione statici. Item estende la funzionalità di base di [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) aggiungendo l&#39;attivazione specifica del menu e la gestione dei clic.

* `menuseparator`

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Aggiunge una barra di separazione a un menu, utilizzata per dividere gruppi logici di voci di menu. In genere, puoi aggiungerne uno utilizzando &quot;-&quot; nella chiamata ad add() o nella configurazione degli elementi, anziché crearne uno direttamente.

* `menutextitem`

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Aggiunge una stringa di testo statica a un menu, utilizzata come separatore di intestazione o di gruppo.

* `metadata`

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Metadata` fornisce un set di campi per determinare le informazioni necessarie per un campo di metadati utilizzato, ad esempio, nelle pagine dell&#39;Editor risorse.

  Fornisce i seguenti campi:

* `multifield`

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `MultiField` è un elenco modificabile di campi modulo per la modifica di proprietà con più valori.

* `mvt`

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Il componente Multivariate Testing può essere utilizzato per definire e modificare un set di immagini presentate come banner alternati. Le statistiche sui tassi di click-through vengono raccolte per banner.

* `notificationinbox`

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `NotificationInbox` consente all&#39;utente di sottoscrivere azioni WCM e gestire le notifiche.

* `numberfield`

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo di testo numerico che fornisce il filtro automatico della sequenza di tasti e la convalida numerica.

* `offlineimporter`

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OfflineImporter` è uno strumento per importare e convertire documenti di Microsoft® Word in pagine di AEM. Questa funzione consente di modificare il contenuto offline utilizzando un elaboratore di testi.

* `ownerdraw`

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OwnerDraw` può contenere codice HTML personalizzato (immesso direttamente o recuperato da un URL).

* `paging`

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Con l’aumento del numero di record, aumenta il tempo necessario al browser per eseguirne il rendering. Il paging viene utilizzato per ridurre la quantità di dati scambiati con il client.

* `panel`

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `panel` è un contenitore con funzionalità e componenti strutturali specifici che lo rendono il perfetto elemento di base per le interfacce utente orientate alle applicazioni.

  I pannelli, in virtù della loro ereditarietà, provengono da [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `paragraphreference`

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Il campo Riferimento paragrafo consente di sfogliare le pagine e selezionare uno dei relativi paragrafi. È costituito da un campo trigger e da una finestra di dialogo associata per l&#39;esplorazione dei paragrafi.

* `password`

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Password` è simile a un [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ma mantiene il valore privato, consentendo agli utenti di immettere dati sensibili.

* `pathcompletion`

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: usa [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) invece**

* `pathfield`

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PathField` è un campo di input progettato per i percorsi con completamento del percorso e un pulsante per aprire un [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per la navigazione nell&#39;archivio del server. Può anche sfogliare i paragrafi di pagina per la generazione avanzata di collegamenti.

* `progress`

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Componente barra di avanzamento aggiornabile. La barra di avanzamento supporta due diverse modalità: manuale e automatica.

  In modalità manuale, sei responsabile della visualizzazione, dell&#39;aggiornamento (tramite [updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)) e della cancellazione della barra di avanzamento in base alle esigenze dal tuo codice. Questo metodo è più appropriato quando si desidera visualizzare l’avanzamento.

* `propertygrid`

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Implementazione di una griglia specializzata progettata per simulare la griglia di proprietà tradizionale, come generalmente si vede negli IDE di sviluppo. Ogni riga della griglia rappresenta una proprietà di un oggetto e i dati vengono memorizzati come set di coppie nome/valore in [CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) s.

* `propgrid`

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PropertyGrid` è una griglia generica utilizzata per visualizzare e modificare le proprietà degli oggetti.

* `quicktip`

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `@xtype quicktip` - Classe di descrizioni comandi specializzata per le descrizioni comandi che può essere specificata nel markup e gestita automaticamente dall&#39;istanza globale [CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Per ulteriori dettagli ed esempi sull&#39;utilizzo, vedere l&#39;intestazione della classe QuickTips.

* `radio`

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo `radio` singolo. Uguale a Casella di controllo, ma viene fornito per comodità per impostare automaticamente il tipo di input. Il browser raggruppa automaticamente i pulsanti di scelta quando ogni pulsante di scelta del gruppo utilizza lo stesso nome.


* `radiogroup`

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenitore di raggruppamento per i controlli [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `referencesdialog`

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `ReferencesDialog` è una finestra di dialogo per la visualizzazione dei riferimenti in una pagina.

* `restoretreedialog`

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RestoreTreeDialog` è una finestra di dialogo per il ripristino di una versione precedente di una struttura.

* `restoreversiondialog`

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RestoreVersionDialog è una finestra di dialogo per il ripristino di una versione precedente di una pagina.

* `richtext`

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RichText` fornisce un campo modulo per la modifica di informazioni di testo formattato (testo RTF).

  Il componente `RichText` fornisce attualmente le seguenti funzionalità:

* `rolloutplan`

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Il RolloutPlan fornisce una finestra di dialogo per controllare lo stato di rollout di una pagina. Un [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) avvia il RolloutPlan.

* `rolloutwizard`

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RolloutWizard` fornisce una procedura guidata per il rollout di una pagina. RolloutWizard avvia un [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `searchfield`

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SearchField` fornisce un campo di ricerca che fornisce i risultati in un elenco a discesa che può essere utilizzato per la ricerca nel repository.

* `selection`

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Selection` consente all&#39;utente di scegliere tra diverse opzioni. Le opzioni possono far parte della configurazione o essere caricate da una risposta JSON. È possibile eseguire il rendering della selezione come elenco a discesa (selezione) o in una casella combinata (selezione più immissione testo libero).

* `sidekick`

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Sidekick` è un helper mobile che fornisce all&#39;utente strumenti comuni per la modifica delle pagine.

* `siteadmin`

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteAdmin` è una console che fornisce funzioni di amministrazione di WCM.

* `siteimporter`

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteImporter` consente all&#39;utente di importare siti Web completi e creare progetti iniziali.

* `sizefield`

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SizeField` consente all&#39;utente di immettere la larghezza e l&#39;altezza (ad esempio, per un&#39;immagine).

* `slider`

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Dispositivo di scorrimento che supporta l&#39;orientamento verticale o orizzontale, le regolazioni della tastiera, lo snap configurabile, il clic sull&#39;asse e l&#39;animazione. Può essere aggiunto come elemento a qualsiasi contenitore. Ad esempio, utilizzo: ...

* `slideshow`

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Il componente Presentazione consente di definire e modificare un set di immagini e titoli delle immagini. Gli utenti possono visualizzare il set come una presentazione.

  Il componente Presentazione è basato sul componente [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `smartfile`

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartFile è un caricatore di file intelligente.

  Se è installato un plug-in Flash (versione >= 9), i caricamenti vengono eseguiti utilizzando la libreria SWFupload che offre un modo pratico per gestire i caricamenti.

* `smartimage`

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartImage è un caricatore di immagini intelligente. Fornisce strumenti per elaborare un’immagine caricata, ad esempio uno strumento per definire le mappe immagine e un ritaglio immagine.

  Il componente è progettato per essere utilizzato in una scheda della finestra di dialogo separata.

* `spacer`

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Utilizzato per fornire uno spazio considerevole in un layout.

* `spinner`

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Spinner` è un campo trigger per valori numerici, di data o di ora. Il valore può essere aumentato e diminuito utilizzando i trigger su e giù forniti, la rotellina di scorrimento o i tasti.

* `splitbutton`

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `splitbutton` che fornisce una freccia a discesa incorporata che può attivare un evento separatamente dall&#39;evento clic predefinito del pulsante. In genere viene utilizzato per visualizzare un menu a discesa che fornisce opzioni aggiuntive all&#39;azione pulsante principale, ma qualsiasi gestore personalizzato può fornire l&#39;implementazione `arrowclick`.

* `static`

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Static` può essere utilizzato per visualizzare testo arbitrario o HTML.

* `statistics`

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Statistics` visualizza le impression della pagina come grafico. Il widget consente di selezionare un periodo per il quale visualizzare le statistiche.

* `store`

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  La classe `Store` incapsula una cache lato client di oggetti [Record](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) che forniscono dati di input per componenti quali [GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), [ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o [DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `suggestfield`

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SuggestField` fornisce all&#39;utente suggerimenti in base alla voce.

* `switcher`

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Switcher` fornisce un gruppo di pulsanti per la barra dell&#39;intestazione in una console per passare da Siti Web, Assets digitale, Strumenti, Flusso di lavoro e Sicurezza.

* `tableedit`

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **Obsoleto: utilizzare [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).**

* `tableedit2`

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TableEdit2` fornisce un widget per creare tabelle.

* `tabpanel`

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenitore di schede di base. I TabPanels possono essere utilizzati esattamente come un [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) standard a scopo di layout, ma dispongono anche di un supporto speciale per contenere i componenti figlio ([`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)).

* `tags`

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ```
  CQ.tagging.TagInputField
  ```

  è un widget di modulo per l’immissione di tag. Dispone di un menu a comparsa per selezionare da tag esistenti, include il completamento automatico e molte altre funzioni.

* `textarea`

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo di testo a più righe. Può essere utilizzato come sostituzione diretta dei tradizionali campi `textarea` e aggiunge il supporto per il ridimensionamento automatico.

* `textbutton`

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TextButton` fornisce un collegamento di testo con le funzionalità di un [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `textfield`

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Campo di testo di base. Può essere utilizzata come sostituzione diretta degli input di testo tradizionali o come classe base per controlli di input più sofisticati (come [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)).

* `thumbnail`

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `timefield`

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Fornisce un campo di immissione tempo con un elenco a discesa dell’ora e una convalida automatica dell’ora. Esempio: ...

* `tip`

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Suggerimento @xtype Classe base per [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e [CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) che fornisce il layout e il posizionamento di base necessari per tutte le classi basate su suggerimenti. Questa classe può essere utilizzata direttamente per semplici suggerimenti statici.

* `titleseparator`

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Aggiunge una barra di separazione a un menu, utilizzata per dividere gruppi logici di voci di menu. Il separatore può anche contenere un titolo.

* `toolbar`

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Classe `Toolbar` di base. Sebbene [`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per la barra degli strumenti sia [`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html), gli elementi della barra degli strumenti (elementi figlio per il contenitore della barra degli strumenti) possono essere virtualmente qualsiasi tipo di componente. Gli elementi della barra degli strumenti possono essere creati esplicitamente tramite i rispettivi costruttori.

* `tooltip`

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Un&#39;implementazione `tooltip` standard per fornire informazioni aggiuntive quando si passa il mouse su un elemento di destinazione. Descrizione comando @xtype.

* `treegrid`

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype `treegrid`

* `treepanel`

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TreePanel` fornisce una rappresentazione dell&#39;interfaccia utente con struttura ad albero dei dati con struttura ad albero.

  [TreeNode](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) aggiunti a `TreePanel` possono contenere metadati utilizzati dall&#39;applicazione nella proprietà [attributes](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

* `trigger`

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Fornisce un comodo wrapper per `TextFields` che aggiunge un pulsante di attivazione cliccabile (sembra una casella combinata per impostazione predefinita). Il trigger non ha un&#39;azione predefinita, pertanto devi assegnare una funzione per implementare il gestore di clic del trigger ignorando [onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Puoi creare direttamente `TriggerField`, poiché esegue il rendering esattamente come una casella combinata.

* `uploaddialog`

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `UploadDialog` consente all&#39;utente di caricare i file nel repository Crea un nuovo UploadDialog.

* `userinfo`

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Elemento della barra degli strumenti per visualizzare il nome utente corrente e consentire azioni dell’utente come la modifica delle proprietà e della rappresentazione dell’utente.

* `viewport`

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Contenitore specifico che rappresenta l’area di applicazione visualizzabile (il riquadro di visualizzazione del browser).

  `Viewport` si riproduce nel corpo del documento, si ridimensiona automaticamente alle dimensioni del riquadro di visualizzazione del browser e gestisce il ridimensionamento delle finestre. È possibile creare un solo riquadro di visualizzazione.

* `window`

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Pannello specializzato destinato a essere utilizzato come finestra di applicazione. Per impostazione predefinita, Windows è mobile, [ridimensionabile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) e [trascinabile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html). Windows può essere [ingrandito](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) per riempire il riquadro di visualizzazione, ripristinato alle dimensioni precedenti e può essere [ridotto a icona](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)d.

* `xmlstore`

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  Una piccola classe helper per semplificare la creazione di [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s da dati XML. `XmlStore` è configurato automaticamente con un [CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html).

  `cqinclude`: pseudo xtype che include definizioni di widget da un percorso diverso nell&#39;archivio. Viene utilizzato in genere nelle finestre di dialogo delle pagine. Non esiste alcuna classe widget JavaScript effettiva per questo xtype. La classe `CQ.Util` la elabora utilizzando la funzione `formatData()`.
