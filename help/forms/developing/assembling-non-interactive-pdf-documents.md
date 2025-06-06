---
title: Assemblaggio di documenti PDF non interattivi
description: Utilizza un modulo PDF non interattivo come input per assemblare un documento PDF non interattivo utilizzando l’API Java e l’API del servizio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
hidefromtoc: true
exl-id: fc5ea2a6-79b4-436e-b5bc-c4beaf3619ee
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Assemblaggio di documenti PDF non interattivi {#assembling-non-interactive-pdf-documents}

È possibile assemblare un documento PDF non interattivo quando si utilizza come input un modulo PDF interattivo. Si supponga di disporre di un modulo che gli utenti possono utilizzare per immettere dati nei relativi campi. È possibile passare tale modulo al servizio Assembler, in modo che quest&#39;ultimo restituisca un documento di PDF che impedisce agli utenti di immettere dati nei propri campi. Questo documento è un modulo PDF non interattivo. Nell&#39;illustrazione seguente, ad esempio, viene illustrata un&#39;applicazione ipotecaria che rappresenta un modulo interattivo.

Ai fini della presente discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

All&#39;interno di questo documento DDX, si noti che all&#39;attributo di origine viene assegnato il valore `inDoc`. Nelle situazioni in cui viene passato un solo documento PDF di input al servizio Assembler e viene restituito un documento PDF e si richiama l&#39;operazione `invokeOneDocument`, assegnare il valore `inDoc` all&#39;attributo di origine di PDF. Quando si richiama l&#39;operazione `invokeOneDocument`, il valore `inDoc` è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si trasmettono due o più documenti PDF di input al servizio Assembler, è possibile richiamare l&#39;operazione `invokeDDX`. In questa situazione, assegnare il nome file del documento PDF di input all&#39;attributo `source`.

Questo documento DDX contiene l&#39;elemento `NoXFA`, che indica al servizio Assembler di restituire un documento PDF non interattivo.

Il servizio Assembler può assemblare documenti PDF non interattivi senza che il servizio di output faccia parte dell’installazione di AEM Forms se il documento PDF di input è basato su un modulo Acrobat o su un modulo XFA statico. Tuttavia, se il documento PDF di input è un modulo XFA dinamico, il servizio di output deve far parte dell’installazione di AEM Forms. Se il servizio di output non fa parte dell’installazione di AEM Forms quando viene assemblato un modulo XFA dinamico, viene generata un’eccezione. Vedere [Creazione di flussi di output del documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti concetti quali la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento dell&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (Vedere [Assemblaggio di documenti di PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF non interattivo, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler di PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento a un documento interattivo di PDF.
1. Impostare le opzioni di runtime.
1. Assemblare il documento PDF.
1. Salvare il documento non interattivo di PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms.

**Creare un client Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39;elemento `NoXFA`, che indica al servizio Assembler di restituire un documento PDF non interattivo.

**Riferimento a un documento interattivo di PDF**

È necessario fare riferimento a un documento PDF interattivo e passarlo al servizio Assembler per recuperare un documento PDF non interattivo.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il documento PDF**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX, aver fatto riferimento a un documento PDF interattivo e aver impostato le opzioni di runtime, è possibile richiamare l&#39;operazione `invokeOneDocument`. Poiché al servizio Assembler viene passato un solo documento PDF di input e viene restituito un singolo documento, è possibile utilizzare l&#39;operazione `invokeOneDocument` anziché l&#39;operazione `invokeDDX`.

**Salvare il documento non interattivo di PDF**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto insieme. In altre parole, quando si richiama l&#39;operazione `invokeOneDocument`, viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene istruzioni per la creazione di un documento PDF non interattivo, il servizio Assembler restituisce un documento PDF non interattivo che può essere salvato come file PDF.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF non interattivo utilizzando l’API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assembla un documento PDF non interattivo utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento a un documento interattivo di PDF.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando il percorso di un documento PDF interattivo.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF. L&#39;oggetto `com.adobe.idp.Document` è passato al metodo `invokeOneDocument`.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assemblare il documento PDF.

   Richiama il metodo `invokeOneDocument` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX. Verificare che il documento DDX contenga il valore `inDoc` per l&#39;elemento di origine PDF.
   * Oggetto `com.adobe.idp.Document` contenente il documento PDF interattivo.
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello del registro dei processi.

   Il metodo `invokeOneDocument` restituisce un oggetto `com.adobe.idp.Document` che contiene un documento PDF non interattivo.

1. Salvare il documento non interattivo di PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `invokeOneDocument`.

* &quot;Guida rapida (modalità SOAP): assemblaggio di un documento PDF non interattivo tramite l’API Java&quot;

## Assemblare un documento PDF non interattivo utilizzando l’API del servizio web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assemblare un documento PDF non interattivo utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente di AEM Forms al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Fai riferimento a un documento interattivo di PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` è passato a `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare il documento PDF.

   Richiama il metodo `invokeOneDocument` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX
   * Oggetto `BLOB` che rappresenta il documento interattivo di PDF
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeOneDocument` restituisce un oggetto `BLOB` che contiene un documento PDF non interattivo.

1. Salvare il documento non interattivo di PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF non interattivo e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `invokeOneDocument`. Compilare la matrice di byte ottenendo il valore del campo `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

* &quot;Guida rapida (MTOM): assemblaggio di un documento PDF non interattivo tramite l’API del servizio web&quot;.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
