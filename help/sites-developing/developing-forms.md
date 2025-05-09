---
title: Sviluppo di Forms (interfaccia classica)
description: Scopri come sviluppare moduli per l’interfaccia classica di Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: d1475168-6625-4d27-9c3b-01e415c2f398
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---

# Sviluppo di Forms (interfaccia classica){#developing-forms-classic-ui}

La struttura di base di un modulo è la seguente:

* Inizio modulo
* Elementi modulo
* Fine modulo

Tutti questi elementi vengono realizzati con una serie di [componenti modulo](/help/sites-authoring/default-components.md#form) predefiniti, disponibili in un&#39;installazione standard di AEM.

Oltre a [sviluppare nuovi componenti](/help/sites-developing/developing-components-samples.md) da utilizzare nei moduli, è possibile:

* [Precarica il modulo con i valori](#preloading-form-values)
* [Precarica (determinati) campi con più valori](#preloading-form-fields-with-multiple-values)
* [Sviluppare nuove azioni](#developing-your-own-form-actions)
* [Sviluppare nuovi vincoli](#developing-your-own-form-constraints)
* [Mostrare o nascondere campi modulo specifici](#showing-and-hiding-form-components)

[Utilizzo di script](#developing-scripts-for-use-with-forms) per estendere le funzionalità laddove necessario.

>[!NOTE]
>
>Questo documento si concentra sullo sviluppo di moduli utilizzando [Componenti Foundation](/help/sites-authoring/default-components-foundation.md) nell&#39;interfaccia utente classica. Adobe consiglia di utilizzare i nuovi [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Nascondi condizioni](/help/sites-developing/hide-conditions.md) per lo sviluppo di moduli nell&#39;interfaccia utente touch.

## Precaricamento dei valori modulo {#preloading-form-values}

Il componente di inizio modulo fornisce un campo per il **percorso di caricamento**, un percorso facoltativo che punta a un nodo nell&#39;archivio.

Il percorso di caricamento è il percorso delle proprietà del nodo utilizzato per caricare valori predefiniti in più campi del modulo.

Questo è un campo facoltativo che specifica il percorso di un nodo nell’archivio. Se le proprietà di questo nodo corrispondono ai nomi dei campi, i campi appropriati del modulo vengono precaricati con il valore di tali proprietà. Se non esiste alcuna corrispondenza, il campo contiene il valore predefinito.

>[!NOTE]
>
>Un&#39;azione [modulo](#developing-your-own-form-actions) può anche impostare la risorsa da cui caricare i valori iniziali. Questa operazione viene eseguita utilizzando `FormsHelper#setFormLoadResource` in `init.jsp`.
>
>Solo se non è impostato, il modulo verrà popolato dal percorso impostato nel componente modulo iniziale dall’autore.

### Precaricamento dei campi modulo con più valori {#preloading-form-fields-with-multiple-values}

Vari campi modulo hanno anche il percorso di caricamento **Elementi**, di nuovo un percorso facoltativo che punta a un nodo nell&#39;archivio.

Il percorso di caricamento **Elementi** è il percorso delle proprietà del nodo utilizzato per caricare valori predefiniti in quel campo specifico del modulo, ad esempio un [elenco a discesa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [gruppo di caselle di controllo](/help/sites-authoring/default-components-foundation.md#checkbox-group) o [gruppo di caselle di controllo](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Esempio: precaricamento di un elenco a discesa con più valori {#example-preloading-a-dropdown-list-with-multiple-values}

È possibile configurare un elenco a discesa con l’intervallo di valori desiderato.

Il percorso di caricamento **Elementi** può essere utilizzato per accedere a un elenco da una cartella nel repository e precaricarli nel campo:

1. Crea una cartella Sling ( `sling:Folder`)
ad esempio, `/etc/designs/<myDesign>/formlistvalues`

1. Aggiungere una nuova proprietà (ad esempio, `myList`) di tipo stringa con più valori ( `String[]`) per contenere l&#39;elenco di elementi a discesa. Il contenuto può essere importato anche utilizzando uno script, ad esempio con uno script JSP o cURL in uno script shell.

1. Utilizza il percorso completo nel campo **Percorso di caricamento elementi**:
ad esempio, `/etc/designs/geometrixx/formlistvalues/myList`

Nota che se i valori in `String[]` sono del formato seguente:

* `AL=Alabama`
* `AK=Alaska`

e così via, AEM genera l’elenco come:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Questa funzione può, ad esempio, essere utilizzata in un ambiente multilingue.

### Sviluppo di azioni personalizzate per i moduli {#developing-your-own-form-actions}

Un modulo richiede un&#39;azione. Un&#39;azione definisce l&#39;operazione eseguita quando il modulo viene inviato con i dati utente.

Con un’installazione standard di AEM è disponibile una serie di azioni, descritte in:

`/libs/foundation/components/form/actions`

e nell&#39;elenco **Tipo azione** del componente **Modulo**:

![chlimage_1-8](assets/chlimage_1-8.png)

In questa sezione viene illustrato come sviluppare un&#39;azione modulo personalizzata da includere nell&#39;elenco.

Puoi aggiungere la tua azione in `/apps` come segue:

1. Creare un nodo di tipo `sling:Folder`. Specifica un nome che rifletta l’azione da implementare.

   Ad esempio:

   `/apps/myProject/components/customFormAction`

1. In questo nodo definisci le seguenti proprietà, quindi fai clic su **Salva tutto** per mantenere le modifiche:

   * `sling:resourceType` - impostato come `foundation/components/form/action`

   * `componentGroup` - definisci come `.hidden`

   * Facoltativamente:

      * `jcr:title` - specifica un titolo desiderato da visualizzare nell&#39;elenco a discesa. Se non è impostato, viene visualizzato il nome del nodo

      * `jcr:description` - immetti una descrizione a tua scelta

1. Nella cartella crea un nodo di dialogo:

   1. Aggiungi i campi in modo che l’autore possa modificare la finestra di dialogo dei moduli una volta scelta l’azione.

1. Nella cartella crea:

   1. Uno script post.
Il nome dello script è `post.POST.<extension>`, ad esempio `post.POST.jsp`
Lo script post viene richiamato quando un modulo viene inviato per elaborare il modulo, contiene il codice che gestisce i dati provenienti dal modulo `POST`.

   1. Aggiungi uno script di inoltro che viene richiamato al momento dell’invio del modulo.
Il nome dello script è `forward.<extension`>, ad esempio `forward.jsp`
Questo script può definire un percorso. La richiesta corrente viene quindi inoltrata al percorso specificato.

   La chiamata necessaria è `FormsHelper#setForwardPath` (2 varianti). Un caso tipico è quello di eseguire una convalida, o logica, per trovare il percorso di destinazione e quindi inoltrarlo a tale percorso, consentendo al servlet Sling POST predefinito di eseguire l’archiviazione effettiva in JCR.

   Potrebbe esserci anche un altro servlet che esegue l&#39;elaborazione effettiva, in tal caso l&#39;azione del modulo e `forward.jsp` fungerebbero solo da codice &quot;glue&quot;. Un esempio è l&#39;azione di posta in `/libs/foundation/components/form/actions/mail`, che inoltra i dettagli a `<currentpath>.mail.html` dove si trova un servlet di posta.

   Quindi:

   * un `post.POST.jsp` è utile per piccole operazioni che sono completamente eseguite dall&#39;azione stessa
   * mentre `forward.jsp` è utile quando è richiesta solo la delega.

   L’ordine di esecuzione per gli script è:

   * Al rendering del modulo ( `GET`):

      1. `init.jsp`
      1. per tutti i vincoli del campo: `clientvalidation.jsp`
      1. validationRT del modulo: `clientvalidation.jsp`
      1. il modulo viene caricato tramite la risorsa di caricamento se impostata
      1. `addfields.jsp` durante il rendering di `<form></form>`

   * durante la gestione di un modulo `POST`:

      1. `init.jsp`
      1. per tutti i vincoli del campo: `servervalidation.jsp`
      1. validationRT del modulo: `servervalidation.jsp`
      1. `forward.jsp`
      1. se è stato impostato un percorso di inoltro ( `FormsHelper.setForwardPath`), inoltrare la richiesta, quindi chiamare `cleanup.jsp`

      1. se non è stato impostato alcun percorso di inoltro, chiamare `post.POST.jsp` (termina qui, non è stato chiamato `cleanup.jsp`)

1. Sempre nella cartella, se lo desideri, aggiungi:

   1. Script per l’aggiunta di campi.
Il nome dello script è `addfields.<extension>`, ad esempio `addfields.jsp`
Uno script `addfields` viene richiamato immediatamente dopo la scrittura del HTML per l&#39;avvio del modulo. Questo consente all’azione di aggiungere campi di input personalizzati o altri HTML all’interno del modulo.

   1. Uno script di inizializzazione.
Il nome dello script è `init.<extension>`, ad esempio `init.jsp`
Questo script viene richiamato al momento del rendering del modulo. Può essere utilizzato per inizializzare le specifiche dell’azione.

   1. Uno script di pulizia.
Il nome dello script è `cleanup.<extension>`, ad esempio `cleanup.jsp`
Questo script può essere utilizzato per eseguire la pulizia.

1. Utilizza il componente **Forms** in un parsys. Il menu a discesa **Tipo azione** includerà ora la nuova azione.

   >[!NOTE]
   >
   >Per visualizzare le azioni predefinite che fanno parte del prodotto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Sviluppo di vincoli di modulo personalizzati {#developing-your-own-form-constraints}

I vincoli possono essere imposti a due livelli:

* Per [singoli campi (vedere la procedura seguente)](#constraints-for-individual-fields)
* Come [convalida globale modulo](#form-global-constraints)

#### Vincoli per singoli campi {#constraints-for-individual-fields}

È possibile aggiungere vincoli personalizzati per un singolo campo (in `/apps`) come segue:

1. Creare un nodo di tipo `sling:Folder`. Specificare un nome che rifletta il vincolo da implementare.

   Ad esempio:

   `/apps/myProject/components/customFormConstraint`

1. In questo nodo definisci le seguenti proprietà, quindi fai clic su **Salva tutto** per mantenere le modifiche:

   * `sling:resourceType` - impostato su `foundation/components/form/constraint`

   * `constraintMessage` - messaggio personalizzato visualizzato se il campo non è valido, in base al vincolo, al momento dell&#39;invio del modulo

   * Facoltativamente:

      * `jcr:title` - specifica un titolo desiderato da visualizzare nell&#39;elenco di selezione. Se non è impostato, viene visualizzato il nome del nodo
      * `hint` - ulteriori informazioni per l&#39;utente su come utilizzare il campo

1. All&#39;interno di questa cartella, possono essere necessari i seguenti script:

   * Uno script di convalida client:
Il nome dello script è `clientvalidation.<extension>`, ad esempio `clientvalidation.jsp`
Viene richiamato quando viene eseguito il rendering del campo modulo. Può essere utilizzato per creare JavaScript client per convalidare il campo sul client.

   * Uno script di convalida del server:
Il nome dello script è `servervalidation.<extension>`, ad esempio `servervalidation.jsp`
Viene richiamato al momento dell’invio del modulo. Può essere utilizzato per convalidare il campo sul server dopo l’invio.

>[!NOTE]
>
>I vincoli di esempio sono disponibili in:
>
>`/libs/foundation/components/form/constraints`

#### Vincoli globali del modulo {#form-global-constraints}

La convalida globale del modulo viene specificata configurando un tipo di risorsa nel componente modulo iniziale ( `validationRT`). Ad esempio:

`apps/myProject/components/form/validation`

Puoi quindi definire:

* a `clientvalidation.jsp` - inserito dopo gli script di convalida client del campo
* e un `servervalidation.jsp` - chiamato anche dopo le convalide del singolo server di campo su un `POST`.

### Mostrare e nascondere i componenti del modulo {#showing-and-hiding-form-components}

È possibile configurare il modulo in modo da mostrare o nascondere i componenti del modulo in base al valore degli altri campi del modulo.

La modifica della visibilità di un campo modulo è utile quando il campo è necessario solo in determinate condizioni. Ad esempio, in un modulo di feedback, una domanda chiede ai clienti se desiderano ricevere informazioni sui prodotti tramite e-mail. Selezionando sì, viene visualizzato un campo di testo che consente al cliente di digitare il proprio indirizzo e-mail.

Utilizzare la finestra di dialogo **Modifica regole di visualizzazione/nascondi** per specificare le condizioni in cui un componente del modulo viene visualizzato o nascosto.

![showhideeditor](assets/showhideeditor.png)

Utilizzare i campi nella parte superiore della finestra di dialogo per specificare le informazioni seguenti:

* Indica se si stanno specificando le condizioni per nascondere o visualizzare il componente.
* Indica se devono essere soddisfatte alcune o tutte le condizioni per mostrare o nascondere il componente.

Sotto questi campi vengono visualizzate una o più condizioni. Una condizione confronta il valore di un altro componente del modulo (nello stesso modulo) con un valore. Se il valore effettivo nel campo soddisfa la condizione, la condizione restituisce true. Le condizioni includono le seguenti informazioni:

* Titolo del campo modulo che viene testato.
* Un operatore.
* Viene confrontato un valore con il valore del campo.

Ad esempio, un componente Gruppo pulsanti di scelta con il titolo `Receive email notifications?`* * contiene `Yes` e `No` pulsanti di scelta. Un componente Campo di testo con titolo `Email Address` utilizza la seguente condizione in modo che sia visibile se `Yes` è selezionato:

![showhidecondition](assets/showhidecondition.png)

In JavaScript, le condizioni utilizzano il valore della proprietà Nome elemento per fare riferimento ai campi. Nell&#39;esempio precedente, la proprietà Nome elemento del componente Gruppo pulsanti di scelta è `contact`. Il codice seguente è il codice JavaScript equivalente per tale esempio:

`((contact == "Yes"))`

**Per mostrare o nascondere un componente modulo:**

1. Modifica il componente modulo specifico.

1. Seleziona **Mostra/Nascondi** per aprire la finestra di dialogo **Modifica regole**:

   * Nel primo elenco a discesa, selezionare **Mostra** o **Nascondi** per specificare se le condizioni determinano se mostrare o nascondere il componente.

   * Nell’elenco a discesa alla fine della riga superiore, seleziona:

      * **all** - se tutte le condizioni devono essere true per mostrare o nascondere il componente
      * **any** - se solo una o più condizioni devono essere true per mostrare o nascondere il componente

   * Nella riga della condizione, visualizzata come predefinita, selezionare un componente, un operatore e quindi specificare un valore.
   * Se necessario, aggiungere altre condizioni facendo clic su **Aggiungi condizione**.

   Ad esempio:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Fare clic su **OK** per salvare la definizione.

1. Dopo aver salvato la definizione, accanto all&#39;opzione **Mostra/Nascondi** nelle proprietà del componente modulo viene visualizzato il collegamento **Modifica regole**. Fare clic su questo collegamento per aprire la finestra di dialogo **Modifica mostra/nascondi regole** per apportare modifiche.

   Fare clic su **OK** per salvare tutte le modifiche.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Gli effetti delle definizioni Mostra/Nascondi possono essere visualizzati e testati:
   >
   >* in modalità **Anteprima** nell&#39;ambiente di authoring (è necessario ricaricare la pagina al primo passaggio all&#39;anteprima)
   >
   >* sull’ambiente di pubblicazione

#### Gestione dei riferimenti ai componenti interrotti {#handling-broken-component-references}

Le condizioni Show/hide utilizzano il valore della proprietà Element Name per fare riferimento ad altri componenti del modulo. La configurazione Mostra/Nascondi non è valida quando una delle condizioni fa riferimento a un componente eliminato o la cui proprietà Nome elemento è stata modificata. Quando si verifica questa situazione, è necessario aggiornare manualmente le condizioni o si verifica un errore durante il caricamento del modulo.

Quando la configurazione Mostra/Nascondi non è valida, viene fornita solo come codice JavaScript. Modifica il codice per risolvere i problemi. Il codice utilizza la proprietà Nome elemento utilizzata in origine per fare riferimento ai componenti.

### Sviluppo di script da utilizzare con Forms {#developing-scripts-for-use-with-forms}

Per ulteriori informazioni sugli elementi API che possono essere utilizzati durante la scrittura di script, vedi [JavaScript relativi ai moduli](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

È possibile utilizzarlo per azioni quali la chiamata di un servizio prima dell’invio del modulo e l’annullamento del servizio in caso di errore:

* Definire il tipo di risorsa di convalida
* Includi uno script per la convalida:

   * Nel JSP, chiamare il servizio Web e creare un oggetto `com.day.cq.wcm.foundation.forms.ValidationInfo` contenente i messaggi di errore. In caso di errori, i dati del modulo non verranno registrati.
