---
title: Componenti di Adobe Campaign
description: Quando si esegue l’integrazione con Adobe Campaign, sono disponibili componenti per l’utilizzo di newsletter e moduli.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
exl-id: abdb803b-a770-4f4b-8788-45d067341e0f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 6%

---

# Componenti di Adobe Campaign{#adobe-campaign-components}

Quando si esegue l’integrazione con Adobe Campaign, sono disponibili componenti per l’utilizzo di newsletter e moduli. Entrambi sono descritti in questo documento.

>[!CAUTION]
>
>I componenti e-mail di AEM sono stati dichiarati obsoleti. A causa della natura dell’e-mail, che unisce contenuto e stile, i componenti e-mail forniti come predefiniti da AEM vengono riutilizzati in modo limitato per i clienti, a causa della necessità di implementare stili personalizzati in tutti i componenti necessari per i progetti.
>
>I componenti e-mail possono essere implementati a livello di progetto e i componenti e-mail AEM obsoleti illustrano come farlo. Tuttavia, non utilizzare questi componenti obsoleti nei progetti.

## Componenti della newsletter di Adobe Campaign {#adobe-campaign-newsletter-components}

Tutti i componenti di Campaign seguono le best practice descritte in [Best practice per i modelli e-mail](/help/sites-administering/best-practices-for-email-templates.md) e si basano sul linguaggio di markup Adobe [HTL](https://helpx.adobe.com/it/experience-manager/htl/using/overview.html).

Quando apri una newsletter/e-mail configurata per l&#39;integrazione con Adobe Campaign, dovresti vedere i seguenti componenti nella sezione **Newsletter Adobe Campaign**:

* Intestazione (Campaign)
* Immagine (Campaign)
* Collegamento (Campagna)
* Modello immagini di Scene7 (Campaign)
* Riferimento di destinazione (Campaign)
* Testo e immagine (Campaign)
* Testo e personalizzazione (Campaign)

La descrizione di questi componenti è riportata nella sezione seguente.

![chlimage_1-81](assets/chlimage_1-81.png)

### Intestazione (Campaign) {#heading-campaign}

Il componente intestazione può:

* Visualizza il nome della pagina corrente lasciando vuoto il campo **Titolo**.
* Visualizza un testo specificato nel campo **Titolo**.

Puoi modificare direttamente il componente **Intestazione (Campaign)**. Lascia vuoto per usare il titolo della pagina.

![chlimage_1-82](assets/chlimage_1-82.png)

Puoi configurare quanto segue:

* **Titolo**
Se si desidera utilizzare un nome diverso dal titolo della pagina, immetterlo qui.

* **Livello di intestazione (1, 2, 3, 4)**
Il livello di intestazione si basa sulle dimensioni di intestazione 1-4 di HTML.

L’esempio seguente mostra un componente Titolo (Campagna) visualizzato.

![chlimage_1-83](assets/chlimage_1-83.png)

### Immagine (Campaign) {#image-campaign}

Il componente Immagine (campagna) visualizza un’immagine e il testo che la accompagna in base ai parametri specificati.

Puoi caricare un’immagine, quindi modificarla e manipolarla (ad esempio ritagliarla, ruotarla, aggiungere un collegamento/titolo/testo).

Puoi caricare un’immagine, quindi modificarla e manipolarla (ad esempio ritagliarla, ruotarla, aggiungere un collegamento/titolo/testo). È possibile trascinare un&#39;immagine da [Content Finder](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui) direttamente nel componente o nella relativa finestra di dialogo di modifica. Puoi anche fare doppio clic nell’area centrale della finestra di dialogo Modifica per sfogliare il file system locale e caricare un’immagine. Le due schede della finestra di dialogo Modifica controllano anche tutte le definizioni e le manipolazioni dell’immagine:

![chlimage_1-84](assets/chlimage_1-84.png)

Quando viene caricata un’immagine, puoi configurare quanto segue:

* **Mappa**
Per mappare un&#39;immagine, selezionare Mappa. È possibile specificare la modalità di creazione della mappa immagine (rettangolo, poligono e così via) e il punto a cui deve puntare l&#39;area.

* **Ritaglio**
Seleziona Ritaglia per ritagliare un’immagine. Utilizzare il mouse per ritagliare l&#39;immagine.

* **Ruota**
Per ruotare un&#39;immagine, selezionare Ruota. Usare ripetutamente fino a quando l&#39;immagine non viene ruotata nel modo desiderato.

* **Cancella**
Rimuove l&#39;immagine corrente.

* Barra di zoom (solo classica)
Per ingrandire e ridurre l&#39;immagine, utilizzare la barra di scorrimento sotto l&#39;immagine (sopra i pulsanti OK e Annulla)
* **Titolo**
Titolo dell&#39;immagine.

* **Testo alternativo**
Testo alternativo da utilizzare per la creazione di contenuto accessibile.

* **Collegamento A**
Crea un collegamento alle risorse o ad altre pagine del tuo sito web.

* **Descrizione**
Descrizione dell&#39;immagine.

* **Dimensione**
Imposta l&#39;altezza e la larghezza dell&#39;immagine.

>[!NOTE]
>
>Immetti le informazioni nel campo **Testo alternativo** della scheda **Avanzate** oppure l&#39;immagine non può essere salvata e viene visualizzato il seguente messaggio di errore:
>
>`Validation failed. Verify the values of the marked fields.`
>

L’esempio seguente mostra un componente Immagine (Campaign) visualizzato.

![chlimage_1-85](assets/chlimage_1-85.png)

### Collegamento (Campagna) {#link-campaign}

Il componente Collegamento (Campagna) consente di aggiungere un collegamento alla newsletter. Questo componente è disponibile solo nell’interfaccia utente classica, ma è possibile aggiungerne uno nell’interfaccia touch e aprirlo in modalità di compatibilità.

![chlimage_1-86](assets/chlimage_1-86.png)

Puoi configurare quanto segue nelle schede **Visualizzazione**, **Informazioni URL** o **Avanzate**:

* **Didascalia collegamento**
Didascalia del collegamento. Questo è il testo visualizzato dagli utenti.

* **Descrizione comando collegamento**
Aggiunge ulteriori informazioni sull&#39;utilizzo del collegamento.

* **TipoCollegamento**
Nell&#39;elenco a discesa selezionare tra un **URL personalizzato** e un **documento adattivo**. Questo campo è obbligatorio. Se selezioni URL personalizzato, puoi fornire l’URL del collegamento. Se selezioni Documento adattivo, puoi fornire il percorso del documento.

* **Parametro URL aggiuntivo**
Aggiungi eventuali parametri URL aggiuntivi. Fai clic su Aggiungi elemento per aggiungere più elementi.

>[!NOTE]
>
>Immetti le informazioni nel campo **Tipo di collegamento** nella scheda **Informazioni URL** oppure il componente non può essere salvato e viene visualizzato il seguente messaggio di errore:
>
>`Validation failed. Verify the values of the marked fields.`
>

L’esempio seguente mostra un componente Collega (Campagna) visualizzato.

![chlimage_1-87](assets/chlimage_1-87.png)

### Riferimento di destinazione (Campaign) {#targeted-reference-campaign}

Il componente Riferimento di destinazione (Campaign) consente di creare un riferimento a un paragrafo di destinazione.

In questo componente, passa al paragrafo di destinazione per selezionarlo.

Fare clic sul menu a discesa per passare al paragrafo a cui si desidera fare riferimento. Al termine, fare clic su **OK**.

### Testo e immagine (Campaign) {#text-image-campaign}

Il componente Testo e immagine (Campaign) aggiunge un blocco di testo e un’immagine.

![chlimage_1-88](assets/chlimage_1-88.png)

Come per i componenti Testo e Personalization (Campaign) e Immagine (Campaign), puoi configurare:

* **Testo**
Immettere il testo. Utilizza la barra degli strumenti per modificare la formattazione, creare elenchi e aggiungere collegamenti.

* **Immagine**
Trascina un&#39;immagine dal Finder dei contenuti o fai clic per passare a un&#39;immagine. Ritagliare o ruotare in base alle esigenze.

* **Proprietà immagine** (**Proprietà immagine avanzate**)
Consente di specificare quanto segue:

   * **Titolo**
Titolo del blocco, visualizzato a comparsa.

   * **Testo alternativo**
Testo alternativo da visualizzare se l’immagine non può essere visualizzata.

   * **Collegamento a**
Crea un collegamento alle risorse o ad altre pagine del tuo sito web.

   * **Descrizione**
Descrizione dell&#39;immagine.

   * **Dimensione**
Imposta l&#39;altezza e la larghezza dell&#39;immagine.

>[!NOTE]
>
>Il campo **Testo alternativo** nella scheda **Avanzate** è obbligatorio oppure il componente non può essere salvato e viene visualizzato il seguente messaggio di errore:
>
>`Validation failed. Verify the values of the marked fields.`
>

L’esempio seguente mostra un componente Testo e immagine (Campaign) visualizzato.

![chlimage_1-89](assets/chlimage_1-89.png)

### Testo e personalizzazione (Campaign) {#text-personalization-campaign}

Il componente Testo e Personalization (Campaign) consente di immettere un blocco di testo utilizzando un editor di WYSIWYG, con funzionalità fornite dall&#39;[editor Rich Text](/help/sites-authoring/rich-text-editor.md). Questo componente consente inoltre di utilizzare i campi di contesto e i blocchi di personalizzazione disponibili da Adobe Campaign. Vedere anche [Inserimento di Personalization](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization).

La selezione delle icone consente di formattare il testo, incluse le caratteristiche dei caratteri, l&#39;allineamento, i collegamenti, gli elenchi e i rientri.

Aggiungi il testo come si farebbe normalmente nell’editor Rich Text. Aggiungi la personalizzazione selezionando il menu a discesa Adobe Campaign e selezionando i campi appropriati.

![chlimage_1-90](assets/chlimage_1-90.png)

Aggiungi i campi di testo e di contesto o i blocchi di personalizzazione per creare il contenuto. Quindi, seleziona ClientContext per verificare i dati nei profili utente tipo. Dopo aver selezionato una persona, i campi di personalizzazione vengono sostituiti automaticamente dai dati del profilo selezionato.

>[!NOTE]
>
>Vengono presi in considerazione solo i campi definiti nello schema **nms:seedMember** o in una delle sue estensioni. Gli attributi delle tabelle collegate a `nms:seedMember` non sono disponibili.

## Componenti di Adobe Campaign Form {#adobe-campaign-form-components}

I componenti Adobe Campaign vengono utilizzati per creare un modulo che gli utenti compilano per abbonarsi a una newsletter, annullare l’abbonamento a una newsletter o aggiornare i propri profili utente. Per ulteriori informazioni, vedere [Creazione di Adobe Campaign Forms](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md).

Ogni campo componente può essere collegato a un campo del database di Adobe Campaign. I campi disponibili variano a seconda del tipo di dati in essi contenuti, come descritto nella sezione [Componenti e tipo di dati](#components-and-data-type). Se estendi lo schema dei destinatari in Adobe Campaign, i nuovi campi saranno disponibili nei componenti i cui tipi di dati corrispondono.

Quando apri un modulo configurato per l&#39;integrazione con Adobe Campaign, nella sezione **Adobe Campaign** vengono visualizzati i seguenti componenti:

* Casella di selezione (Campaign)
* Campo data (Campaign) e Campo data/HTML5 (Campaign)
* Chiave principale crittografata (Campaign)
* Visualizzazione errori (Campaign)
* Chiave di riconciliazione nascosta (Campaign)
* Campo numerico (Campaign)
* Campo opzione (Campaign)
* Lista di controllo delle iscrizioni (Campaign)
* Campo testo (Campaign)

Questa sezione descrive in dettaglio ogni componente.

### Componenti e tipo di dati {#components-and-data-type}

La tabella seguente descrive i componenti disponibili per visualizzare e modificare i dati del profilo di Adobe Campaign. Ogni componente può essere mappato su un campo del profilo Adobe Campaign per visualizzarne il valore e aggiornare il campo quando il modulo viene inviato. I diversi componenti possono essere associati solo a campi di un tipo di dati appropriato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Componente</strong></p> </td>
   <td><p><strong>Tipo di dati del campo Adobe Campaign</strong></p> </td>
   <td><p><strong>Campo di esempio</strong></p> </td>
  </tr>
  <tr>
   <td><p>Casella di selezione (Campaign)</p> </td>
   <td><p>booleano</p> </td>
   <td><p>Non contattare più (tramite alcun canale)</p> </td>
  </tr>
  <tr>
   <td><p>Campo data (Campaign)</p> <p>Campo data/HTML 5 (Campaign)</p> </td>
   <td><p>data</p> </td>
   <td><p>Data di nascita</p> </td>
  </tr>
  <tr>
   <td><p>Campo numerico (Campaign)</p> </td>
   <td><p>numerico (byte, breve, lungo, doppio)</p> </td>
   <td><p>Età</p> </td>
  </tr>
  <tr>
   <td><p>Campo opzione (Campaign)</p> </td>
   <td><p>byte con valori associati</p> </td>
   <td><p>Genere</p> </td>
  </tr>
  <tr>
   <td><p>Campo testo (Campaign)</p> </td>
   <td><p>stringa</p> </td>
   <td><p>E-mail</p> </td>
  </tr>
 </tbody>
</table>

### Impostazioni comuni alla maggior parte dei componenti {#settings-common-to-most-components}

I componenti di Adobe Campaign hanno impostazioni comuni a tutti i componenti (ad eccezione dei componenti Crittografia chiave primaria e Riconciliazione nascosta).

Nella maggior parte dei componenti, puoi configurare i seguenti elementi:

#### Titolo e testo {#title-and-text}

* **Titolo**
Se desideri utilizzare un nome diverso da quello dell’elemento, inseriscilo qui.

* **Nascondi titolo**
Selezionare questa casella di controllo se non si desidera visualizzare il titolo.

* **Descrizione**
Aggiungi una descrizione al campo per fornire ulteriori informazioni agli utenti.

* **Mostra solo valore**
Mostra solo il valore, se presente

#### Adobe Campaign {#adobe-campaign}

Puoi configurare quanto segue:

* **Mappatura**
Se necessario, seleziona un campo di personalizzazione Adobe Campaign.

* **Chiave riconciliazione**
Seleziona questa casella di controllo se questo campo fa parte della chiave di riconciliazione.

#### Vincoli {#constraints}

* **Obbligatorio** - Selezionare questa casella di controllo per rendere obbligatorio il componente, ovvero gli utenti devono immettere un valore.
* **Messaggio richiesto** - È possibile aggiungere un messaggio che indica che il campo è obbligatorio.

#### Attribuzione stile {#styling}

* **CSS**
Immetti le classi CSS da utilizzare per questo componente.

### Casella di selezione (Campaign) {#checkbox-campaign}

Il componente Casella di controllo (Campaign) consente all’utente di modificare i campi del profilo Adobe Campaign di tipo dati booleano. Ad esempio, puoi avere un componente Casella di controllo (Campagna) che consente al destinatario di specificare che non desidera essere contattato tramite alcun canale.

Puoi [configurare le impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components) nel componente Casella di controllo (Campagna).

L’esempio seguente mostra un componente Casella di controllo (Campaign) visualizzato.

![chlimage_1-91](assets/chlimage_1-91.png)

### Campo data (Campaign) e Campo data/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilizza il campo data per consentire ai destinatari di impostare una data, ad esempio per specificare la data di nascita. Il formato della data corrisponde al formato utilizzato nell’istanza Adobe Campaign.

Oltre alle [impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components), puoi configurare quanto segue:

* **Vincoli - Vincolo** - È possibile selezionare - **Nessuno** o **Data** per aggiungere il vincolo di una data o nessun vincolo. Se selezioni data, la risposta che gli utenti immettono nel campo deve essere in un formato data.

* **Messaggio vincolo** - È inoltre possibile aggiungere un messaggio vincolo per consentire agli utenti di formattare correttamente le risposte.
* **Stile - Larghezza** - Regola la larghezza del campo toccando o facendo clic sulle icone **+** e **-** o immettendo un numero.

L’esempio seguente mostra un componente Campo data (Campaign) con la larghezza regolata.

![chlimage_1-92](assets/chlimage_1-92.png)

### Chiave principale crittografata (Campaign) {#encrypted-primary-key-campaign}

Questo componente definisce il nome del parametro URL che conterrà l&#39;identificatore di un profilo di Adobe Campaign (**Identificatore risorsa principale** o **Chiave primaria crittografata** in Adobe Campaign Standard e 6.1, rispettivamente).

Ogni modulo che visualizza e modifica i dati del profilo di Adobe Campaign **deve** includere un componente chiave primaria crittografata.

Nel componente Chiave primaria crittografata (Campaign) puoi configurare quanto segue:

* **Titolo e testo - Nome elemento** - Impostazione predefinita: encryptedPK. È necessario modificare il nome dell&#39;elemento solo quando è in conflitto con il nome di un altro elemento nel modulo. Non ci sono due campi modulo che possono avere lo stesso nome elemento.
* **Adobe Campaign - Parametro URL** - Aggiungi il parametro URL per EPK. Ad esempio, puoi utilizzare il valore **epk**.

L’esempio seguente mostra un componente Chiave primaria crittografata (Campaign) visualizzato.

![chlimage_1-93](assets/chlimage_1-93.png)

### Visualizzazione errori (Campaign) {#error-display-campaign}

Questo componente consente di visualizzare gli errori di back-end. Per il corretto funzionamento del componente, la gestione degli errori del modulo deve essere impostata su Inoltra.

L’esempio seguente mostra un componente Visualizzazione errori (Campaign) visualizzato.

![chlimage_1-94](assets/chlimage_1-94.png)

### Chiave di riconciliazione nascosta (Campaign) {#hidden-reconciliation-key-campaign}

Il componente Chiave riconciliazione nascosta (Campaign) consente di aggiungere campi nascosti come parte della chiave di riconciliazione a un modulo.

Nel componente Chiave riconciliazione nascosta (Campaign) puoi configurare quanto segue:

* **Titolo e testo - Nome elemento** - Impostazione predefinita: reconcilKey. È necessario modificare il nome dell&#39;elemento solo quando è in conflitto con il nome di un altro elemento nel modulo. Non ci sono due campi modulo che possono avere lo stesso nome elemento.
* **Adobe Campaign - Mappatura** - Esegui il mapping a un campo di personalizzazione Adobe Campaign.

L’esempio seguente mostra un componente Chiave di riconciliazione nascosta (Campaign) visualizzato.

![chlimage_1-95](assets/chlimage_1-95.png)

### Campo numerico (Campaign) {#numeric-field-campaign}

Utilizza il campo numerico per consentire ai destinatari di immettere numeri, ad esempio la loro età.

Oltre alle [impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components), puoi configurare quanto segue:

* **Vincoli - Vincolo** a discesa
È possibile selezionare - **Nessuno** o **Numerico -** per aggiungere il vincolo di un numero o di nessun vincolo. Se si seleziona numero, la risposta che gli utenti immettono nel campo deve essere numerica.

* **Messaggio vincolo** - È inoltre possibile aggiungere un messaggio vincolo per consentire agli utenti di formattare correttamente le risposte.
* **Stile - Larghezza** - Regola la larghezza del campo toccando o facendo clic sulle icone **+** e **-** o immettendo un numero.

L’esempio seguente mostra un componente Campo numerico (Campaign) con la larghezza configurata.

![chlimage_1-96](assets/chlimage_1-96.png)

### Campo opzione (Campaign) {#option-field-campaign}

Questo elenco a discesa consente di selezionare un’opzione, ad esempio il genere o lo stato di un destinatario.

È possibile [configurare le impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components) nel componente Campo opzione (Campaign). Per popolare l’elenco a discesa, seleziona il campo appropriato nei campi di personalizzazione di Adobe Campaign toccando o facendo clic sul simbolo Adobe Campaign e navigando fino al campo.

L’esempio seguente mostra un componente Campo opzione (Campaign) visualizzato.

![chlimage_1-97](assets/chlimage_1-97.png)

### Lista di controllo delle iscrizioni (Campaign) {#subscriptions-checklist-campaign}

Utilizza il componente **Elenco di controllo sottoscrizioni (Campaign)** per modificare le sottoscrizioni associate a un profilo Adobe Campaign.

Quando viene aggiunto a un modulo, questo componente visualizza tutte le sottoscrizioni disponibili come caselle di controllo e consente all’utente di selezionare le sottoscrizioni desiderate. Quando gli utenti inviano il modulo, questo componente sottoscrive o annulla l&#39;abbonamento dell&#39;utente ai servizi selezionati a seconda del tipo di azione del modulo (**Adobe Campaign: Subscribe to Services** o **Adobe Campaign: Unsubscribe from Services**).

>[!NOTE]
>
>Il componente non controlla i servizi a cui l’utente è già abbonato/da cui ha annullato l’abbonamento.

È possibile [configurare le impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components) nel componente Elenco di controllo sottoscrizioni (Campaign). Non sono disponibili configurazioni di Adobe Campaign per questo componente.

L’esempio seguente mostra un componente Elenco di controllo iscrizioni (Campaign) visualizzato.

![chlimage_1-98](assets/chlimage_1-98.png)

### Campo testo (Campaign) {#text-field-campaign}

Il componente Campo di testo (Campaign) che consente di immettere dati di tipo stringa, ad esempio un nome, un cognome, un indirizzo, un indirizzo e-mail e così via.

Oltre alle [impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components), puoi configurare quanto segue:

* **Vincoli - Vincolo** - Elenco a discesa - È possibile selezionare - **Nessuno**, **E-mail**, **Nome** (senza umlaut) per aggiungere il vincolo di un indirizzo e-mail, di un nome o di nessun vincolo. Se selezioni e-mail, la risposta che gli utenti immettono nel campo deve essere un indirizzo e-mail. Se selezioni nome, deve essere un nome (gli umlaut non sono consentiti).

* **Messaggio vincolo** - È inoltre possibile aggiungere un messaggio vincolo per consentire agli utenti di formattare correttamente le risposte.
* **Stile - Larghezza** - Regola la larghezza del campo toccando o facendo clic sulle icone **+** e **-** o immettendo un numero.

L’esempio seguente mostra un componente Campo di testo (Campaign) visualizzato.

![chlimage_1-99](assets/chlimage_1-99.png)
