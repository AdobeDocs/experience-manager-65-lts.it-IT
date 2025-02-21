---
title: Utilizzo delle utilità di XMP
description: Utilizza le API Java e Web Service di XMP Utilities per importare in modo programmatico i metadati di XMP in un documento PDF e recuperare e salvare i metadati di XMP da un documento PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Utilizzo delle utilità di XMP {#working-with-xmp-utilities}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Utilità di XMP**

I documenti di PDF contengono metadati, ovvero informazioni sul documento distinte dal contenuto del documento, ad esempio testo e grafica. Adobe Extensible Metadata Platform (XMP) è uno standard per la gestione dei metadati dei documenti.

Il servizio Utilità XMP consente di recuperare e salvare i metadati XMP dai documenti PDF e di importare i metadati XMP nei documenti PDF.

Puoi eseguire queste attività utilizzando il servizio Utilità XMP:

* Importare i metadati nei documenti di PDF. (Vedi [Importazione dei metadati nei documenti di PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Esporta metadati da documenti PDF. (Vedi [Esportazione dei metadati dai documenti di PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione dei metadati nei documenti di PDF {#importing-metadata-into-pdf-documents}

Puoi utilizzare le API Java e dei servizi web di XMP Utilities per importare in modo programmatico i metadati XMP in un documento PDF. I metadati forniscono informazioni su un documento di PDF, ad esempio l&#39;autore del documento e le parole chiave correlate al documento. I metadati possono essere visualizzati nella finestra di dialogo Proprietà documento del documento, come illustrato nella figura seguente.

![ww_ww_metadata](assets/ww_ww_metadatadialog.png)

Per importare in modo programmatico i metadati in un documento di PDF, è possibile utilizzare un documento XML esistente che specifica i valori dei metadati oppure un oggetto di tipo `XMPUtilityMetadata`. (Vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>In questa sezione viene illustrato come utilizzare un documento XML per importare metadati in un documento PDF.

Il codice XML riportato di seguito contiene i valori dei metadati corrispondenti all&#39;illustrazione precedente. Ad esempio, notate gli elementi in grassetto, che specificano le parole chiave.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare i metadati di XMP in un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client XMPUtilityService.
1. Richiama l’operazione di importazione dei metadati di XMP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di poter eseguire un&#39;operazione di Utilità XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con l&#39;API Java, questo viene ottenuto creando un oggetto `XMPUtilityServiceClient`. Con l&#39;API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `XMPUtilityServiceService`.

**Richiama l&#39;operazione di importazione metadati XMP**

Dopo aver creato il client del servizio, è possibile richiamare una delle operazioni di importazione dei metadati di XMP per importare i metadati di XMP nel documento di PDF specificato.

**Consulta anche**

[Importare metadati XMP tramite API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione dei metadati di XMP tramite l’API del servizio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare metadati XMP tramite API Java {#import-xmp-metadata-using-the-java-api}

Importa i metadati di XMP utilizzando l’API XMP Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare a livello di programmazione il servizio Utilità XMP.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama l’operazione di importazione dei metadati XMP

   Per modificare i metadati di XMP, richiamare il metodo `importMetadata` dell&#39;oggetto `XMPUtilityServiceClient` o il relativo metodo `importXMP`.

   Se si utilizza il metodo `importMetadata`, passare i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il file PDF.
   * Oggetto `XMPUtilityMetadata` contenente i metadati da importare.

   Se si utilizza il metodo `importXMP`, passare i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il file PDF.
   * Oggetto `com.adobe.idp.Document` che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un oggetto `com.adobe.idp.Document` che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto su disco.

**Consulta anche**

[Importazione dei metadati nei documenti di PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importazione dei metadati di XMP tramite l’API del servizio web {#importing-xmp-metadata-using-the-web-service-api}

Per importare in modo programmatico i metadati di XMP utilizzando l’API del servizio web XMP Utilities, esegui le seguenti attività:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del servizio Utilità XMP. (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceService` utilizzando il costruttore di classe proxy.

1. Richiama l’operazione di importazione dei metadati XMP

   Per modificare i metadati di XMP, richiamare il metodo `importMetadata` dell&#39;oggetto `XMPUtilityServiceService` o il relativo metodo `importXMP`.

   Se si utilizza il metodo `importMetadata`, passare i seguenti valori:

   * Oggetto `BLOB` che rappresenta il file PDF.
   * Oggetto `XMPUtilityMetadata` contenente i metadati da importare.

   Se si utilizza il metodo `importXMP`, passare i seguenti valori:

   * Oggetto `BLOB` che rappresenta il file PDF.
   * Oggetto `BLOB` che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un oggetto `BLOB` che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto su disco.

**Consulta anche**

[Importazione dei metadati nei documenti di PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Esportazione di metadati da documenti PDF {#exporting-metadata-from-pdf-documents}

Puoi utilizzare le API Java e dei servizi web di XMP Utilities per recuperare e salvare a livello di programmazione i metadati di XMP da un documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i metadati di XMP da un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client XMPUtilityService.
1. Richiama l’operazione di esportazione dei metadati di XMP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di poter eseguire un&#39;operazione di Utilità XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con il punto di accesso Java, questo viene ottenuto creando un oggetto `XMPUtilityServiceClient`. Con l&#39;API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `XMPUtilityServiceService`.

**Richiama l&#39;operazione di esportazione dei metadati di XMP**

Dopo aver creato il client del servizio, è possibile richiamare una delle operazioni di esportazione dei metadati di XMP, che può essere utilizzata per esaminare i metadati di XMP o salvarli su disco.

**Consulta anche**

[Importare metadati XMP tramite API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione dei metadati di XMP tramite l’API del servizio web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i metadati di XMP utilizzando l’API Java {#export-xmp-metadata-using-the-java-api}

Esportare i metadati di XMP utilizzando l’API XMP Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare a livello di programmazione il servizio Utilità XMP.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama l’operazione di importazione dei metadati XMP

   Per verificare i metadati di XMP, richiamare il metodo `exportMetadata` dell&#39;oggetto `XMPUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `XMPUtilityMetadata` contenente i metadati recuperati.

   Per recuperare e salvare i metadati di XMP, richiamare il metodo `exportXMP` dell&#39;oggetto `XMPUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` contenente i metadati recuperati, che è possibile salvare successivamente su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i metadati di XMP utilizzando l’API del servizio web {#export-xmp-metadata-using-the-web-service-api}

Esporta i metadati di XMP utilizzando l’API XMP Utilities (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il file WSDL del servizio Utilità XMP.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceService` utilizzando il costruttore di classe proxy.

1. Richiama l’operazione di importazione dei metadati XMP

   Per verificare i metadati di XMP, richiamare il metodo `exportMetadata` dell&#39;oggetto `XMPUtilityServiceClient` e passare un oggetto `BLOB` che rappresenta il file PDF. Il metodo restituisce un oggetto `XMPUtilityMetadata` contenente i metadati recuperati.

   Per recuperare e salvare i metadati di XMP, richiamare il metodo `exportXMP` dell&#39;oggetto `XMPUtilityServiceClient` e passare un oggetto `BLOB` che rappresenta il file PDF. Il metodo restituisce un oggetto `BLOB` contenente i metadati recuperati, che è possibile salvare successivamente su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
