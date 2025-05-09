---
title: Configurazione dei componenti predefiniti in modalità Progettazione
description: Configurazione dei componenti di Adobe Experience Manager in modalità Progettazione.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 679ec753-1beb-49d2-9ed3-ee9abdd5f1a9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 10%

---

# Configurazione dei componenti predefiniti in modalità Progettazione{#configuring-components-in-design-mode}

Quando l’istanza AEM è installata come preconfigurata, una selezione di componenti è immediatamente disponibile nel browser Componenti.

Oltre a questi, sono disponibili vari altri componenti. È possibile utilizzare la modalità Progettazione per [abilitare/disabilitare tali componenti](#enable-disable-components). Se attivato e si trova nella pagina, è possibile utilizzare la modalità Progettazione per [configurare gli aspetti della progettazione del componente](#configuring-the-design-of-a-component) modificando i parametri dell&#39;attributo.

>[!NOTE]
>
>Presta attenzione quando modifichi questi componenti. Le impostazioni di progettazione sono spesso parte integrante della progettazione dell’intero sito web, pertanto devono essere modificate solo da un utente con i privilegi e l’esperienza appropriati, spesso un amministratore o uno sviluppatore. Per ulteriori informazioni, vedere [Sviluppo di componenti](/help/sites-developing/components.md).

>[!NOTE]
>
>La modalità Progettazione è disponibile solo per i modelli statici. I modelli creati con modelli modificabili devono essere modificati utilizzando l&#39;[editor modelli](/help/sites-authoring/templates.md).

>[!NOTE]
>
>La modalità progettazione è disponibile solo per le configurazioni di progettazione archiviate come contenuto in ( `/etc`).
>
>A partire da AEM 6.4, si consiglia di memorizzare le progettazioni come dati di configurazione in `/apps` per supportare scenari di distribuzione continua. Le progettazioni memorizzate in `/apps` non sono modificabili in fase di esecuzione e la modalità Progettazione non sarà disponibile per gli utenti non amministratori per tali modelli.

Ciò comporta l’aggiunta o la rimozione dei componenti consentiti nel sistema paragrafo per la pagina. Il sistema paragrafo ( `parsys`) è un componente composto che contiene tutti gli altri componenti paragrafo. Il sistema paragrafo consente agli autori di aggiungere a una pagina componenti di tipi diversi, in quanto contiene tutti gli altri componenti paragrafo. Ogni tipo di paragrafo è rappresentato come componente.

Ad esempio, il contenuto di una pagina di prodotto può contenere un sistema paragrafo con i seguenti elementi:

* Immagine del prodotto (sotto forma di immagine o paragrafo textimage)
* Descrizione del prodotto (come paragrafo di testo)
* Tabella con dati tecnici (come paragrafo di tabella)
* Compilazione di un modulo da parte degli utenti (come inizio del modulo, elemento del modulo e paragrafo finale del modulo)

>[!NOTE]
>
>Per ulteriori informazioni su `parsys`, vedere [Sviluppo di componenti](/help/sites-developing/components.md) e [Linee guida per l&#39;utilizzo di modelli e componenti](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components).

>[!CAUTION]
>
>La modifica della progettazione utilizzando la modalità Progettazione come descritto in questo articolo è il metodo consigliato per definire le progettazioni di modelli statici
>
>La modifica di progetti in CRX DE, ad esempio, non è una best practice e l’applicazione di tali progetti può variare rispetto al comportamento previsto.

## Abilita/Disabilita componenti {#enable-disable-components}

Per attivare o disattivare un componente:

1. Selezionare la modalità **Progettazione**.

   ![schermata_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Fai clic su un componente. Se selezionato, il componente presenta un bordo blu.

   ![schermata_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Fai clic sull&#39;icona **Elemento padre**.

   ![Elemento padre](do-not-localize/screen_shot_2018-03-22at103204.png)

   In questo modo viene selezionato il sistema paragrafo contenente il componente corrente.

1. L&#39;icona **Configura** per il sistema paragrafo è visualizzata nella barra delle azioni dell&#39;elemento padre.

   ![Configura](do-not-localize/screen_shot_2018-03-22at103256.png)

   Seleziona questa opzione per visualizzare la finestra di dialogo.

1. Utilizza la finestra di dialogo per definire i componenti disponibili nel browser Componenti durante la modifica della pagina corrente.

   ![schermata_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   La finestra di dialogo ha due schede:

   * Componenti consentiti
   * Impostazioni

   **Componenti consentiti**

   Nella scheda **Componenti consentiti**, puoi definire quali componenti sono disponibili per i parsys.

   * I componenti sono raggruppati in base ai rispettivi gruppi di componenti, che possono essere espansi e compressi.
   * È possibile selezionare un intero gruppo selezionando il nome del gruppo e deselezionando tutti gli elementi.
   * Il segno meno significa che è stato selezionato almeno un elemento del gruppo, ma non tutti.
   * È disponibile una ricerca per filtrare un componente in base al nome.
   * I numeri elencati a destra del nome del gruppo di componenti rappresentano il numero totale di componenti selezionati in tale gruppo indipendentemente dal filtro.

   Puoi definire la configurazione per ogni componente pagina. Se le pagine figlie utilizzano lo stesso modello e/o componente pagina (solitamente allineato), la stessa configurazione verrà applicata al sistema paragrafo corrispondente.

   >[!NOTE]
   >
   >I componenti dei moduli adattivi sono progettati per funzionare all’interno del Contenitore di moduli adattivi e utilizzare l’ecosistema Forms. Pertanto, questi componenti devono essere utilizzati solo nell’editor di moduli adattivi e non funzioneranno nell’editor di pagine Sites.

   **Impostazioni**

   Nella scheda **Impostazioni** puoi definire opzioni aggiuntive, ad esempio per disegnare un ancoraggio per ciascun componente e definire la spaziatura interna delle celle di ciascun contenitore.

1. Seleziona **Fine** per salvare la configurazione.

## Configurazione della progettazione di un componente {#configuring-the-design-of-a-component}

1. Selezionare la modalità **Progettazione**.

   ![schermata_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Fai clic su un componente con un bordo blu. In questo esempio, viene selezionato un componente immagine protagonista.

   ![schermata_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Utilizza l&#39;icona **Configura** per aprire la finestra di dialogo.

   ![Icona Configura](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Nella finestra di dialogo per progettazione puoi configurare il componente in base ai parametri di progettazione disponibili.

   ![schermata_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   La finestra di dialogo ha tre schede:

   * Principale
   * Funzioni
   * Stili

   **Proprietà**

   La scheda **Proprietà** consente di configurare importanti parametri di progettazione del componente. Ad esempio, per un componente immagine puoi definire le dimensioni minima e massima consentite per l’immagine.

   **Funzioni**

   La scheda **Funzionalità** consente di abilitare o disabilitare funzionalità aggiuntive del componente. Ad esempio, per un componente immagine puoi definire l’orientamento dell’immagine, le opzioni di ritaglio disponibili e se è possibile caricare un’immagine.

   **Stili**

   La scheda **Stili** consente di definire le classi e gli stili CSS da utilizzare con il componente.

   ![schermata_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Utilizza il pulsante **Aggiungi** per aggiungere altre voci a un elenco di finestre di dialogo a più voci.

   ![Aggiungi voce aggiuntiva](assets/chlimage_1-94.png)

   Utilizza l&#39;icona **Elimina** per rimuovere una voce da un elenco di finestre di dialogo a più voci.

   ![Elimina](do-not-localize/screen_shot_2018-03-22at103809.png)

   Utilizza l&#39;icona **Sposta** per cambiare l&#39;ordine delle voci in un elenco di finestre di dialogo a più voci.

   ![Sposta](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Fai clic sull&#39;icona **Fine** per salvare e chiudere la finestra di dialogo.
