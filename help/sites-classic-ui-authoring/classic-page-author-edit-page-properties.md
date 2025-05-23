---
title: Modifica delle proprietà di pagina
description: Le proprietà di una pagina possono variare a seconda della natura della pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni sulla Live Copy saranno disponibili nel modo appropriato.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 0dd160d5-6a08-4c11-92d2-a5a75fc47dba
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 20%

---

# Modifica delle proprietà di una pagina{#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni sulla Live Copy saranno disponibili nel modo appropriato.

## Proprietà pagina {#page-properties}

Le proprietà sono distribuite in diverse schede:

### Base {#basic}

* **Titolo**

  Il titolo della pagina viene visualizzato in varie posizioni. Ad esempio, l&#39;elenco di schede **Siti Web** e le visualizzazioni **Siti** per schede/elenchi.

  Questo campo è obbligatorio.

* **Tag**

  Qui puoi aggiungere o rimuovere i tag dalla pagina aggiornando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * Per aggiungere un tag completamente nuovo, digitane il nome in una casella di selezione vuota.

     Il nuovo tag verrà effettivamente creato quando premi Invio. Il nuovo tag verrà quindi visualizzato in una casella, con una piccola stella a destra che indica che si tratta di un nuovo tag.

   * Con l’elenco a discesa puoi selezionare uno dei tag esistenti.
   * Quando si passa il mouse su una voce di tag nel riquadro di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere il tag per la pagina.

* **Nascondi in navigazione**

  Un interruttore per indicare se la pagina viene visualizzata o nascosta nella navigazione della pagina.

* **Titolo pagina**

  Titolo da utilizzare nella pagina.

* **Titolo navigazione**

  Puoi specificare un titolo separato da utilizzare nella navigazione (ad esempio, se desideri qualcosa di più conciso). Se vuoto, il **Titolo** è utilizzato.

* **Sottotitolo**

  Sottotitolo da utilizzare nella pagina.

* **Descrizione**

  Descrizione della pagina, il suo scopo o altri dettagli.

* **Ora di attivazione**

  La data e l’ora in cui verrà attivata la pagina pubblicata. Quando viene pubblicata, la pagina rimarrà inattiva fino all’ora specificata.

  Lascia questi campi vuoti per le pagine da pubblicare immediatamente (lo scenario più consueto).

* **Ora di disattivazione**

  L’ora in cui la pagina pubblicata verrà disattivata.

  Di nuovo, lascia vuoti questi campi per le pagine che desideri pubblicare immediatamente.

* **URL personalizzato**

  Consente di immettere un URL personalizzato per questa pagina. Questo ti consente di avere un URL più breve e più espressivo.

  Ad esempio, se l&#39;URL personalizzato è impostato su w `elcome` per la pagina identificata dal percorso / `v1.0/startpage` per il sito Web h `ttp://example.com,` allora h `ttp://example.com/welcome` sarà l&#39;URL personalizzato di h `ttp://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >Gli URL personalizzati:
  >
  >* deve essere univoco, quindi accertati che il valore non sia già utilizzato da un’altra pagina.
  >* non supportano i pattern regex.

* **Reindirizza URL personalizzato**

  Indica se desideri che la pagina utilizzi il Vanity URL.

### Avanzate  {#advanced}

* **Lingua**

  Lingua della pagina.

* **Reindirizzamento**

  Indica la pagina a cui deve essere automaticamente reindirizzata la pagina.

* **Design**

  Indica la [progettazione](/help/sites-developing/designer.md) da utilizzare per questa pagina.

* **Alias**

  Specificare un alias da utilizzare per la pagina.

* **Abilita gruppo utenti chiuso**

  Abilita o disabilita l&#39;utilizzo di [gruppi utenti chiusi](/help/sites-administering/cug.md) (CUG).

* **Pagina di accesso**

  Pagina da utilizzare per l’accesso.

* **Gruppi ammessi**

  Gruppi idonei per l’accesso al CUG.

* **Area di autenticazione**

  Nome area di autenticazione per il gruppo utenti chiusi.

* **Configurazione esportazione**

  Specifica una configurazione di esportazione.

### Miniatura  {#thumbnail}

* **Miniatura pagina**

  Mostra l&#39;immagine di anteprima della pagina. Operazioni disponibili:

   * **Genera anteprima**

     Genera un’anteprima della pagina da utilizzare come miniatura.

   * **Carica immagine**

     Carica un&#39;immagine da usare come miniatura.

### Servizi cloud {#cloud-services}

* **Servizi cloud**

  Definisci le proprietà per [Cloud Services](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Personalizzazione**

  Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Autorizzazioni   {#permissions}

* **Autorizzazioni** (interfaccia touch)

  Visualizza le [autorizzazioni valide e aggiungi nuove autorizzazioni](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

  Definisci le proprietà per una pagina blueprint nella [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

  Definisci le proprietà per una pagina Live Copy nella [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisci i collegamenti alle pagine che forniscono funzionalità a livello di sito, ad esempio **Pagina registrazione**, **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-2}

### Modifica delle proprietà di una pagina specifica {#editing-page-properties-for-a-specific-page}

Le Proprietà pagina definiscono le varie proprietà della pagina, ad esempio i titoli, quando vengono visualizzati sul sito web e altri.

1. Apri la pagina da modificare.

1. Nella barra laterale apri la scheda **Pagina**, quindi seleziona **Proprietà pagina...**

   Viene visualizzata una finestra di dialogo con più schede.

1. Apporta le modifiche necessarie, quindi fai clic su **OK** per salvare.
