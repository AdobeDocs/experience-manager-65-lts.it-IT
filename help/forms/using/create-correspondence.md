---
title: Crea corrispondenza
description: Dopo aver creato un modello di lettera, puoi utilizzarlo per creare corrispondenza in AEM Forms gestendo dati, contenuto e allegati.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: cb6528fd-6761-412d-8413-c72049acf91d
source-git-commit: d9eb2edf01200b575c6f99a47e5c010e3b3ca28a
workflow-type: tm+mt
source-wordcount: '3805'
ht-degree: 0%

---

# Crea corrispondenza{#create-correspondence}

## Creare corrispondenza nell’interfaccia utente Crea corrispondenza {#create-correspondence-in-the-create-correspondence-user-interface}

Dopo aver creato un modello di [lettere in Gestione corrispondenza](/help/forms/using/create-letter.md), l&#39;utente finale/agente/perito di attestazione può aprire la lettera nell&#39;interfaccia utente Crea corrispondenza e creare una corrispondenza immettendo dati, impostando contenuto e gestendo allegati. Infine, il perito o l&#39;agente può gestire il contenuto in modalità anteprima e inviare la lettera.

### Visualizzare in anteprima una corrispondenza {#preview-a-correspondence}

Selezionare la lettera da visualizzare in anteprima seguendo la procedura descritta di seguito.

1. Nella pagina Lettere selezionare **Seleziona**.
1. Seleziona la lettera appropriata toccandola.

   ![Seleziona lettera](assets/1_selectletter.png)

   Seleziona lettera

1. Per una lettera basata sul dizionario dati, selezionare **Anteprima** > **Anteprima**. In alternativa, per una lettera non basata sul dizionario dati, selezionare **Anteprima**. Puoi anche passare il cursore su una lettera (senza selezionarla) e selezionare l’icona Anteprima lettera per visualizzarne l’anteprima.

   >[!NOTE]
   >
   >Se alla lettera non è associato un dizionario dati, viene visualizzata l’anteprima della lettera. In caso contrario, se la lettera è basata sul dizionario dati, Gestione corrispondenza visualizza le opzioni Anteprima e Personalizzata nel menu Anteprima e puoi selezionare una delle due opzioni. È inoltre possibile associare i dati di test a un dizionario dati. Quando al dizionario dati [sono associati dati di test](../../forms/using/data-dictionary.md#p-working-with-test-data-p), quando si seleziona l&#39;opzione di anteprima, viene aperta l&#39;anteprima normale con i dati di test compilati.

1. Per poter eseguire il rendering di una corrispondenza durante l’anteprima, è necessario essere un amministratore o far parte di uno dei seguenti gruppi:

   * forms-users (per visualizzare l’anteprima sull’istanza di authoring)
   * cm-agent-users (per la rappresentazione nell’istanza Publish)

   Se non disponi delle autorizzazioni necessarie, richiedi all’amministratore l’accesso appropriato. Per ulteriori informazioni sulla creazione e l&#39;aggiunta di utenti ai gruppi, vedere [Aggiunta di utenti o gruppi a un gruppo](/help/sites-administering/security.md). Se tenti di eseguire il rendering di una corrispondenza senza disporre delle autorizzazioni appropriate, viene visualizzata la pagina di errore 404.

1. Se hai selezionato **Anteprima** > **Personalizzata**, viene visualizzata una finestra di dialogo. Nella finestra di dialogo, seleziona un file di dati corrispondente al dizionario dati con cui visualizzare l&#39;anteprima della lettera, quindi seleziona **Anteprima**. Un file di dati viene creato in base a un dizionario dati per una lettera specifica. Per ulteriori informazioni sul file di dati, vedere [Dizionario dati](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Anteprima lettera](assets/8_previewcustomdatafile.png)

1. Per impostazione predefinita, viene aperta l’anteprima della lettera HTML (anteprima moduli mobili) con la scheda Dati attivata.

   Per ulteriori informazioni sui moduli per dispositivi mobili e sulle funzionalità supportate, vedere [Differenziazione delle funzionalità tra Mobile Forms e PDF forms](/help/forms/using/feature-differentiation-html5-forms-pdf-forms.md).

   Sono disponibili tre schede: dati, contenuto e allegati. Se non sono presenti elementi di dati (variabili segnaposto e campi di layout), la lettera si apre direttamente in con la scheda Contenuto visualizzata. La scheda Allegati è disponibile solo se sono presenti allegati o se è abilitato l&#39;accesso alla libreria.

   >[!NOTE]
   >
   >Per ulteriori informazioni sul passaggio dalla modalità di rendering HTML o PDF all&#39;anteprima della lettera, vedere [Modifica della modalità di rendering della lettera](#changerenditionmode). Per ulteriori informazioni sul supporto di PDF in Gestione della corrispondenza e AEM, consulta [Interruzione dei plug-in del browser NPAPI e relativo impatto](https://helpx.adobe.com/it/acrobat/kb/change-in-support-for-acrobat-and-reader-plug-ins-in-modern-web-.html).

### Immetti i dati {#enterdata}

Nella scheda Dati, compila i campi di layout e i segnaposto disponibili.

1. Immetti i dati e le variabili di contenuto nei campi, in base alle esigenze. Compila tutti i campi obbligatori contrassegnati da un asterisco (&#42;) per abilitare il pulsante **Invia**.

   Selezionare un valore del campo dati nell&#39;anteprima lettera di HTML per evidenziare il campo dati corrispondente nella scheda Dati.

   ![Immettere i dati nella lettera](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png)

### Gestione contenuto {#managecontent}

Nella scheda del contenuto, gestisci il contenuto, ad esempio frammenti di documento e variabili di contenuto, nella lettera.

1. Seleziona **Contenuto**. Gestione corrispondenza visualizza la scheda contenuto della lettera.

   ![Scheda Contenuto - evidenzia modulo nel contenuto](assets/3_content.png)

1. Modifica i moduli di contenuto, come richiesto, nella scheda Contenuto. Per spostare lo stato attivo sul modulo del contenuto rilevante nella gerarchia del contenuto, puoi selezionare la riga o il paragrafo pertinente nell’anteprima della lettera oppure selezionare il modulo del contenuto direttamente nella gerarchia del contenuto.

   Ad esempio, la riga &quot;Abbiamo rivisto...&quot; è selezionata nell’immagine seguente e il relativo modulo di contenuto è selezionato nella scheda Contenuto.

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   Nella scheda Contenuto o Dati, toccando Evidenzia moduli selezionati ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) in alto a sinistra nell’anteprima della lettera di HTML, puoi disabilitare o abilitare la funzionalità per passare al modulo contenuto/dati quando il campo testo, paragrafo o dati pertinente è selezionato nell’anteprima della lettera.

   Per ulteriori informazioni sulle azioni disponibili per vari moduli nell&#39;interfaccia utente Crea corrispondenza, vedere [Azioni e informazioni disponibili nell&#39;interfaccia utente Crea corrispondenza](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Per individuare i moduli di contenuto, utilizzare il campo Trova. Inserisci il nome o il titolo completo o parziale del modulo di contenuto per cercarlo nella corrispondenza.
1. Selezionare l&#39;icona di visualizzazione ( ![visualizzazione](assets/display.png)) davanti a un elenco, testo, condizione o area di destinazione per visualizzarla o nasconderla nella lettera.
1. Per modificare un modulo di testo in linea o modificabile, seleziona l&#39;icona **Modifica** pertinente ( ![edittextmodule](assets/edittextmodule.png)) oppure fai doppio clic sul modulo di testo corrispondente nell&#39;anteprima della lettera.

   Il sistema visualizza un editor di testo per modificare e formattare il testo.

   Il correttore ortografico predefinito nel browser controlla l&#39;ortografia nell&#39;editor di testo. Per gestire il controllo ortografico e grammaticale, è possibile modificare le impostazioni del correttore ortografico del browser oppure installare i plug-in e gli add-on del browser per il controllo ortografico e grammaticale.

   È inoltre possibile utilizzare le varie scelte rapide da tastiera disponibili nell&#39;editor di testo per gestire, modificare e formattare il testo. Per ulteriori informazioni sulle scelte rapide da tastiera dell&#39;[Editor di testo](/help/forms/using/keyboard-shortcuts.md#correspondence-management) in Scelte rapide da tastiera per Gestione corrispondenza.

   ![5_edittextmodule](assets/5_edittextmodule.png)

   È possibile riutilizzare uno o più paragrafi di testo esistenti in un&#39;altra applicazione del documento. È possibile copiare e incollare direttamente il testo, ad esempio da MS Word, pagine HTML o qualsiasi altra applicazione.

   È possibile copiare e incollare uno o più paragrafi di testo in un modulo di testo modificabile. Ad esempio, è possibile disporre di un documento di MS Word con un elenco puntato di prove di residenza accettabili come:

   ![pastetextmsword](assets/pastetextmsword.png)

   È possibile copiare e incollare direttamente il testo dal documento di MS Word in un modulo di testo modificabile. Nel modulo di testo viene mantenuta la formattazione come elenco puntato, carattere e colore del testo.

   ![pastetexteditablemodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >La formattazione del testo incollato, tuttavia, presenta alcune limitazioni.

   È possibile applicare un rientro al testo e ai numeri nella lettera utilizzando il tasto TAB. È ad esempio possibile utilizzare il tasto TAB per allineare più colonne di testo di un elenco in un formato tabulare.

   ![tabspaces](assets/tabspaces.png)

   Esempio: utilizzo del tasto TAB per allineare più colonne di testo in un formato tabulare

1. Se necessario, inserisci caratteri speciali nella corrispondenza. Ad esempio, è possibile utilizzare la tavolozza Caratteri speciali per inserire:

   * Simboli di valuta come €,¥ e £
   * Simboli matematici come ∑, √, ∂ e ^
   * Simboli di punteggiatura come ‟ e &quot;

   ![caratteri speciali](assets/specialcharacters.png)

   Gestione della corrispondenza supporta 210 caratteri speciali. L&#39;amministratore può [aggiungere il supporto di caratteri speciali aggiuntivi/personalizzati tramite personalizzazione](../../forms/using/custom-special-characters.md).

1. Per evidenziare/enfatizzare parti di testo in un modulo inline modificabile, selezionate il testo e selezionate Colore evidenziazione.

   ![letterbackgroundcolor](assets/letterbackgroundcolor.png)

   È possibile selezionare direttamente un colore di base `**[A]**` presente nella tavolozza Colori di base oppure selezionare **Seleziona** dopo aver utilizzato il cursore `**[B]**` per scegliere la tonalità appropriata del colore.

   Se necessario, è anche possibile passare alla scheda Avanzate per selezionare la tonalità, la luminosità e la saturazione `**[C]**` appropriate per creare il colore preciso, quindi selezionare Seleziona `**[D]**` per applicare il colore per evidenziare il testo.

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. Apporta le modifiche appropriate al contenuto e al formato e seleziona **Salva**. Selezionare ( ![editnextmoduleccr](assets/editnextmoduleccr.png)) per spostarsi tra moduli di testo modificabili oppure selezionare **Salva e Successivo** per salvare le modifiche e passare al successivo modulo di testo modificabile.
1. Il sistema visualizza anche le variabili non compilate per ciascuno dei rami. Quando non ci sono variabili vuote, le variabili vuote vengono visualizzate come 0. Se è presente una variabile non compilata, puoi selezionare un ramo per espanderla e individuare la variabile non compilata. Utilizza la barra degli strumenti del contenuto per eliminare il contenuto, aumentare/ridurre il rientro del contenuto e inserire interruzioni di pagina prima/dopo il contenuto.

   È possibile inserire interruzioni di pagina al di sopra e al di sotto dei moduli dati anche quando fanno parte di elenchi e condizioni.

1. Selezionare Apri/chiudi variabile di contenuto ( ![opencontentvariables](assets/opencontentvariables.png)) per aprire le variabili di contenuto e compilarle in modo appropriato.
1. Una volta compilata correttamente la variabile non compilata, il conteggio della variabile non compilata viene impostato su 0.

   Nell’interfaccia utente per la creazione di corrispondenza, il conteggio delle variabili non compilate viene visualizzato a ogni livello della gerarchia di qualsiasi modulo che contiene almeno una variabile. Se un modulo contiene variabili non compilate, il conteggio viene visualizzato a livello di variabile, modulo, area di destinazione e modello di lettera.

   Il conteggio delle variabili non compilate include:

   * Solo variabili del dizionario dati non protette e segnaposto. Il conteggio delle variabili non include variabili layout o del dizionario dati protetto.
   * Campi obbligatori
   * Campi layout se obbligatori e associati all’utente.
   * Solo istanze di variabili univoche. Se un modulo, un’area di destinazione o un modello di lettera contiene due o più istanze della stessa variabile, il conteggio viene visualizzato come 1 (uno). Tuttavia, per ciascuna istanza, il conteggio viene visualizzato come 1.

   Il conteggio delle variabili non compilate non include i moduli deselezionati. Se un modulo è incluso in un modello di lettera ma non è incluso nella lettera, il conteggio delle variabili non compilate in questo modulo non viene visualizzato.

   Per l&#39;area di destinazione, il modulo e la variabile, il conteggio viene visualizzato a destra di ciascun oggetto nel modello di lettera. Tuttavia, per il modello completo, il conteggio viene visualizzato nella barra di stato Crea corrispondenza.

   I moduli in un modello di lettera visualizzano il conteggio delle variabili non compilate come descritto di seguito:

   * **Testo** Visualizza la somma delle variabili segnaposto non compilate univoche e degli elementi del dizionario dati contenuti nel modulo di testo.
   * **Condizione** Visualizza la somma delle variabili di condizione univoche non compilate contenute nella condizione e delle variabili contenute nei moduli risultanti.
   * **Elenco** Visualizza la somma di tutte le variabili univoche non compilate contenute nei moduli assegnati all&#39;elenco.
   * **Area di destinazione** Visualizza la somma di tutte le variabili univoche non compilate contenute nei moduli assegnati all&#39;area di destinazione.

   Per quanto riguarda le variabili con valori predefiniti, tieni presente quanto segue:

   * Un campo variabile booleano predefinito è *false*. Tuttavia, la variabile è considerata non compilata. Ciò implica che il conteggio delle variabili include tutti i campi della variabile booleana con valore *false*.

   * Il valore predefinito di un campo variabile numerica è *0 (zero)*. Tuttavia, la variabile è considerata non compilata. Ciò implica che il conteggio delle variabili include tutti i campi delle variabili numeriche con valore *0 (zero)*.

#### Azioni e informazioni disponibili nella scheda Crea contenuto corrispondenza {#actions-and-info-available-in-the-create-correspondence-content-tab}

**Area di destinazione**

* Inserisci riga vuota: inserisce una nuova riga vuota.
* Inserisci testo in linea: inserisce un nuovo modulo di testo.
* Blocco ordine (info): indica che l&#39;ordine del contenuto non può essere modificato.
* Valori non compilati (info): indica il numero di variabili non compilate nell&#39;area di destinazione.

**Modulo**

* Selezione (icona occhio): include\esclude il modulo dalla lettera.
* Salta punti elenco (applicabile ai moduli elenco e ai relativi moduli figlio): salta i punti elenco in un modulo specifico.
* Interruzione di pagina prima di (applicabile ai moduli figlio dell’area di destinazione): inserisce l’interruzione di pagina prima del modulo.
* Interruzione di pagina dopo (applicabile ai moduli figlio dell’area di destinazione): inserisce l’interruzione di pagina prima del modulo.
* Valori non compilati (info): indica il numero di variabili non compilate nell&#39;area di destinazione.
* Modifica (solo moduli di testo): apri l’editor Rich Text per modificare il modulo di testo.
* Pannello dati (moduli di testo e condizione): apre tutte le variabili del modulo.

**Modulo elenco**

* Inserisci riga vuota: inserisce una nuova riga vuota.
* Libreria dei contenuti: apre la libreria dei contenuti per aggiungere moduli all’elenco.
* Impostazione elenco (solo elenco nidificato):
* Blocco ordine (info): indica che l&#39;ordine delle voci dell&#39;elenco non può essere modificato.

### Gestisci allegati {#manage-attachments}

1. Seleziona **Allegati**. Gestione corrispondenza visualizza gli allegati disponibili, in base alle impostazioni configurate durante la creazione del modello di lettera.
1. È possibile scegliere di non inviare un allegato insieme alla lettera toccando l&#39;icona di visualizzazione e selezionare la croce nell&#39;allegato per eliminarlo dalla lettera. Per gli allegati specificati, durante la creazione di un modello di lettera, come Obbligatorio, le icone Visualizza ed Elimina sono disattivate.
1. Seleziona l&#39;icona Accesso libreria ( ![accesso libreria](assets/libraryaccess.png)) per accedere alla libreria dei contenuti e inserire risorse DAM come allegati.

   >[!NOTE]
   >
   >L’icona Accesso libreria è disponibile solo se è stato abilitato l’accesso alla libreria durante l’authoring della lettera.

1. Se l&#39;ordine degli allegati non è stato bloccato durante la creazione della corrispondenza, è possibile riordinare gli allegati selezionando un allegato e toccando le frecce giù e su.

   Per ulteriori informazioni, vedere [Consegna allegato](#attachmentdelivery).

### Gestire il contenuto in anteprima e inviare la lettera {#manage-content-in-preview-and-submit-the-letter}

Puoi apportare modifiche al layout e al contenuto per garantire che la lettera abbia l’aspetto desiderato e inviarla ai vari processi di post.

1. Per evidenziare tutto il contenuto modificabile nella lettera, selezionare **Evidenzia sezioni modificabili**.

   Il contenuto modificabile della lettera viene evidenziato con sfondo grigio.

   ![Evidenzia contenuto modificabile](assets/4_highlightmoduleincontent-1.png)

1. Modifica i moduli di contenuto, come richiesto, nella scheda Contenuto. Per spostare lo stato attivo sul modulo del contenuto rilevante nella gerarchia del contenuto, puoi selezionare la riga o il paragrafo pertinente nell’anteprima della lettera oppure selezionare il modulo del contenuto direttamente nella gerarchia del contenuto.

   Ad esempio, la riga &quot;Per consentirci di accedere a...&quot; è selezionata nell&#39;immagine seguente e il modulo di contenuto corrispondente è selezionato nella scheda Contenuto.

   Toccando Evidenzia moduli selezionati nel contenuto ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)), puoi disabilitare o abilitare la funzionalità per evidenziare il modulo del contenuto nella scheda Contenuto quando il testo, il paragrafo o il campo dati rilevante viene toccato nell&#39;anteprima della lettera.

   Per ulteriori informazioni sulle azioni disponibili per vari moduli nell&#39;interfaccia utente Crea corrispondenza, vedere [Azioni e informazioni disponibili nell&#39;interfaccia utente Crea corrispondenza](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Per aggiungere un&#39;interruzione di pagina alla lettera, selezionare il punto in cui si desidera inserire un&#39;interruzione di pagina e selezionare Interruzione di pagina prima o Interruzione di pagina dopo ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Nella lettera viene inserito un segnaposto di interruzione di pagina esplicito. Per visualizzare il modo in cui un’interruzione di pagina esplicita influisce sulla lettera, consulta l’anteprima PDF semplificata.

   >[!NOTE]
   >
   >Poiché i moduli mobili non supportano le interruzioni di pagina, le intestazioni e i piè di pagina vengono visualizzati una sola volta. Tuttavia, è possibile impostare esplicitamente le intestazioni e i piè di pagina nel layout (per pagina) in modo che vengano visualizzati nell&#39;anteprima dei moduli mobili. Inoltre, le eventuali pagine vuote nella lettera non vengono visualizzate nell’anteprima dei moduli per dispositivi mobili.

   ![Interruzione di pagina esplicita](assets/8_pagebreak.png)

1. Per salvare la lettera come bozza e continuare a utilizzarla in seguito, selezionare Salva come bozza. Per utilizzare questa opzione, la lettera deve essere [pubblicata](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Per ulteriori informazioni, vedere Istanza bozza in [Salvataggio delle bozze e invio delle istanze di lettere](#savingdrafts).

   ![saveasdraft](assets/saveasdraft.png)

   Viene visualizzata la finestra di dialogo Nome bozza lettera con l&#39;ID istanza della lettera. Facoltativamente, puoi modificare questo ID. Prendere nota dell&#39;ID lettera, quindi selezionare **Fine**. In seguito puoi utilizzare questo ID per [ricaricare la bozza della lettera](submit-letter-topostprocess.md#reloaddraft).

1. Per visualizzare l&#39;anteprima della lettera come PDF appiattito con il layout esatto e le interruzioni di pagina che verranno inviate, selezionare ( ![anteprima](assets/preview.png)) Anteprima.

   La lettera viene visualizzata come un PDF appiattito. Il PDF appiattito è l&#39;esatta rappresentazione della lettera, in quanto verrà inviata con i font, le interruzioni e il layout corretti della lettera.

   >[!NOTE]
   >
   >Se utilizzi il tipo di rappresentazione Mozilla Firefox e HTML, per visualizzare l’anteprima della lettera come PDF appiattito, assicurati di utilizzare il plug-in nativo del browser e non il plug-in Acrobat. Per selezionare il plug-in del browser nativo, vai alle impostazioni di Mozilla Firefox e per il tipo di contenuto PDF, seleziona Anteprima in Firefox.

1. Se l&#39;anteprima di PDF appiattita è soddisfacente, selezionare **Invia** per inviare la lettera. In alternativa, per modificare la lettera, seleziona **Esci da anteprima** per tornare all&#39;anteprima dell&#39;interfaccia utente per la creazione di corrispondenza della lettera e apportare modifiche alla lettera. Quando selezioni Invia, se la configurazione Gestisci istanza lettera è abilitata nell’istanza Pubblica, viene generata l’istanza della lettera di invio.

   Per ulteriori informazioni, vedere Istanza bozza in Salvataggio delle bozze e invio delle istanze di lettere.

   È inoltre possibile salvare la lettera come bozza per modificarla in un secondo momento.

   Dopo aver apportato le modifiche necessarie, è possibile inviare la lettera dall&#39;anteprima di HTML5 oppure selezionare nuovamente Anteprima per rivedere l&#39;output del PDF appiattito.

   Per informazioni sulle differenze tra HTML5 Forms e PDF forms, vedere [Differenziazione delle caratteristiche tra HTML5 Forms e PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## Salvataggio delle bozze e invio delle istanze di lettere {#savingdrafts}

Quando si esegue il rendering di una lettera nell’interfaccia utente Crea corrispondenza, è possibile salvare la lettera come visualizzata.

È possibile salvare due tipi di istanze di lettere: Istanza bozza e Istanza invio.

* **Istanza bozza**: l&#39;istanza bozza acquisisce lo stato corrente della lettera visualizzata in anteprima. Per salvare una bozza di istanza, accertatevi innanzitutto che la lettera e tutte le risorse a cui fa riferimento la lettera siano nello stato Pubblicato. Per informazioni sulla pubblicazione di una lettera, consulta [Pubblicare una risorsa](../../forms/using/publishing-unpublishing-forms.md#publishanasset). È necessario pubblicare una lettera prima di salvarla come bozza, poiché quando si pubblica una lettera, si crea una versione della lettera, delle risorse dipendenti e dei dati a quel punto. La versione pubblicata di una lettera non può essere modificata da te o da un altro utente e può essere ripristinata in un secondo momento senza alcuna discrepanza imprevista dalla versione pubblicata. Puoi tornare a questa istanza in un secondo momento e continuare da dove ti sei allontanato.

* **Istanza di invio**: le istanze di invio acquisiscono lo stato della lettera durante l&#39;invio. L’istanza di invio memorizza lo stato PDF dell’istanza della lettera dopo la post-elaborazione insieme ai dati immessi dall’utente nell’interfaccia utente di Creazione corrispondenza.

Tali istanze possono essere salvate solo quando la lettera viene visualizzata nell’istanza Publish. Per impostazione predefinita, il salvataggio sulle istanze è disattivato. Per abilitare il salvataggio delle istanze di lettere, effettuare le seguenti operazioni.

1. In AEM, apri la configurazione della console web di Adobe Experience Manager per il server utilizzando il seguente URL: https://&lt;server>:&lt;porta>/&lt;contextpath>/system/console/configMgr
1. Individua **[!UICONTROL Configurazioni gestione corrispondenza]** e fai clic su di esso.
1. Controlla **[!UICONTROL Gestisci istanze lettere nella configurazione di pubblicazione]** e fai clic su **[!UICONTROL Salva]**.

### Abilita funzione Salva bozza {#enable-save-draft-feature}

Prima di pubblicare lettere o salvare bozze nell’istanza di pubblicazione, effettua le seguenti operazioni sull’istanza di authoring e di pubblicazione per abilitare la funzione Salva come bozza:

Per impostazione predefinita, le proprietà *cq:lastReplicationAction*, *cq:lastreplicated* e *cq:lastReplicatedBy* non vengono trasferite all&#39;istanza Publish. Per trasferire le proprietà *cq:lastReplicationAction*, *cq:lastreplicated* e *cq:lastReplicatedBy* all&#39;istanza Publish, disabilitare il componente [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory]. Per disattivare il componente:

1. Nell’istanza di authoring, apri la console Componenti della console Web di Adobe Experience Manager. URL predefinito: `http://author-server:port/system/console/components`

1. Cerca il componente **[!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory]**.

1. Fare clic sull&#39;icona ![Disable button](/help/forms/using/assets/enablebutton.png) per disabilitare il componente [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory].

![Istanza autore](/help/forms/using/assets/replicationproperties.png)

Per abilitare la funzione Salva come bozza, sostituisci l&#39;URL esistente in [!UICONTROL URL di authoring di VersionRestoreManager] con l&#39;URL dell&#39;istanza di authoring. Per sostituire l’URL:

1. Nell&#39;istanza di pubblicazione aprire [!UICONTROL Configurazione console Web di Adobe Manager]. URL predefinito: `https://publish-server:port/system/console/configMgr`

1. Cerca e apri il componente **[!UICONTROL Gestione corrispondenza - Configurazioni ripristino versione istanza di authoring]**.

1. Individuare il campo **[!UICONTROL URL autore]** di VersionRestoreManager e specificare l&#39;URL per l&#39;istanza di authoring.

1. Fai clic su Salva.

![Istanza di pubblicazione](/help/forms/using/assets/correspondencemanagement.png)

Quando è attivato il salvataggio delle istanze di lettere, è possibile selezionare la posizione in cui salvare le istanze di lettere. Sono disponibili due opzioni per il salvataggio delle istanze di lettere: Salvataggio locale o Salvataggio remoto.

### Salvataggio locale {#local-save}

Le istanze di lettere vengono salvate nell’istanza di pubblicazione e vengono replicate in senso inverso nell’istanza di authoring.

### Salvataggio remoto {#remote-save}

Questa opzione è disponibile per le persone che hanno dubbi sul salvataggio dei dati utente nelle istanze di pubblicazione, che in genere si trovano al di fuori del firewall aziendale. Quando è attivato il salvataggio remoto, le istanze di lettere non vengono salvate nell’istanza di pubblicazione, ma vengono salvate in remoto nell’autore dell’elaborazione specificato tramite le configurazioni di SDK del client LiveCycle.

#### Abilita salvataggio remoto {#enable-remote-save}

1. In AEM, aprire Configurazione console Web Adobe Experience Manager per il server utilizzando il seguente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. Cerca **[!UICONTROL Configurazioni gestione corrispondenza]** e fai clic su di essa.
1. Individua la configurazione di **[!UICONTROL Salvataggio remoto]**, verificala e fai clic su **[!UICONTROL Salva]**.

#### Specificare le impostazioni di elaborazione dell’autore {#specify-processing-author-settings}

1. In AEM, aprire Configurazione console Web Adobe Experience Manager per il server utilizzando il seguente URL: `https://<server>:<port>/system/console/configMgr`

   ![Configurazione console Web Adobe Experience Manager](assets/2configmanager.png)

1. In questa pagina, individua Adobe LiveCycle Client SDK Configuration ed espandila facendo clic su di essa.

1. Nell&#39;URL del server di elaborazione, immettere il nome del server LiveCycle, fornire le informazioni di accesso, quindi fare clic su **Salva**.

   ![Immettere il nome e le informazioni di accesso del server LiveCycle](assets/3configmanager.png)

1. Se necessario, impostare il nome utente e la password con cui si desidera accedere al server.

#### Consegna dell’allegato {#attachmentdelivery}

* Gli allegati della lettera sono disponibili per la fase post in PDF, che viene creata dopo l’invio della lettera.
* Quando viene eseguito il rendering della lettera utilizzando le API lato server come PDF interattivo o non interattivo, il PDF sottoposto a rendering contiene allegati come allegati PDF.
* Quando un processo di post associato a un modello di lettera viene caricato come parte delle operazioni Invia o Completa corrispondenza tramite l’interfaccia utente Crea corrispondenza, gli allegati vengono passati come parametro List&lt;com.adobe.idp.Document> in AttachmentDocs.
* Anche i meccanismi di consegna predefiniti, come e-mail e Stampa, consegnano allegati insieme al PDF della corrispondenza generata.

## Modalità di rappresentazione dell’anteprima di una lettera: anteprima moduli mobile e anteprima PDF {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms Correspondence Management visualizza una lettera come HTML nell’interfaccia utente per la creazione di corrispondenza. Tuttavia, Gestione della corrispondenza supporta ancora il ripristino dell’anteprima PDF invece di quella HTML. Per ulteriori informazioni sul passaggio dalla modalità di anteprima HTML alla modalità PDF, vedere [Modificare la modalità di rendering della lettera](#changerenditionmode).

Di seguito sono riportati i vantaggi e le funzionalità disponibili nell’anteprima di HTML e PDF.

**Vantaggi di Mobile Forms/Anteprima HTML**

* **Selezionare un valore di campo dati per evidenziare il campo dati corrispondente**: nell&#39;interfaccia utente Crea corrispondenza è possibile selezionare un valore di campo dati nella lettera per evidenziare il campo dati corrispondente nella scheda Dati. Per ulteriori informazioni, vedere [Immettere i dati](#enterdata).

* **Supporto browser**: i browser ritirano gradualmente il supporto per NPAPI, influendo sull&#39;anteprima PDF della lettera. Questo non influisce sull’anteprima di una lettera nei moduli HTML/mobili.
* **Evidenzia contenuto modificabile in una lettera**: nell&#39;interfaccia utente Crea corrispondenza è possibile selezionare Evidenzia contenuto modificabile per evidenziare tutto il contenuto modificabile nella lettera in grigio. Per ulteriori informazioni, vedere [Gestione contenuto](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>` **Vantaggi dell&#39;anteprima PDF**

* **Interruzione di pagina**: nell&#39;anteprima di PDF puoi visualizzare esattamente in che modo le interruzioni di pagina nella lettera influiscono sul relativo output.
* **Anteprima finale**: nell&#39;anteprima di PDF è possibile visualizzare la formattazione e l&#39;aspetto esatti della lettera così come apparirà nell&#39;output.

Per informazioni sul supporto degli script in PDF forms, vedere [Supporto degli script](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html).

Per ulteriori informazioni sul supporto degli script nei moduli HTML5, vedere [Supporto degli script per i moduli HTML5](/help/forms/using/scripting-support.md).

### Cambia la modalità di rappresentazione della lettera {#changerenditionmode}

Per impostazione predefinita, nell’interfaccia utente per la creazione di corrispondenza vengono utilizzati i moduli HTML o mobili per eseguire il rendering dell’anteprima della lettera. L’anteprima dei moduli mobili non presenta problemi di rendering in alcun browser, poiché utilizza il plug-in nativo del browser e non richiede plug-in aggiuntivi. Potete cambiare la modalità di anteprima della lettera in PDF. Tuttavia, i vincoli del browser possono creare problemi per diverse funzioni dell’anteprima PDF interattiva della lettera.

Per ulteriori informazioni sulla compatibilità del browser con l&#39;anteprima della lettera, vedere [Interruzione dei plug-in del browser NPAPI e relativo impatto](https://helpx.adobe.com/it/acrobat/kb/change-in-support-for-acrobat-and-reader-plug-ins-in-modern-web-.html).

La procedura seguente illustra come modificare la modalità di anteprima della lettera:

1. Vai a `https://[system]:'port'/system/console/configMgr` e, se necessario, accedi come Amministratore.
1. Vai a **[!UICONTROL Configurazioni di gestione della corrispondenza]** > **[!UICONTROL Tipo di rappresentazione]** e seleziona **Rappresentazione HTML** (predefinita) o **Rappresentazione PDF**.
1. Fai clic su **[!UICONTROL Salva]**.
