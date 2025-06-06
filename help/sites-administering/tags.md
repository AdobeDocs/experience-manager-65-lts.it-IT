---
title: Amministrazione dei tag
description: Scopri come gestire e amministrare i tag in Adobe Experience Manager.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 6659ca39-f297-40b9-88e2-d942aa653e9b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 4%

---

# Amministrazione dei tag {#administering-tags}

I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. Possono essere considerate come parole chiave o etichette (metadati) che consentono di trovare più rapidamente il contenuto come risultato di una ricerca.

In Adobe Experience Manager (AEM), un tag può essere una proprietà di

* un nodo di contenuto per una pagina (vedi [Utilizzo dei tag](/help/sites-authoring/tags.md))

* un nodo di metadati per una risorsa (vedi [Gestione dei metadati per Digital Assets](/help/assets/metadata.md))

## Funzioni tag {#tag-features}

Alcune delle funzioni dei tag in AEM includono:

* I tag possono essere raggruppati in vari spazi dei nomi. Tali gerarchie consentono la creazione di tassonomie. Queste tassonomie sono globali in AEM.
* La restrizione principale per i nuovi tag creati è che devono essere univoci all’interno di uno spazio dei nomi specifico.
* Il titolo di un tag non deve includere i caratteri di separazione del percorso del tag (né verranno visualizzati se presenti)

   * due punti `:` - delimita il tag dello spazio dei nomi
   * barra `/` - delimita i tag secondari

* I tag possono essere applicati da autori e visitatori del sito. Indipendentemente dall’autore, tutte le forme di tag sono disponibili per la selezione, sia durante l’assegnazione a una pagina che durante la ricerca.
* I tag possono essere creati e la relativa tassonomia può essere modificata dai membri del gruppo &quot;amministratori di tag&quot; e dai membri con diritti di modifica per `/content/cq:tags`.

   * Un tag che contiene tag figlio viene definito tag contenitore
   * Un tag che non è un tag contenitore viene definito tag foglia
   * Uno spazio dei nomi dei tag è un tag foglia o un tag contenitore

* I tag vengono utilizzati dal [componente Ricerca](https://helpx.adobe.com/it/experience-manager/core-components/using/quick-search.html) per facilitare la ricerca del contenuto.
* I tag sono utilizzati dal [componente Teaser](https://helpx.adobe.com/it/experience-manager/core-components/using/teaser.html), che monitora il cloud di tag di un utente per fornire contenuti mirati.
* Se l’assegnazione tag è un aspetto importante del contenuto

   * assicurati di creare un pacchetto di tag con le pagine che li utilizzano
   * assicurati che [le autorizzazioni tag](#setting-tag-permissions) abilitino l&#39;accesso in lettura

## Console per assegnazione tag {#tagging-console}

La console Assegnazione tag consente di creare e gestire i tag e le relative tassonomie. Un obiettivo è quello di evitare di avere molti tag simili relativi essenzialmente alla stessa cosa : per esempio, pagina e pagine o calzature e scarpe.

I tag vengono gestiti raggruppandoli in spazi dei nomi, esaminando l’utilizzo dei tag esistenti prima di crearne di nuovi e riorganizzandoli senza disconnettere il tag dal contenuto a cui si fa attualmente riferimento.

Per accedere alla console Assegnazione tag:

* all’autore
* accedi con privilegi amministrativi
* dalla navigazione globale

   * seleziona **`Tools`**
   * seleziona **`General`**
   * seleziona **`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Creazione di uno spazio dei nomi {#creating-a-namespace}

Per creare uno spazio dei nomi, selezionare l&#39;icona **`Create Namespace`**.

Lo spazio dei nomi è di per sé un tag e non deve contenere tag secondari. Tuttavia, per continuare a creare una tassonomia, [crea tag secondari](#creating-tags), che a loro volta possono essere tag foglia o tag contenitore.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creazione_tag_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Titolo**
  *(obbligatorio)* Titolo visualizzato per lo spazio dei nomi.

* **Nome**
  *(facoltativo)* Nome per lo spazio dei nomi. Se non viene specificato, viene creato un nome di nodo valido dal titolo. Vedi [TagID](/help/sites-developing/framework.md#tagid).

* **Descrizione**
  *(facoltativo)* Descrizione dello spazio dei nomi.

Una volta inserite le informazioni richieste

* seleziona **Crea**

### Operazioni sui tag {#operations-on-tags}

La selezione di uno spazio dei nomi o di un altro tag rende disponibili le seguenti operazioni:

* [Visualizza proprietà](#viewing-tag-properties)
* [Riferimenti](#showing-tag-references)
* [Crea tag](#creating-tags)
* [Modifica](#editing-tags)
* [Spostare](#moving-tags)
* [Unisci](#merging-tags)
* [Pubblicazione](#publishing-tags)
* [Annulla pubblicazione](#unpublishing-tags)
* [Elimina](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

Quando la finestra del browser non è sufficientemente ampia da visualizzare tutte le icone, le icone più a destra sono raggruppate sotto l&#39;icona **`... More`**, che, se selezionata, visualizzerà un elenco a discesa delle icone delle operazioni nascoste.

![chlimage_1-185](assets/chlimage_1-185.png)

### Selezione di un tag dello spazio dei nomi {#selecting-a-namespace-tag}

Quando viene selezionato per la prima volta, se lo spazio dei nomi non contiene tag, le proprietà vengono visualizzate a destra, altrimenti vengono visualizzati i tag figlio. Per ogni tag selezionato vengono visualizzati i tag in esso contenuti o le relative proprietà se non sono presenti tag figlio.

Per selezionare il tag per le operazioni e per la selezione multipla, seleziona solo l’icona accanto al titolo. Selezionando il titolo verranno visualizzate solo le proprietà o verrà aperto il tag per visualizzarne il contenuto.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Visualizzazione delle proprietà dei tag {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Quando si seleziona uno spazio dei nomi o un altro tag, la selezione dell&#39;icona **`View Properties`** determina la visualizzazione delle informazioni relative a `name`, ora dell&#39;ultima modifica e numero di riferimenti. Se pubblicato, vengono visualizzati l’ora dell’ultima pubblicazione e l’ID dell’editore. Queste informazioni vengono visualizzate in una colonna a sinistra delle colonne dei tag.

![chlimage_1-189](assets/chlimage_1-189.png)

### Visualizzazione dei riferimenti dei tag {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Quando selezioni uno spazio dei nomi o un altro tag, l&#39;icona **Riferimenti** identifica il contenuto a cui è stato applicato il tag.

La visualizzazione iniziale è un conteggio dei tag applicati.

![chlimage_1-191](assets/chlimage_1-191.png)

Selezionando la freccia a destra del conteggio, vengono elencati i nomi dei riferimenti.

Il tracciato del riferimento viene visualizzato come descrizione quando si passa il puntatore su un riferimento.

![chlimage_1-192](assets/chlimage_1-192.png)

### Creazione di tag {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Quando si seleziona uno spazio dei nomi o un altro tag selezionando l&#39;icona accanto al titolo, è possibile creare un tag figlio per il tag corrente selezionando l&#39;icona **`Create Tag`**.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Titolo**
*(obbligatorio) *Un titolo di visualizzazione per il tag.

* **Nome**
*(facoltativo) *Un nome per il tag. Se non viene specificato, viene creato un nome di nodo valido dal titolo. Vedi [TagID](/help/sites-developing/framework.md#tagid).

* **Descrizione**
*(facoltativo) *Una descrizione del tag.

Una volta inserite le informazioni richieste

* seleziona **Crea**

### Modifica dei tag {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Quando si seleziona uno spazio dei nomi o un altro tag, è possibile modificare il Titolo, la Descrizione e specificare le localizzazioni del Titolo selezionando l&#39;icona **`Edit`**.

Dopo aver apportato le modifiche, seleziona **Salva**.

Per informazioni dettagliate sull&#39;aggiunta di traduzioni per lingua, vedere la sezione relativa a [Gestione dei tag in lingue diverse](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Spostamento dei tag {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Quando si seleziona uno spazio dei nomi o un altro tag, la selezione dell&#39;icona **`Move`** consentirà agli amministratori e agli sviluppatori di tag di ripulire la tassonomia spostando il tag in una nuova posizione o rinominandolo. Quando il tag selezionato è un tag contenitore, lo spostamento del tag comporta lo spostamento anche di tutti i tag figlio.

>[!NOTE]
>
>Si consiglia di consentire agli autori solo di [modificare](#editing-tags) il tag `title`, non di spostare o rinominare i tag.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Percorso**
  *(sola lettura)* Percorso corrente del tag selezionato.

* **Sposta in**
Individua il nuovo percorso in cui spostare il tag.

* **Rinomina in**
Visualizza inizialmente il `name` corrente del tag. È possibile immettere un nuovo `name`.

* seleziona **Salva**

### Unione di tag {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

L’unione di tag può essere utilizzata quando una tassonomia presenta duplicati. Quando il tag A viene unito al tag B, tutte le pagine contrassegnate con il tag A vengono contrassegnate con il tag B e il tag A non è più disponibile per gli autori.

Quando selezioni uno spazio dei nomi o un altro tag, l&#39;icona **Unisci** apre un pannello in cui è possibile selezionare il percorso in cui eseguire l&#39;unione.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Percorso**
  *(sola lettura)* Percorso del tag selezionato da unire in un altro tag.

* **Unisci in**
Sfoglia per selezionare il percorso del tag in cui eseguire l’unione.

>[!NOTE]
>
>Dopo l&#39;unione, il **percorso** selezionato in origine non esisterà (virtualmente) più.
>
>Quando un tag di riferimento viene spostato o unito, il tag non viene fisicamente eliminato in modo tale da poter mantenere i riferimenti.

### Pubblicazione dei tag {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Quando è selezionato uno spazio dei nomi o un altro tag, seleziona l&#39;icona **Pubblica** per attivare il tag nell&#39;ambiente di pubblicazione. Analogamente al contenuto della pagina, viene pubblicato solo il tag selezionato, indipendentemente dal fatto che si tratti o meno di un tag contenitore.

Per pubblicare una tassonomia (uno spazio dei nomi e tag secondari), è consigliabile creare un [pacchetto](/help/sites-administering/package-manager.md) dello spazio dei nomi (vedi [Nodo principale tassonomia](/help/sites-developing/framework.md#taxonomy-root-node)). Assicurarsi di [applicare le autorizzazioni](#setting-tag-permissions) allo spazio dei nomi prima di creare il pacchetto.

### Annullamento della pubblicazione dei tag {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Quando selezioni uno spazio dei nomi o un altro tag, se fai clic sull&#39;icona **Annulla pubblicazione**, il tag verrà disattivato nell&#39;ambiente di authoring e rimosso dall&#39;ambiente di pubblicazione. Simile all&#39;operazione `Delete`, se il tag selezionato è un tag contenitore, tutti i relativi tag figlio verranno disattivati nell&#39;ambiente di authoring e rimossi dall&#39;ambiente di pubblicazione.

### Eliminazione dei tag {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Quando viene selezionato uno spazio dei nomi o un altro tag, se si seleziona l&#39;icona **Elimina** il tag verrà rimosso definitivamente dall&#39;ambiente di authoring. Se il tag è stato pubblicato, viene rimosso anche dall’ambiente di pubblicazione. Se il tag selezionato è un tag contenitore, verranno rimossi anche tutti i relativi tag figlio.

## Impostazione delle autorizzazioni dei tag {#setting-tag-permissions}

Le autorizzazioni per i tag sono [&#39;sicure (per impostazione predefinita)&#39;](/help/sites-administering/production-ready.md). Si tratta di una best practice per l&#39;ambiente di pubblicazione che richiede l&#39;autorizzazione di lettura per essere consentita in modo esplicito per i tag. In pratica, questo avviene creando un pacchetto dello spazio dei nomi dei tag dopo aver impostato le autorizzazioni per l’authoring e installando il pacchetto su tutte le istanze di pubblicazione.

* sull’istanza di authoring

   * accedi con privilegi amministrativi
   * accedere a [Console sicurezza](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * ad esempio, passa a http://localhost:4502/useradmin

   * nel riquadro di sinistra, selezionare il gruppo (o l&#39;utente) per il quale deve essere concessa l&#39;[autorizzazione di lettura](/help/sites-administering/security.md#permissions)
   * nel riquadro di destra, individua il **Percorso &#x200B;** dello spazio dei nomi dei tag

      * ad esempio, `/content/cq:tags/mycommunity`

   * seleziona `checkbox`nella colonna **Leggi**
   * seleziona **Salva**

![chlimage_1-204](assets/chlimage_1-204.png)

* assicurarsi che tutte le istanze di pubblicazione abbiano le stesse autorizzazioni

   * un approccio consiste nel [creare un pacchetto](/help/sites-administering/package-manager.md#package-manager) dello spazio dei nomi sull&#39;autore

      * nella scheda `Advanced`, per `AC Handling` seleziona `Overwrite`

   * replicare il pacchetto

      * scegli `Replicate` da gestione pacchetti

## Gestione dei tag in lingue diverse {#managing-tags-in-different-languages}

La proprietà `title` di un tag può essere tradotta in più lingue. Una volta tradotto, il tag appropriato `title` può essere visualizzato in base alla lingua dell&#39;utente o alla lingua della pagina.

### Definizione dei titoli di tag in più lingue {#defining-tag-titles-in-multiple-languages}

Di seguito viene descritto come tradurre il `title`tag **Animali** dall&#39;inglese al tedesco e al francese.

Per iniziare, seleziona il tag nello spazio dei nomi **Foto Stock** e fai clic sull&#39;icona **`Edit`** (consulta la sezione [Modifica dei tag](#editing-tags)).

Il pannello Modifica tag consente di scegliere le lingue in cui localizzare il titolo del tag.

Quando viene selezionata una lingua, viene visualizzata una casella di testo in cui è possibile immettere il titolo tradotto.

Una volta immesse tutte le traduzioni, seleziona **Salva** per uscire dalla modalità di modifica.

![chlimage_1-205](assets/chlimage_1-205.png)

In generale, la lingua scelta per il tag viene presa dalla lingua della pagina, quando disponibile. Quando il widget [`tag`](/help/sites-developing/building.md#tagging-on-the-client-side) viene utilizzato in altri casi (ad esempio nei moduli o nelle finestre di dialogo), il linguaggio dei tag dipende dal contesto.

Invece di usare l’impostazione della lingua della pagina, la console Assegnazione tag utilizza l’impostazione della lingua utente. Nella console Assegnazione tag, per il tag &quot;Animals&quot;, veniva visualizzato &quot;Animaux&quot; per un utente che impostava la lingua sul francese nelle proprietà utente.

Per aggiungere una nuova lingua alla finestra di dialogo, vedere [Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>Il tag cloud e le parole chiave meta nel componente pagina standard utilizzano il tag localizzato `titles` in base alla lingua della pagina, se disponibile.

## Riferimenti {#resources}

* [Assegnazione di tag per sviluppatori](/help/sites-developing/tags.md)

  Informazioni sul framework dei tag ed estensione e inclusione dei tag nelle applicazioni personalizzate.

* [Console classica per l’assegnazione di tag dell’interfaccia utente](/help/sites-administering/classic-console.md)
