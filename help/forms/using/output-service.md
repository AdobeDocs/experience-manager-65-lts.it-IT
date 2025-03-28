---
title: Servizio di output
description: Descrive il servizio di output, parte di AEM Document Services
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Output Service
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: de7b8970-bbac-419b-8e87-8d853b82f44a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---

# Servizio di output{#output-service}

## Panoramica {#overview}

Il servizio di output è un servizio OSGi incluso in AEM Document Services. Il servizio di output supporta vari formati di output e funzioni di progettazione dell’output di AEM Forms Designer. Il servizio di output può convertire modelli XFA e dati XML per generare documenti di stampa in vari formati.

Il servizio di output consente di creare applicazioni che permettono di:

* Generare i documenti compilando i file modello con dati XML.
* Genera moduli di output in vari formati, inclusi flussi di stampa non interattivi PDF, PostScript, PCL e ZPL.
* Generare PDF di stampa da PDF modulo XFA.
* Generare in blocco documenti PDF, PostScript, PCL e ZPL unendo più set di dati con i modelli forniti.

>[!NOTE]
>
>Il servizio di output è un&#39;applicazione a 32 bit. In Microsoft Windows, un&#39;applicazione a 32 bit può utilizzare un massimo di 2 GB di memoria. Il limite si applica anche al servizio di output.

## Creazione di documenti modulo non interattivi {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

In genere, si creano modelli utilizzando AEM Forms Designer. Le API `generatePDFOutput` e `generatePrintedOutput` del servizio di output consentono di convertire direttamente questi modelli in vari formati, inclusi PDF, PostScript, ZPL e PCL.

L&#39;operazione `generatePDFOutput` genera PDF, mentre l&#39;operazione `generatePrintedOutput` genera formati PostScript, ZPL e PCL. Il primo parametro di entrambe le operazioni accetta il nome del file modello (ad esempio, `ExpenseClaim.xdp`) o un oggetto Document contenente il modello. Quando si specifica il nome del file modello, specificare anche la directory principale del contenuto come percorso della cartella che contiene il modello. È possibile specificare la directory principale del contenuto utilizzando il parametro `PDFOutputOptions` o `PrintedOutputOptions`. Consulta JavaScript per informazioni dettagliate su altre opzioni che puoi specificare utilizzando questi parametri.

Il secondo parametro accetta un documento XML che viene unito al modello durante la generazione del documento di output.

L&#39;operazione `generatePDFOutput` può inoltre accettare un modulo PDF basato su XFA come input e restituire una versione non interattiva del modulo PDF come output.

## Generazione di documenti modulo non interattivi {#generating-non-interactive-form-documents}

Si consideri uno scenario in cui sono presenti uno o più modelli e più record di dati XML per ciascun modello.

Utilizzare le operazioni `generatePDFOutputBatch` e `generatePrintedOutputBatch` del servizio di output per generare un documento di stampa per ogni record.

È inoltre possibile combinare i record in un unico documento. Entrambe le operazioni richiedono quattro parametri.

Il primo parametro è una mappa che contiene una stringa arbitraria come chiave e il nome del file modello come valore.

Il secondo parametro è un mapping diverso il cui valore è un oggetto Document contenente dati XML. La chiave è la stessa di quella specificata per il primo parametro.

Il terzo parametro per `generatePDFOutputBatch` o `generatePrintedOutputBatch` è rispettivamente di tipo `PDFOutputOptions` o `PrintedOutputOptions`.

I tipi di parametri sono gli stessi dei tipi dei parametri per le operazioni `generatePDFOutput` e `generatePrintedOutput` e hanno lo stesso effetto.

Il quarto parametro è di tipo `BatchOptions`, utilizzato per specificare se è possibile generare un file separato per ogni record. Il valore predefinito di questo parametro è false.

Sia `generatePrintedOutputBatch` che `generatePDFOutputBatch` restituiscono un valore di tipo `BatchResult`. Il valore contiene un elenco di documenti generati. Contiene inoltre un documento di metadati in formato XML che contiene informazioni relative a ciascun documento generato.
