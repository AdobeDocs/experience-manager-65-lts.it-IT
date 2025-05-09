---
title: Servizio Forms
description: L'articolo descrive il servizio Forms e le attività relative ai moduli che è possibile eseguire con il servizio Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Forms Service,PDF Generator
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 1e7aa0fa-4440-42fb-8e0b-3c757568b78f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Servizio Forms {#forms-service}

## Panoramica {#overview}

Il servizio Forms consente di creare applicazioni client di acquisizione dati interattive per la convalida, l&#39;elaborazione, la trasformazione e la distribuzione di moduli generalmente creati in Designer. Il servizio Forms esegue il rendering come documenti di PDF di qualsiasi struttura di modulo sviluppata.

Il servizio Forms consente inoltre alle organizzazioni di estendere i processi di acquisizione dati intelligente distribuendo moduli elettronici come PDF di Adobe. Puoi anche utilizzare il servizio per importare ed esportare dati rispettivamente da e verso PDF forms esistenti.

Utilizza il servizio Forms per effettuare le seguenti operazioni:

* Esegui il rendering di PDF forms in base a modelli e dati XML.
* Abilita l’integrazione dei dati del modulo per importare ed estrarre dati da PDF forms.
* Eseguire il rendering dei moduli basati su frammenti.

## Creazione di PDF forms  {#creating-pdf-forms-nbsp}

Utilizza il servizio Form per creare PDF forms per l’acquisizione dei dati. In genere, si inizia con un modello Designer di AEM Forms. Utilizzare l&#39;operazione `renderPDFForm` (collegamento a Javadoc) del servizio Forms per convertire il modello in un modulo PDF.

Il primo parametro dell&#39;operazione `renderPDFForm` è il nome del file modello, ad esempio `ExpenseClaim.xdp`. È possibile memorizzare il file modello in un file system locale, in un repository CRX oppure in un percorso HTTP o FTP. È possibile specificare il percorso del file modello impostando la directory principale del contenuto nel parametro `PDFFormRenderOptions` dell&#39;operazione `renderPDFForm`. Per informazioni dettagliate sulle altre opzioni che è possibile specificare per il parametro `PDFFormRenderOptions`, vedere JavaScript.

L&#39;operazione `renderPDFForm` può accettare anche dati XML. I dati XML vengono uniti al modello durante la creazione di un PDF Form in modo che il modulo PDF generato contenga i dati specificati. Il secondo parametro per l&#39;operazione `renderPDFForm` può accettare un oggetto Document (Javadoc) contenente dati XML.

## Estrazione di dati da PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Utilizzare l&#39;operazione `exportData` (Javadoc) del servizio Forms per estrarre dati XML da un modulo di PDF. Questa operazione accetta un documento come primo parametro. È possibile esportare i dati come documento XDP o come file XML. Se si esportano i dati come file XML, i dati esportati rimuovono l&#39;inviluppo XDP e restituiscono un file XML normale. Potete specificare questa disposizione utilizzando il secondo parametro.

## Importazione di dati in PDF forms {#importing-data-into-pdf-forms}

Il servizio Forms consente inoltre di unire un modulo PDF creato con AEM Forms Designer o l&#39;operazione `renderPDFForm` con dati XML. L&#39;operazione `importData` (Javadoc) del servizio Forms accetta il modulo PDF e i dati XML e restituisce un modulo PDF con dati XML.

## Rendering di moduli basati su frammenti {#rendering-forms-based-on-fragments}

Il servizio Forms può eseguire il rendering dei moduli in base ai frammenti creati con AEM Forms Designer. Un frammento è una parte riutilizzabile di un modulo. Viene salvato come file XDP separato che può essere inserito in più progettazioni di moduli. Ad esempio, un frammento può includere un blocco di indirizzi o un testo legale.

L’utilizzo di frammenti semplifica e accelera la creazione e la gestione di un numero elevato di moduli. Durante la creazione di un modulo, inserisci un riferimento al frammento richiesto affinché venga visualizzato nel modulo. Il riferimento al frammento contiene un sottomodulo che punta al file XDP fisico.

Di seguito sono riportati i vantaggi dell’utilizzo dei frammenti:

* **Riutilizzo del contenuto**: è possibile riutilizzare il contenuto in più progettazioni di moduli. Per riutilizzare rapidamente parti dello stesso contenuto in più moduli, crea un frammento. La copia o la ricreazione del contenuto richiede più tempo. L’utilizzo dei frammenti assicura inoltre che le parti utilizzate di frequente di una progettazione di moduli abbiano contenuto e aspetto coerenti in tutti i moduli di riferimento.
* **Aggiornamenti globali**: è possibile apportare modifiche globali a più moduli una sola volta in un file. Puoi modificare il contenuto, gli oggetti script, le associazioni di dati, il layout o gli stili in un frammento. Tutti i moduli XDP che fanno riferimento al frammento riflettono le modifiche.
* **Creazione di moduli condivisi**: è possibile condividere la creazione di moduli tra diverse risorse. Gli sviluppatori di moduli con esperienza nello scripting o altre funzioni avanzate di AEM Forms Designer possono sviluppare e condividere frammenti che utilizzano script e proprietà dinamiche. I progettisti di moduli possono utilizzare i frammenti per progettare i moduli. Inoltre, possono utilizzare i frammenti per garantire che tutte le parti di un modulo abbiano un aspetto e una funzionalità coerenti tra più moduli.
