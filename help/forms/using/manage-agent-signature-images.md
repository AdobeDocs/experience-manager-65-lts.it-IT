---
title: Gestisci immagini firma agente
description: Dopo aver creato un modello di lettera, puoi utilizzarlo per creare corrispondenza in AEM Forms gestendo dati, contenuto e allegati.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 3081dedf-ba92-4205-af67-930524719e60
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Gestisci immagini firma agente{#manage-agent-signature-images}

## Panoramica {#overview}

In Gestione corrispondenza puoi utilizzare un’immagine per eseguire il rendering della firma dell’agente in lettere. Dopo aver impostato l&#39;immagine della firma dell&#39;agente durante la creazione di una lettera, è possibile eseguire il rendering dell&#39;immagine della firma dell&#39;agente nella lettera come firma dell&#39;agente mittente.

Il DDE agentSignatureImage è un DDE calcolato che rappresenta l&#39;immagine della firma dell&#39;agente. L’espressione per questo DDE calcolato utilizza una nuova funzione personalizzata esposta dal blocco predefinito di Expression Manager. Questa funzione personalizzata considera agentID e agentFolder come parametri di input e recupera il contenuto dell’immagine in base a tali parametri. Il dizionario dati di sistema SystemContext consente alle lettere di Gestione corrispondenza di accedere alle informazioni nel contesto di sistema corrente. Il contesto di sistema include informazioni sui parametri di configurazione attivi e utente attualmente connessi.

È possibile aggiungere immagini nella cartella cmuserroot. In [Proprietà di configurazione di Gestione corrispondenza](/help/forms/using/cm-configuration-properties.md), utilizzando la proprietà radice utente CM è possibile modificare la cartella da cui viene prelevata l&#39;immagine della firma dell&#39;agente.

Il valore di agentFolder DDE viene ricavato dal parametro di configurazione CMUserRoot per le proprietà di configurazione di Gestione corrispondenza. Per impostazione predefinita, questo parametro di configurazione punta a/content/cmUserRoot nell’archivio CRX. È possibile modificare il valore della configurazione CMUserRoot in Proprietà di configurazione.
È inoltre possibile sovrascrivere la funzione personalizzata predefinita per definire la propria logica per il recupero dell’immagine della firma utente.

## Aggiunta dell&#39;immagine della firma agente {#adding-agent-signature-image}

1. Assicurati che l’immagine della firma dell’agente abbia lo stesso nome del nome utente di AEM dell’utente. L&#39;estensione non è necessaria per il nome file dell&#39;immagine.
1. In CRX, creare una cartella denominata `cmUserRoot` nella cartella dei contenuti.

   1. Vai a `https://'[server]:[port]'/crx/de`. Se necessario, accedi come amministratore.

   1. Fare clic con il pulsante destro del mouse sulla cartella **content** e selezionare **Create** > **Create Folder**.

      ![Crea cartella](assets/1_createnode_cmuserroot.png)

   1. Nella finestra di dialogo Crea cartella immettere il nome della cartella come `cmUserRoot`. Fare clic su **Salva tutto**.

      >[!NOTE]
      >
      >cmUserRoot è il percorso predefinito in cui AEM cerca l&#39;immagine della firma dell&#39;agente. È tuttavia possibile modificarla modificando la proprietà Cartella principale utente di CM nelle [proprietà di configurazione di Gestione corrispondenza](/help/forms/using/cm-configuration-properties.md).

1. In Esplora contenuto, passa alla cartella cmUserRoot e aggiungi l’immagine della firma dell’agente.

   1. Vai a `https://'[server]:[port]'/crx/explorer/index.jsp`. Se necessario, accedi come amministratore.
   1. Fare clic su **Esplora contenuto**. Esplora contenuto si apre in una nuova finestra.
   1. In Esplora contenuto passare alla cartella cmUserRoot e selezionarla. Fare clic con il pulsante destro del mouse sulla cartella **cmUserRoot** e selezionare **Nuovo nodo**.

      ![Nuovo nodo in cmUserRoot](assets/2_cmuserroot_newnode.png)

      Effettuare le seguenti voci nella riga per il nuovo nodo, quindi fare clic sul segno di spunta verde.

      **Nome:** JohnDoe (o il nome del file di firma dell&#39;agente)

      **Tipo:** nt:file

      Nella cartella `cmUserRoot` viene creata una nuova cartella denominata `JohnDoe` (o il nome specificato nel passaggio precedente).

   1. Fare clic sulla nuova cartella creata (qui `JohnDoe`). In Esplora contenuto il contenuto della cartella viene visualizzato come inattivo.

   1. Fare doppio clic sulla proprietà **jcr:content**, impostarne il tipo come **nt:resource**, quindi fare clic sul segno di spunta verde per salvare la voce.

      Se la proprietà non è presente, creare innanzitutto una proprietà denominata jcr:content.

      ![jcr:content, proprietà](assets/3_jcrcontentntresource.png)

      Tra le sottoproprietà di jcr:content vi è jcr:data, che è inattivo. Fare doppio clic su jcr:data. La proprietà diventa modificabile e nella voce viene visualizzato il pulsante Scegli file. Fare clic su **Scegli file** e selezionare il file di immagine da utilizzare come logo. Il file di immagine non deve avere un&#39;estensione.

      ![Dati JCR](assets/5_jcrdata.png)

   Fare clic su **Salva tutto**.

1. Verificare che l&#39;XDP\layout utilizzato nella lettera disponga di un campo immagine in basso a sinistra (o in un altro punto appropriato del layout in cui si desidera eseguire il rendering della firma) per eseguire il rendering dell&#39;immagine della firma.
1. Durante la creazione della corrispondenza, nella scheda Dati seleziona un campo immagine per l’immagine della firma seguendo la procedura riportata di seguito:

   1. Selezionate Sistema (System) dal menu a comparsa Tipo di collegamento nel riquadro di destra.

   1. Selezionare il DDE agentSignatureImage dall&#39;elenco nel pannello Elemento dati per il DD SystemContext.

   1. Salva la lettera.

1. Quando viene eseguito il rendering della lettera, puoi vedere la firma nell’anteprima della lettera nel campo immagine in base al layout.

   ![Immagine della firma dell&#39;agente nella lettera](assets/letterwithsignature.png)
