---
title: Conversione di file con PDF Generator
description: Il servizio PDF Generator converte i formati di file nativi in PDF. Converte inoltre PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1d2adc53-498f-43f5-b664-0b9dd864b9a1
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# Conversione di file con PDF Generator{#converting-files-using-pdf-generator}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

È possibile utilizzare le pagine Web di PDF Generator per convertire i file.

## Creazione di un file PDF {#create-a-pdf-file}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Crea PDF.
1. Fare clic su Sfoglia per trovare e selezionare il file.

   >[!NOTE]
   >
   >PDF Generator è in grado di rilevare automaticamente il tipo di file con estensione doc, xls, ppt e rtf, anche quando nel nome del file manca l&#39;estensione. Questa funzionalità non funziona con i file docx, xlsx e pptx.

1. In Impostazioni di configurazione, selezionare Usa impostazioni personalizzate o Carica file impostazioni.

   * Se utilizzi impostazioni personalizzate, seleziona un’impostazione Adobe PDF, un’impostazione di sicurezza e un’impostazione del tipo di file, quindi specifica un timeout.

     Le impostazioni di Adobe PDF sono applicabili solo alle conversioni PS-to-PDF, EPS-to-PDF, PRN-to-PDF, Image-to-PDF con OCR e Native-to-PDF. L’impostazione di timeout specifica il tempo massimo necessario per il completamento della conversione. Il valore predefinito è 270 secondi. Queste impostazioni non vengono utilizzate durante le conversioni da Image a PDF e da OpenOffice a PDF.

   * Se si sta caricando un file di impostazioni, digitarne il percorso e il nome nella casella oppure fare clic su Sfoglia per trovare e selezionare il file.

1. (Facoltativo) In File metadati XMP digitare il percorso e il nome del file XMP oppure fare clic su Sfoglia per individuare e selezionare il file. Un file XMP può essere utilizzato per includere informazioni sui metadati standard. (Vedi [Informazioni sui file XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Fai clic su Crea. Quando il file viene creato, viene visualizzato un collegamento. Se si verifica un errore durante la conversione, viene visualizzato un avviso. Se si sta creando un file Postscript, l&#39;avviso contiene anche un collegamento al file di registro.
1. Fai clic sul collegamento del file PDF. Il file viene aperto in Acrobat.

### Informazioni sui file XMP {#about-xmp-files}

I documenti PDF creati da PDF Generator in Acrobat 5.0 o versione successiva contengono metadati di documento in formato XML. *Metadati* include informazioni sul documento e sul relativo contenuto, ad esempio il nome dell&#39;autore, le parole chiave e le informazioni sul copyright utilizzabili dalle utilità di ricerca.

I metadati del documento contengono (ma non sono limitati a) informazioni che vengono visualizzate anche nella scheda Descrizione della finestra di dialogo Proprietà documento in Acrobat. Le modifiche apportate nella scheda Descrizione vengono riportate nei metadati del documento. I metadati dei documenti possono essere estesi e modificati utilizzando prodotti di terze parti.

Adobe Extensible Metadata Platform (XMP) fornisce alle applicazioni Adobe un framework XML comune che standardizza la creazione, l’elaborazione e lo scambio di metadati dei documenti tra i flussi di lavoro di pubblicazione. È possibile salvare e importare il codice sorgente XML dei metadati del documento in formato XMP, semplificando la condivisione dei metadati tra vari documenti. Per ulteriori informazioni sui file di XMP, vedere [Piattaforma metadati estensibile (XMP)](https://www.adobe.com/products/xmp/) e [Centro sviluppatori Adobe XMP](https://www.adobe.com/devnet/xmp.html).

Puoi creare file XMP in Acrobat.

## Convertire un file HTML o ZIP in PDF {#convert-an-html-file-or-zip-file-to-pdf}

Puoi utilizzare PDF Generator per convertire in Adobe PDF i seguenti tipi di file:

* File HTML, che è possibile convertire caricando un file HTML o specificando l&#39;URL di una pagina Web o di un sito Web.
* File archiviati (ZIP), che possono contenere file HTML, file immagine o entrambi.

Se il file ZIP contiene più di un file HTML al livello più basso della gerarchia delle cartelle, il file ZIP deve contenere anche un file index.htm o index.html.

>[!NOTE]
>
>* La funzione da HTML a PDF richiede alcuni tipi di carattere nella directory dei caratteri di sistema. Nei sistemi Linux, Solaris e AIX, la directory dei font di sistema deve contenere il font Courier. Nei sistemi Windows, la directory dei caratteri di sistema deve contenere Times New Roman.
>
>* (Solo sistemi basati su UNIX) Per convertire una pagina Web con caratteri giapponesi in un documento PDF, nel server AEM Forms deve essere disponibile uno dei seguenti caratteri giapponesi.
>
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;Sazanami Mincho&quot;
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;
>
>* Per caricare un file dal file system locale, utilizzare l&#39;opzione Carica file nella pagina HTML in PDF.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Da HTML a PDF.
1. Specificare il file da convertire eseguendo una delle operazioni seguenti:

   * In Carica file digitare il percorso e il nome del file HTML o ZIP oppure fare clic su Sfoglia per individuarlo e selezionarlo.
   * Nella casella Specifica URL digitare l&#39;URL della pagina o del sito Web da convertire.

   >[!NOTE]
   >
   >Il file che si sta convertendo deve avere l&#39;estensione html, htm o zip.

1. Specificare le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, seleziona Usa impostazioni personalizzate, specifica le impostazioni di sicurezza e del tipo di file, quindi specifica un valore di timeout. Il valore predefinito è 270 secondi.

   >[!NOTE]
   >
   >Se il servizio Generate PDF è stato configurato per l&#39;utilizzo di Acrobat WebCapture, le impostazioni dei tipi di file selezionate in questa pagina non influiscono sul PDF prodotto. Apporta invece le modifiche appropriate alla versione di Acrobat installata sul server.

   * Per utilizzare un file di impostazioni esistente, selezionare Carica file di impostazioni e fare clic su Sfoglia per passare al percorso del file.

1. Per caricare un file XMP, fai clic su Sfoglia e vai al percorso del file. Un file XMP può essere utilizzato per includere informazioni sui metadati standard. (Vedi [Informazioni sui file XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Fai clic su Crea. Al momento della creazione del file, viene visualizzato un collegamento al file PDF.
1. Fai clic sul collegamento per visualizzare il documento PDF in Acrobat.

## Esportare un file PDF in un altro formato (solo Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

È possibile esportare i file PDF in vari formati di file, come descritto nel capitolo Generate PDF Service di [Services Reference](https://www.adobe.com/go/learn_aemforms_services_63).

1. In console di amministrazione, fai clic su Servizi > PDF Generator > Export PDF.
1. Fare clic su Sfoglia per individuare il file PDF da esportare.
1. Nell&#39;elenco File Export PDF da selezionare il formato in cui esportare il file PDF.
1. Nella casella Specificare un timeout immettere il tempo di attesa prima del timeout dell&#39;applicazione. Il valore predefinito è 270 secondi.

   Il tempo di conversione visualizzato quando il file viene convertito potrebbe essere maggiore del valore specificato in questo campo. Il Tempo di conversione include il tempo trascorso in attesa del thread o del processo, il tempo impiegato per convertire il file e il tempo impiegato dal convertitore di fallback (se applicabile). tempo. Il valore di Specifica timeout corrisponde al tempo necessario per convertire il file.

1. (Facoltativo) Nell&#39;opzione **Specifica profilo verifica preliminare personalizzato**, fare clic su Sfoglia e selezionare un [profilo verifica preliminare personalizzato](https://helpx.adobe.com/it/acrobat/using/preflight-profiles-acrobat-pro.html). I profili di verifica preliminare vengono utilizzati solo durante la conversione di documenti in formato archivio PDF (PDF/A).
1. Fai clic su Esporta. Al termine della conversione, viene visualizzato un collegamento al file esportato.
1. Fai clic sul collegamento per visualizzare il file convertito.

## Ottimizzare un PDF (solo Windows) {#optimize-a-pdf}

PDF Generator supporta la riduzione delle dimensioni dei file PDF.

>[!NOTE]
>
>L&#39;ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Ottimizza PDF.
1. Fare clic su Sfoglia per individuare il file PDF da ottimizzare.
1. Specificare le impostazioni di configurazione:

   * Per utilizzare le impostazioni personalizzate, seleziona Usa impostazioni personalizzate, specifica le impostazioni del tipo di file e specifica un valore di timeout. Il valore predefinito è 270 secondi.
   * Per utilizzare un file di impostazioni esistente, selezionare Carica file di impostazioni e fare clic su Sfoglia per passare al percorso del file.

1. Fai clic su Crea.
