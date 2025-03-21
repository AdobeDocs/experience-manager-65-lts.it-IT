---
title: Richiamare AEM Forms tramite servizi Web
description: Richiama i processi AEM Forms utilizzando i servizi web con supporto completo per la generazione WSDL.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations, AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: ca620313-8c2c-44e6-9f29-0d91dc9f6e03
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '9814'
ht-degree: 0%

---

# Richiamare AEM Forms tramite servizi Web {#invoking-aem-forms-using-web-services}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

La maggior parte dei servizi AEM Forms nel contenitore di servizi è configurata per esporre un servizio Web, con supporto completo per la generazione WSDL (Web Service Definition Language). In altre parole, puoi creare oggetti proxy che utilizzano lo stack SOAP nativo di un servizio AEM Forms. Di conseguenza, i servizi AEM Forms possono scambiare ed elaborare i seguenti messaggi SOAP:

* **Richiesta SOAP**: inviata a un servizio Forms da un&#39;applicazione client che richiede un&#39;azione.
* **Risposta SOAP**: inviata a un&#39;applicazione client da un servizio Forms dopo l&#39;elaborazione di una richiesta SOAP.

Utilizzando i servizi web, puoi eseguire le stesse operazioni dei servizi AEM Forms possibili utilizzando l’API Java. Un vantaggio dell’utilizzo dei servizi web per richiamare i servizi AEM Forms è la possibilità di creare un’applicazione client in un ambiente di sviluppo che supporta SOAP. Un&#39;applicazione client non è associata a un ambiente di sviluppo o a un linguaggio di programmazione specifico. È ad esempio possibile creare un&#39;applicazione client utilizzando Microsoft Visual Studio .NET e C# come linguaggio di programmazione.

I servizi AEM Forms sono esposti tramite il protocollo SOAP e sono compatibili con WSI Basic Profile 1.1. Web Services Interoperability (WSI) è un&#39;organizzazione di standard aperti che promuove l&#39;interoperabilità dei servizi web su più piattaforme. Per informazioni, vedere [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms supporta i seguenti standard di servizi web:

* **Codifica**: supporta solo la codifica letterale e del documento (che è la codifica preferita in base al profilo di base WSI). (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: rappresenta un modo per codificare gli allegati con le richieste SOAP. (Vedi [Chiamata di AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: rappresenta un altro modo per codificare gli allegati con le richieste SOAP. (Vedi [Chiamata di AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref).)
* **SOAP con allegati**: supporta sia MIME che DIME (Direct Internet Message Encapsulation). Questi protocolli sono metodi standard per l’invio di allegati tramite SOAP. Le applicazioni Microsoft Visual Studio .NET utilizzano DIME. (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: supporta un profilo token password nome utente, che è un metodo standard per inviare nomi utente e password come parte dell&#39;intestazione SOAP di WS Security. AEM Forms supporta anche l’autenticazione HTTP di base. s

Per richiamare i servizi AEM Forms utilizzando un servizio Web, in genere si crea una libreria proxy che utilizza il servizio WSDL. La sezione *Richiamo di AEM Forms tramite Web Services* utilizza JAX-WS per creare classi proxy Java per richiamare i servizi. (Vedi [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

È possibile recuperare un servizio WDSL specificando la seguente definizione di URL (gli elementi tra parentesi sono facoltativi):

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

Dove:

* *il_serverhost* rappresenta l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms.
* *la porta* rappresenta la porta HTTP utilizzata dal server applicazioni J2EE.
* *service_name* rappresenta il nome del servizio.
* *versione* rappresenta la versione di destinazione di un servizio (per impostazione predefinita viene utilizzata la versione più recente del servizio).
* `async` specifica il valore `true` per abilitare operazioni aggiuntive per la chiamata asincrona ( `false` per impostazione predefinita).
* *lc_version* rappresenta la versione di AEM Forms da richiamare.

Nella tabella seguente sono elencate le definizioni del servizio WSDL (supponendo che AEM Forms sia distribuito sull&#39;host locale e che il post sia 8080).

<table>
 <thead>
  <tr>
   <th><p>Servizio</p></th>
   <th><p>Definizione WSDL</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assemblatore</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Indietro e ripristino</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>moduli con codice a barre</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Converti PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Crittografia </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Moduli</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Integrazione dei dati dei moduli</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Genera PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Genera PDF 3D</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Output</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilità PDF </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Estensioni DC Acrobat Reader</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Archivio</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Firma </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilità XMP</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**Definizioni WSDL processo AEM Forms**

Specificare il nome dell&#39;applicazione e il nome del processo all&#39;interno della definizione WSDL per accedere a un WSDL appartenente a un processo creato in Workbench. Si supponga che il nome dell&#39;applicazione sia `MyApplication` e che il nome del processo sia `EncryptDocument`. In questa situazione, specificare la seguente definizione WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Per informazioni sull&#39;esempio `MyApplication/EncryptDocument` di breve durata, vedere [Esempio di breve durata](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>Un&#39;applicazione può contenere una o più cartelle. In questo caso, specificare il nome della cartella nella definizione WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Accesso a nuove funzionalità tramite i servizi Web**

È possibile accedere alle nuove funzionalità del servizio AEM Forms tramite i servizi web. In AEM Forms, ad esempio, è stata introdotta la possibilità di codificare gli allegati utilizzando MTOM. (Vedi [Chiamata di AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)

Per accedere alle nuove funzionalità introdotte in AEM Forms, specifica l&#39;attributo `lc_version` nella definizione WSDL. Ad esempio, per accedere a nuove funzionalità di servizio (incluso il supporto MTOM), specificare la seguente definizione WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Quando si imposta l&#39;attributo `lc_version`, assicurarsi di utilizzare tre cifre. Ad esempio, 9.0.1 è uguale alla versione 9.0.

**Tipo di dati BLOB servizio Web**

I WSDL dei servizi AEM Forms definiscono molti tipi di dati. Uno dei tipi di dati più importanti esposti in un servizio Web è `BLOB`. Questo tipo di dati viene mappato alla classe `com.adobe.idp.Document` quando si utilizzano le API Java di AEM Forms. (Vedi [Trasmissione di dati ai servizi AEM Forms tramite l&#39;API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Un oggetto `BLOB` invia e recupera dati binari (ad esempio, file PDF, dati XML e così via) da e verso i servizi AEM Forms. Il tipo `BLOB` è definito in un WSDL di servizio come segue:

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

I campi `MTOM` e `swaRef` sono supportati solo in AEM Forms. È possibile utilizzare questi nuovi campi solo se si specifica un URL che include la proprietà `lc_version`.

**Fornitura di oggetti BLOB nelle richieste di servizio**

Se un&#39;operazione del servizio AEM Forms richiede un tipo `BLOB` come valore di input, creare un&#39;istanza del tipo `BLOB` nella logica dell&#39;applicazione. Molti degli avvii rapidi del servizio Web in *Programmazione con AEM Form* mostrano come utilizzare un tipo di dati BLOB.

Assegnare i valori ai campi che appartengono all&#39;istanza `BLOB` nel modo seguente:

* **Base64**: per passare i dati come testo codificato in un formato Base64, impostare i dati nel campo `BLOB.binaryData` e impostare il tipo di dati nel formato MIME (ad esempio, `application/pdf`) nel campo `BLOB.contentType`. (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: per passare dati binari in un allegato MTOM, impostare i dati nel campo `BLOB.MTOM`. Questa impostazione allega i dati alla richiesta SOAP utilizzando il framework Java JAX-WS o l’API nativa del framework SOAP. (Vedi [Chiamata di AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: per passare dati binari in un allegato WS-I SwaRef, impostare i dati nel campo `BLOB.swaRef`. Questa impostazione allega i dati alla richiesta SOAP utilizzando il framework Java JAX-WS. (Vedi [Chiamata di AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref).)
* **Allegato MIME o DIME**: per passare dati in un allegato MIME o DIME, allegare i dati alla richiesta SOAP utilizzando l&#39;API nativa del framework SOAP. Impostare l&#39;identificatore dell&#39;allegato nel campo `BLOB.attachmentID`. (Vedi [Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **URL remoto**: se i dati sono ospitati in un server Web e sono accessibili tramite un URL HTTP, impostare l&#39;URL HTTP nel campo `BLOB.remoteURL`. (Vedi [Richiamare AEM Forms utilizzando i dati BLOB su HTTP](#invoking-aem-forms-using-blob-data-over-http).)

**Accesso ai dati negli oggetti BLOB restituiti dai servizi**

Il protocollo di trasmissione per gli oggetti `BLOB` restituiti dipende da diversi fattori, considerati nell&#39;ordine seguente, che vengono interrotti quando viene soddisfatta la condizione principale:

1. **L&#39;URL di destinazione specifica il protocollo di trasmissione**. Se l&#39;URL di destinazione specificato nella chiamata di SOAP contiene il parametro `blob="`*BLOB_TYPE*&quot;, *BLOB_TYPE* determina il protocollo di trasmissione. *BLOB_TYPE* è un segnaposto per base64, dime, mime, http, mtom o swaref.
1. **L&#39;endpoint del servizio SOAP è Smart**. Se si verificano le seguenti condizioni, i documenti di output vengono restituiti utilizzando lo stesso protocollo di trasmissione dei documenti di input:

   * Il parametro dell&#39;endpoint SOAP del servizio Default Protocol for Output Blob Objects è impostato su Smart.

     Per ogni servizio con un endpoint SOAP, la console di amministrazione consente di specificare il protocollo di trasmissione per i BLOB restituiti. (Vedi [guida per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * Il servizio AEM Forms accetta uno o più documenti come input.

1. **L&#39;endpoint del servizio SOAP non è Smart**. Il protocollo configurato determina il protocollo di trasmissione del documento e i dati vengono restituiti nel campo `BLOB` corrispondente. Ad esempio, se l&#39;endpoint SOAP è impostato su DIME, il BLOB restituito si trova nel campo `blob.attachmentID` indipendentemente dal protocollo di trasmissione di qualsiasi documento di input.
1. **Altrimenti**. Se un servizio non accetta il tipo di documento come input, i documenti di output vengono restituiti nel campo `BLOB.remoteURL` tramite il protocollo HTTP.

Come descritto nella prima condizione, puoi garantire il tipo di trasmissione per tutti i documenti restituiti estendendo l’URL dell’endpoint SOAP con un suffisso come segue:

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Ecco la correlazione tra i tipi di trasmissione e il campo da cui si ottengono i dati:

* **Formato Base64**: impostare il suffisso `blob` su `base64` per restituire i dati nel campo `BLOB.binaryData`.
* **Allegato MIME o DIME**: impostare il suffisso `blob` su `DIME` o `MIME` per restituire i dati come tipo di allegato corrispondente con l&#39;identificatore dell&#39;allegato restituito nel campo `BLOB.attachmentID`. Utilizza l’API proprietaria del framework SOAP per leggere i dati dall’allegato.
* **URL remoto**: impostare il suffisso `blob` su `http` per mantenere i dati nel server applicazioni e restituire l&#39;URL che punta ai dati nel campo `BLOB.remoteURL`.
* **MTOM o SwaRef**: impostare il suffisso `blob` su `mtom` o `swaref` per restituire i dati come tipo di allegato corrispondente con l&#39;identificatore dell&#39;allegato restituito nei campi `BLOB.MTOM` o `BLOB.swaRef`. Utilizza l’API nativa del framework SOAP per leggere i dati dall’allegato.

>[!NOTE]
>
>È consigliabile non superare i 30 MB durante il popolamento di un oggetto `BLOB` richiamando il relativo metodo `setBinaryData`. In caso contrario, è possibile che si verifichi un&#39;eccezione `OutOfMemory`.

>[!NOTE]
>
>Le applicazioni JAX basate su WS che utilizzano il protocollo di trasmissione MTOM sono limitate a 25 MB di dati inviati e ricevuti. Questa limitazione è dovuta a un bug in JAX-WS. Se la dimensione combinata dei file inviati e ricevuti supera i 25 MB, utilizza il protocollo di trasmissione SwaRef invece di quello MTOM. In caso contrario, esiste la possibilità di un&#39;eccezione `OutOfMemory`.

**Trasmissione MTOM di array di byte con codifica base64**

Oltre all&#39;oggetto `BLOB`, il protocollo MTOM supporta qualsiasi parametro di matrice di byte o campo di matrice di byte di tipo complesso. Ciò significa che i framework SOAP client che supportano MTOM possono inviare qualsiasi elemento `xsd:base64Binary` come allegato MTOM (invece di un testo con codifica base64). Gli endpoint di AEM Forms SOAP possono leggere questo tipo di codifica di array di byte. Tuttavia, il servizio AEM Forms restituisce sempre un tipo di matrice di byte come testo con codifica base64. I parametri dell&#39;array di byte di output non supportano MTOM.

I servizi AEM Forms che restituiscono una grande quantità di dati binari utilizzano il tipo Document/BLOB anziché il tipo a matrice di byte. Il tipo di documento è molto più efficiente per la trasmissione di grandi quantità di dati.

## Tipi di dati del servizio Web {#web-service-data-types}

Nella tabella seguente sono elencati i tipi di dati Java e viene visualizzato il tipo di dati del servizio Web corrispondente.

<table>
 <thead>
  <tr>
   <th><p>Tipo di dati Java</p></th>
   <th><p>Tipo di dati del servizio Web</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>Il tipo <code>DATE</code>, definito in un WSDL di servizio come segue:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione del servizio AEM Forms accetta un valore <code>java.util.Date</code> come input, l'applicazione client SOAP deve trasmettere la data nel campo <code>DATE.date</code>. L'impostazione del campo <code>DATE.calendar</code> in questo caso causa un'eccezione di runtime. Se il servizio restituisce un <code>java.util.Date</code>, la data viene restituita nel campo <code>DATE.date</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>Il tipo <code>DATE</code>, definito in un WSDL di servizio come segue:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione del servizio AEM Forms accetta un valore <code>java.util.Calendar</code> come input, l'applicazione client SOAP deve trasmettere la data nel campo <code>DATE.caledendar</code>. L'impostazione del campo <code>DATE.date</code> in questo caso causa un'eccezione di runtime. Se il servizio restituisce un <code>java.util.Calendar</code>, la data viene restituita nel campo <code>DATE.calendar</code>. </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p><code>apachesoap:Map</code>, definito in un WSDL di servizio come segue:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>La mappa è rappresentata come una sequenza di coppie chiave/valore.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>Il tipo XML, definito in un WSDL di servizio come segue:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione del servizio AEM Forms accetta un valore <code>org.w3c.dom.Document</code>, passare i dati XML nel campo <code>XML.document</code>.</p><p>L'impostazione del campo <code>XML.element</code> causa un'eccezione di runtime. Se il servizio restituisce un <code>org.w3c.dom.Document</code>, i dati XML vengono restituiti nel campo <code>XML.document</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>Il tipo XML, definito in un WSDL di servizio come segue:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione del servizio AEM Forms richiede un <code>org.w3c.dom.Element</code> come input, passare i dati XML nel campo <code>XML.element</code>.</p><p>L'impostazione del campo <code>XML.document</code> causa un'eccezione di runtime. Se il servizio restituisce un <code>org.w3c.dom.Element</code>, i dati XML vengono restituiti nel campo <code>XML.element</code>.</p></td>
  </tr>
 </tbody>
</table>

## Creazione di classi proxy Java tramite JAX-WS {#creating-java-proxy-classes-using-jax-ws}

È possibile utilizzare JAX-WS per convertire un servizio Forms WSDL in classi proxy Java. Queste classi consentono di richiamare le operazioni dei servizi AEM Forms. Apache Ant consente di creare uno script di build che genera classi proxy Java facendo riferimento a un WSDL del servizio AEM Forms. Per generare i file proxy JAX-WS, effettuare le seguenti operazioni:

1. Installare Apache Ant nel computer client. (Vedi [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Aggiungi la directory bin al percorso della classe.
   * Impostare la variabile di ambiente `ANT_HOME` sulla directory in cui è stata installata Ant.

1. Installare JDK 1.6 o versione successiva.

   * Aggiungi la directory bin JDK al percorso della classe.
   * Aggiungi la directory bin di JRE al percorso della classe. Il contenitore si trova nella directory `[JDK_INSTALL_LOCATION]/jre`.
   * Impostare la variabile di ambiente `JAVA_HOME` sulla directory in cui è stato installato JDK.

   JDK 1.6 include il programma wsimport utilizzato nel file build.xml. JDK 1.5 non include tale programma.

1. Installare JAX-WS nel computer client. (Vedi [API Java per i servizi Web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Utilizza JAX-WS e Apache Ant per generare classi proxy Java. Crea uno script di generazione della formica per eseguire questa attività. Lo script seguente è uno script di generazione Ant di esempio denominato build.xml:

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   In questo script di Ant Build, la proprietà `url` è impostata per fare riferimento al servizio di crittografia WSDL in esecuzione su localhost. Le proprietà `username` e `password` devono essere impostate su un nome utente e una password di AEM Form validi. L&#39;URL contiene l&#39;attributo `lc_version`. Senza specificare l&#39;opzione `lc_version`, non è possibile richiamare nuove operazioni del servizio AEM Forms.

   >[!NOTE]
   >
   >Sostituire `EncryptionService` con il nome del servizio AEM Forms che si desidera richiamare utilizzando le classi proxy Java. Ad esempio, per creare classi proxy Java per il servizio Rights Management, specifica:

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Crea un file BAT per eseguire lo script di generazione della formica. Il seguente comando può trovarsi all’interno di un file BAT responsabile dell’esecuzione dello script di generazione della formica:

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Inserire lo script di generazione ANT nella directory C:\Program Files\Java\jaxws-ri\bin. Lo script scrive i file JAVA in .cartella /classes. Lo script genera file JAVA che possono richiamare il servizio.

1. Creare un pacchetto dei file JAVA in un file JAR. Se stai lavorando su Eclipse, segui questi passaggi:

   * Crea un progetto Java utilizzato per creare un pacchetto dei file proxy JAVA in un file JAR.
   * Crea una cartella di origine nel progetto.
   * Creare un pacchetto `com.adobe.idp.services` nella cartella Source.
   * Selezionare il pacchetto `com.adobe.idp.services`, quindi importare i file JAVA dalla cartella adobe/idp/services nel pacchetto.
   * Se necessario, creare un pacchetto `org/apache/xml/xmlsoap` nella cartella Source.
   * Seleziona la cartella di origine e importa i file JAVA dalla cartella org/apache/xml/xmlsoap.
   * Impostare il livello di conformità del compilatore Java su 5.0 o versione successiva.
   * Crea il progetto.
   * Esporta il progetto come file JAR.
   * Importa questo file JAR nel percorso di classe di un progetto client. Inoltre, importa tutti i file JAR in &lt;Directory di installazione>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >Tutti i servizi Web Java Quick Start (tranne il servizio Forms) in Programmazione con AEM Forms creano file proxy Java utilizzando JAX-WS. Inoltre, tutti i servizi web Java quick start, utilizzare SwaRef. (Vedi [Chiamata di AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref).)

**Consulta anche**

[Creazione di classi proxy Java tramite l’asse Apache](#creating-java-proxy-classes-using-apache-axis)

[Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding)

[Richiamare AEM Forms utilizzando i dati BLOB su HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Richiamare AEM Forms con SwaRef](#invoking-aem-forms-using-swaref)

## Creazione di classi proxy Java tramite l’asse Apache {#creating-java-proxy-classes-using-apache-axis}

È possibile utilizzare lo strumento Apache Axis WSDL2Java per convertire un servizio Forms in classi proxy Java. Queste classi consentono di richiamare le operazioni del servizio Forms. Utilizzando Apache Ant, potete generare i file della libreria Axis da un WSDL di servizio. Puoi scaricare Apache Axis all&#39;URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Gli avvii rapidi del servizio Web associati al servizio Forms utilizzano le classi proxy Java create utilizzando l’asse Apache. Il servizio Web Forms quick starts utilizza anche Base64 come tipo di codifica. (Consulta [Avvio rapido dell&#39;API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

Per generare i file della libreria Java Axis, effettuare le seguenti operazioni:

1. Installare Apache Ant nel computer client. È disponibile all&#39;indirizzo [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Aggiungi la directory bin al percorso della classe.
   * Impostare la variabile di ambiente `ANT_HOME` sulla directory in cui è stata installata Ant.

1. Installare Apache Axis 1.4 sul computer client. È disponibile all&#39;indirizzo [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. Impostare il percorso della classe per l&#39;utilizzo dei file JAR di Axis nel client del servizio Web, come descritto nelle istruzioni di installazione di Axis all&#39;indirizzo [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Utilizzare lo strumento Apache WSDL2Java in Axis per generare classi proxy Java. Crea uno script di generazione della formica per eseguire questa attività. Lo script seguente è uno script di generazione Ant di esempio denominato build.xml:

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   In questo script di Ant Build, la proprietà `url` è impostata per fare riferimento al servizio di crittografia WSDL in esecuzione su localhost. Le proprietà `username` e `password` devono essere impostate su un nome utente e una password di AEM Form validi.

1. Crea un file BAT per eseguire lo script di generazione della formica. Il seguente comando può trovarsi all’interno di un file BAT responsabile dell’esecuzione dello script di generazione della formica:

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   I file JAVA vengono scritti nella cartella C:\JavaFiles come specificato dalla proprietà `output`. Per richiamare correttamente il servizio Forms, importa questi file JAVA nel percorso della classe.

   Per impostazione predefinita, questi file appartengono a un pacchetto Java denominato `com.adobe.idp.services`. È consigliabile inserire questi file JAVA in un file JAR. Quindi importa il file JAR nel percorso della classe dell’applicazione client.

   >[!NOTE]
   >
   >Esistono diversi modi per inserire file .JAVA in un file JAR. Un metodo consiste nell’utilizzare un IDE Java come Eclipse. Creare un progetto Java e un pacchetto `com.adobe.idp.services` (tutti i file JAVA appartengono a questo pacchetto). Importa quindi tutti i file .JAVA nel pacchetto. Infine, esporta il progetto come file JAR.

1. Modificare l&#39;URL nella classe `EncryptionServiceLocator` per specificare il tipo di codifica. Ad esempio, per utilizzare base64, specificare `?blob=base64` per assicurarsi che l&#39;oggetto `BLOB` restituisca dati binari. Nella classe `EncryptionServiceLocator` individuare la seguente riga di codice:

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   e cambiarlo in:

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Aggiungi i seguenti file JAR di Axis al percorso della classe del progetto Java:

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   Questi file JAR si trovano nella directory `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty`.

**Consulta anche**

[Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding)

[Richiamare AEM Forms utilizzando i dati BLOB su HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Richiamare AEM Forms utilizzando la codifica Base64 {#invoking-aem-forms-using-base64-encoding}

È possibile richiamare un servizio AEM Forms utilizzando la codifica Base64. La codifica Base64 codifica gli allegati inviati con una richiesta di chiamata del servizio Web. In altre parole, i dati di `BLOB` sono codificati in Base64, non l&#39;intero messaggio di SOAP.

&quot;Richiamare AEM Forms utilizzando la codifica Base64&quot; viene descritto come richiamare il seguente processo AEM Forms di breve durata denominato `MyApplication/EncryptDocument` utilizzando la codifica Base64.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

### Creazione di un assembly client .NET che utilizza la codifica Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

È possibile creare un assembly client .NET per richiamare un servizio Forms da un progetto Microsoft Visual Studio .NET. Per creare un assembly client .NET che utilizza la codifica base64, effettuare le seguenti operazioni:

1. Crea una classe proxy basata su un URL di chiamata AEM Forms.
1. Creare un progetto Microsoft Visual Studio .NET che produca l&#39;assembly client .NET.

**Creazione di una classe proxy**

È possibile creare una classe proxy utilizzata per creare l&#39;assembly client .NET utilizzando uno strumento che accompagna Microsoft Visual Studio. Il nome dello strumento è wsdl.exe e si trova nella cartella di installazione di Microsoft Visual Studio. Per creare una classe proxy, aprire il prompt dei comandi e passare alla cartella contenente il file wsdl.exe. Per ulteriori informazioni sullo strumento wsdl.exe, vedere la *Guida MSDN*.

Immetti il seguente comando al prompt dei comandi:

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Per impostazione predefinita, questo strumento crea un file CS nella stessa cartella in base al nome del file WSDL. In questa situazione, viene creato un file CS denominato *EncryptDocumentService.cs*. Questo file CS consente di creare un oggetto proxy che consente di richiamare il servizio specificato nell&#39;URL di chiamata.

Modificare l&#39;URL nella classe proxy per includere `?blob=base64` in modo che l&#39;oggetto `BLOB` restituisca dati binari. Nella classe proxy, individua la seguente riga di codice:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

e cambiarlo in:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

La sezione *Richiamo di AEM Forms utilizzando la codifica Base64* utilizza `MyApplication/EncryptDocument` come esempio. Se si sta creando un assembly client .NET per un altro servizio Forms, assicurarsi di sostituire `MyApplication/EncryptDocument` con il nome del servizio.

**Sviluppo dell&#39;assembly client .NET**

Creare un progetto Libreria di classi di Visual Studio che produce un assembly client .NET. Il file CS creato con wsdl.exe può essere importato in questo progetto. Questo progetto genera un file DLL (l&#39;assembly client .NET) che è possibile utilizzare in altri progetti Visual Studio .NET per richiamare un servizio.

1. Avviare Microsoft Visual Studio .NET.
1. Creare un progetto Libreria di classi e denominarlo DocumentService.
1. Importare il file CS creato con wsdl.exe.
1. Nel menu **Progetto**, seleziona **Aggiungi riferimento**.
1. Nella finestra di dialogo Aggiungi riferimento selezionare **System.Web.Services.dll**.
1. Fare clic su **Seleziona** e quindi su **OK**.
1. Compila e genera il progetto.

>[!NOTE]
>
>Questa procedura consente di creare un assembly client .NET denominato DocumentService.dll che è possibile utilizzare per inviare richieste SOAP al servizio `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Assicurarsi di aver aggiunto `?blob=base64` all&#39;URL nella classe proxy utilizzata per creare l&#39;assembly client .NET. In caso contrario, non è possibile recuperare dati binari dall&#39;oggetto `BLOB`.

**Riferimento all&#39;assembly client .NET**

Inserire l&#39;assembly client .NET appena creato nel computer in cui si sta sviluppando l&#39;applicazione client. Dopo aver inserito l&#39;assembly client .NET in una directory, è possibile fare riferimento a esso da un progetto. Fai riferimento anche alla libreria `System.Web.Services` dal progetto. Se non si fa riferimento a questa libreria, non è possibile utilizzare l&#39;assembly client .NET per richiamare un servizio.

1. Nel menu **Progetto**, seleziona **Aggiungi riferimento**.
1. Fare clic sulla scheda **.NET**.
1. Fare clic su **Sfoglia** e individuare il file DocumentService.dll.
1. Fare clic su **Seleziona** e quindi su **OK**.

**Richiamo di un servizio tramite un assembly client .NET che utilizza la codifica Base64**

È possibile richiamare il servizio `MyApplication/EncryptDocument` (creato in Workbench) utilizzando un assembly client .NET che utilizza la codifica Base64. Per richiamare il servizio `MyApplication/EncryptDocument`, effettuare le seguenti operazioni:

1. Creare un assembly client Microsoft .NET che utilizza il servizio WSDL `MyApplication/EncryptDocument`.
1. Creazione di un progetto Microsoft .NET client. Fare riferimento all&#39;assembly client Microsoft .NET nel progetto client. Fare riferimento anche a `System.Web.Services`.
1. Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `MyApplication_EncryptDocumentService` richiamando il relativo costruttore predefinito.
1. Impostare la proprietà `Credentials` dell&#39;oggetto `MyApplication_EncryptDocumentService` con un oggetto `System.Net.NetworkCredential`. All&#39;interno del costruttore `System.Net.NetworkCredential`, specificare un nome utente di AEM Forms e la password corrispondente. Impostare i valori di autenticazione per consentire all&#39;applicazione client .NET di scambiare messaggi SOAP con AEM Forms.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un passaggio di documento PDF al processo `MyApplication/EncryptDocument`.
1. Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
1. Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
1. Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
1. Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `binaryData` al contenuto della matrice di byte.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `MyApplication_EncryptDocumentService` e passando l&#39;oggetto `BLOB` che contiene il documento PDF. Questo processo restituisce un documento PDF crittografato in un oggetto `BLOB`.
1. Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento crittografato con password.
1. Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `invoke` dell&#39;oggetto `MyApplicationEncryptDocumentService`. Popolare la matrice di byte ottenendo il valore del membro dati `binaryData` dell&#39;oggetto `BLOB`.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

### Richiamare un servizio utilizzando le classi proxy Java e la codifica Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

È possibile richiamare un servizio AEM Forms utilizzando le classi proxy Java e Base64. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando le classi proxy Java, effettuare le seguenti operazioni:

1. Creare classi proxy Java utilizzando JAX-WS che utilizza il servizio WSDL `MyApplication/EncryptDocument`. Utilizza il seguente endpoint WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms.*

1. Crea un pacchetto delle classi proxy Java create utilizzando JAX-WS in un file JAR.
1. Includi il file JAR del proxy Java e i file JAR nel seguente percorso:

   &lt;Directory di installazione>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   nel percorso della classe del progetto client Java.

1. Creare un oggetto `MyApplicationEncryptDocumentService` utilizzando il relativo costruttore.
1. Creare un oggetto `MyApplicationEncryptDocument` richiamando il metodo `getEncryptDocument` dell&#39;oggetto `MyApplicationEncryptDocumentService`.
1. Imposta i valori di connessione necessari per richiamare AEM Forms assegnando valori ai seguenti membri dati:

   * Assegnare l&#39;endpoint WSDL e il tipo di codifica al campo `ENDPOINT_ADDRESS_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando la codifica Base64, specificare il seguente valore URL:

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Assegnare l&#39;utente di AEM Forms al campo `USERNAME_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`.
   * Assegnare il valore della password corrispondente al campo `PASSWORD_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`.

   L&#39;esempio di codice seguente mostra questa logica dell&#39;applicazione:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recuperare il documento PDF da inviare al processo `MyApplication/EncryptDocument` creando un oggetto `java.io.FileInputStream` tramite il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
1. Creare una matrice di byte e popolarla con il contenuto dell&#39;oggetto `java.io.FileInputStream`.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Compilare l&#39;oggetto `BLOB` richiamando il relativo metodo `setBinaryData` e passando la matrice di byte. `setBinaryData` dell&#39;oggetto `BLOB` è il metodo da chiamare quando si utilizza la codifica Base64. Consulta Fornitura di oggetti BLOB nelle richieste di servizio.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `MyApplicationEncryptDocument`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF. Il metodo invoke restituisce un oggetto `BLOB` contenente il documento PDF crittografato.
1. Creare una matrice di byte contenente il documento PDF crittografato richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`.
1. Salvare il documento PDF crittografato come file PDF. Scrivere la matrice di byte in un file.

**Consulta anche**

[Guida introduttiva: Richiamare un servizio utilizzando i file proxy Java e la codifica Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Richiamare AEM Forms tramite MTOM {#invoking-aem-forms-using-mtom}

È possibile richiamare i servizi AEM Forms utilizzando il servizio Web standard MTOM. Questo standard definisce il modo in cui i dati binari, ad esempio un documento PDF, vengono trasmessi tramite Internet o Intranet. Una caratteristica di MTOM è l&#39;utilizzo dell&#39;elemento `XOP:Include`. Questo elemento è definito nella specifica XOP (XML Binary Optimized Packaging) per fare riferimento agli allegati binari di un messaggio di SOAP.

La discussione qui riguarda l&#39;utilizzo di MTOM per richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

>[!NOTE]
>
>Il supporto MTOM è stato aggiunto in AEM Forms, versione 9.

>[!NOTE]
>
>Le applicazioni JAX basate su WS che utilizzano il protocollo di trasmissione MTOM sono limitate a 25 MB di dati inviati e ricevuti. Questa limitazione è dovuta a un bug in JAX-WS. Se la dimensione combinata dei file inviati e ricevuti supera i 25 MB, utilizza il protocollo di trasmissione SwaRef invece di quello MTOM. In caso contrario, esiste la possibilità di un&#39;eccezione `OutOfMemory`.

La discussione qui riguarda l&#39;utilizzo di MTOM all&#39;interno di un progetto Microsoft .NET per richiamare i servizi AEM Forms. .NET Framework utilizzato è 3.5 e l&#39;ambiente di sviluppo è Visual Studio 2008. Se nel computer di sviluppo sono installati i miglioramenti dei servizi Web (WSE), rimuoverli. Il framework .NET 3.5 supporta un framework SOAP denominato Windows Communication Foundation (WCF). Quando si richiama AEM Forms utilizzando MTOM, è supportato solo WCF (non WSE).

### Creazione di un progetto .NET che richiama un servizio tramite MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

È possibile creare un progetto Microsoft .NET che possa richiamare un servizio AEM Forms utilizzando i servizi Web. Creare innanzitutto un progetto Microsoft .NET utilizzando Visual Studio 2008. Per richiamare un servizio AEM Forms, crea un riferimento al servizio AEM Forms che desideri richiamare all’interno del progetto. Quando crei un Riferimento servizio, specifica un URL per il servizio AEM Forms:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Sostituire `localhost` con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms. Sostituire `MyApplication/EncryptDocument` con il nome del servizio AEM Forms da richiamare. Ad esempio, per richiamare un’operazione Rights Management, specifica:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

L&#39;opzione `lc_version` garantisce la disponibilità delle funzionalità di AEM Forms, ad esempio MTOM. Senza specificare l&#39;opzione `lc_version`, non è possibile richiamare AEM Forms utilizzando MTOM.

Dopo aver creato un riferimento al servizio, i tipi di dati associati al servizio AEM Forms sono disponibili per l&#39;utilizzo all&#39;interno del progetto .NET. Per creare un progetto .NET che richiami un servizio AEM Forms, effettuare le seguenti operazioni:

1. Creare un progetto .NET utilizzando Microsoft Visual Studio 2008.
1. Nel menu **Progetto**, seleziona **Aggiungi riferimento servizio**.
1. Nella finestra di dialogo **Indirizzo**, specifica il file WSDL per il servizio AEM Forms. Ad esempio,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Fare clic su **Vai** e quindi su **OK**.

### Richiamare un servizio utilizzando MTOM in un progetto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Considerare il processo `MyApplication/EncryptDocument` che accetta un documento PDF non protetto e restituisce un documento PDF crittografato con password. Per richiamare il processo `MyApplication/EncryptDocument` (creato in Workbench) utilizzando MTOM, effettuare le seguenti operazioni:

1. Creazione di un progetto Microsoft .NET.
1. Creare un oggetto `MyApplication_EncryptDocumentClient` utilizzando il relativo costruttore predefinito.
1. Creare un oggetto `MyApplication_EncryptDocumentClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms e il tipo di codifica:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, assicurarsi di specificare `?blob=mtom`.

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms.*

1. Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del membro dati `EncryptDocumentClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
1. Impostare il membro dati `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
1. Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

   * Assegnare il nome utente di AEM Forms al membro dati `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Assegnare il valore della password corrispondente al membro dati `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Assegnare il valore costante `HttpClientCredentialType.Basic` al membro dati `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al membro dati `BasicHttpBindingSecurity.Security.Mode`.

   Nell&#39;esempio di codice riportato di seguito vengono illustrate queste attività.

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF da passare al processo `MyApplication/EncryptDocument`.
1. Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
1. Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
1. Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
1. Compilare l&#39;oggetto `BLOB` assegnando il relativo membro dati `MTOM` al contenuto della matrice di byte.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `MyApplication_EncryptDocumentClient`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF. Questo processo restituisce un documento PDF crittografato in un oggetto `BLOB`.
1. Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
1. Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `invoke`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

>[!NOTE]
>
>La maggior parte delle operazioni dei servizi AEM Forms hanno un avvio rapido MTOM. Puoi visualizzare questi avvii rapidi nella sezione di avvio rapido corrispondente di un servizio. Ad esempio, per visualizzare la sezione Avvio rapido output, vedere [Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulta anche**

[Guida introduttiva: richiamare un servizio utilizzando MTOM in un progetto .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Accesso a più servizi tramite servizi web](#accessing-multiple-services-using-web-services)

[Creazione di un&#39;applicazione Web ASP.NET che richiama un processo di lunga durata incentrato sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Richiamare AEM Forms con SwaRef {#invoking-aem-forms-using-swaref}

È possibile richiamare i servizi di AEM Forms utilizzando SwaRef. Il contenuto dell&#39;elemento XML `wsi:swaRef` viene inviato come allegato all&#39;interno di un corpo di SOAP che memorizza il riferimento all&#39;allegato. Quando si richiama un servizio Forms utilizzando SwaRef, creare classi proxy Java utilizzando l&#39;API Java per servizi Web XML (JAX-WS). (Vedi [API Java per i servizi Web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

Si tratta di richiamare il seguente processo di breve durata di Forms denominato `MyApplication/EncryptDocument` utilizzando SwaRef.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

>[!NOTE]
>
>Supporto di SwaRef aggiunto in AEM Forms

Di seguito viene illustrato come richiamare i servizi Forms utilizzando SwaRef all’interno di un’applicazione client Java. L&#39;applicazione Java utilizza le classi proxy create mediante JAX-WS.

### Richiama un servizio utilizzando i file di libreria JAX-WS che utilizzano SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Per richiamare il processo `MyApplication/EncryptDocument` utilizzando i file proxy Java creati con JAX-WS e SwaRef, effettuare le seguenti operazioni:

1. Creare classi proxy Java utilizzando JAX-WS che utilizza il servizio WSDL `MyApplication/EncryptDocument`. Utilizza il seguente endpoint WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Per informazioni, vedere [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms.*

1. Crea un pacchetto delle classi proxy Java create utilizzando JAX-WS in un file JAR.
1. Includi il file JAR del proxy Java e i file JAR nel seguente percorso:

   &lt;Directory di installazione>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   nel percorso della classe del progetto client Java.

1. Creare un oggetto `MyApplicationEncryptDocumentService` utilizzando il relativo costruttore.
1. Creare un oggetto `MyApplicationEncryptDocument` richiamando il metodo `getEncryptDocument` dell&#39;oggetto `MyApplicationEncryptDocumentService`.
1. Imposta i valori di connessione necessari per richiamare AEM Forms assegnando valori ai seguenti membri dati:

   * Assegnare l&#39;endpoint WSDL e il tipo di codifica al campo `ENDPOINT_ADDRESS_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando la codifica SwaRef, specificare il seguente valore URL:

     ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Assegnare l&#39;utente di AEM Forms al campo `USERNAME_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`.
   * Assegnare il valore della password corrispondente al campo `PASSWORD_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`.

   L&#39;esempio di codice seguente mostra questa logica dell&#39;applicazione:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recuperare il documento PDF da inviare al processo `MyApplication/EncryptDocument` creando un oggetto `java.io.File` tramite il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
1. Creare un oggetto `javax.activation.DataSource` utilizzando il costruttore `FileDataSource`. Passa l&#39;oggetto `java.io.File`.
1. Creare un oggetto `javax.activation.DataHandler` utilizzando il relativo costruttore e passando l&#39;oggetto `javax.activation.DataSource`.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Compilare l&#39;oggetto `BLOB` richiamando il relativo metodo `setSwaRef` e passando l&#39;oggetto `javax.activation.DataHandler`.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `MyApplicationEncryptDocument` e passando l&#39;oggetto `BLOB` che contiene il documento PDF. Il metodo invoke restituisce un oggetto `BLOB` contenente un documento PDF crittografato.
1. Compilare un oggetto `javax.activation.DataHandler` richiamando il metodo `getSwaRef` dell&#39;oggetto `BLOB`.
1. Convertire l&#39;oggetto `javax.activation.DataHandler` in un&#39;istanza `java.io.InputSteam` richiamando il metodo `getInputStream` dell&#39;oggetto `javax.activation.DataHandler`.
1. Scrivere l&#39;istanza `java.io.InputSteam` in un file PDF che rappresenta il documento PDF crittografato.

>[!NOTE]
>
>La maggior parte delle operazioni di assistenza di AEM Forms sono avviate rapidamente con SwaRef. Puoi visualizzare questi avvii rapidi nella sezione di avvio rapido corrispondente di un servizio. Ad esempio, per visualizzare la sezione Avvio rapido output, vedere [Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulta anche**

[Guida introduttiva: Richiamare un servizio utilizzando SwaRef in un progetto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Richiamare AEM Forms utilizzando i dati BLOB su HTTP {#invoking-aem-forms-using-blob-data-over-http}

È possibile richiamare i servizi AEM Forms utilizzando i servizi web e passando i dati BLOB su HTTP. Il passaggio di dati BLOB su HTTP è una tecnica alternativa all’utilizzo della codifica base64, DIME o MIME. È possibile, ad esempio, passare dati tramite HTTP in un progetto Microsoft .NET che utilizza Web Service Enhancement 3.0, che non supporta DIME o MIME. Quando si utilizzano dati BLOB su HTTP, i dati di input vengono caricati prima che venga richiamato il servizio AEM Forms.

&quot;Richiamare AEM Forms utilizzando i dati BLOB su HTTP&quot; illustra come richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument` passando i dati BLOB su HTTP.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

>[!NOTE]
>
>Si consiglia di avere familiarità con la chiamata di AEM Forms tramite SOAP. (Vedi [Chiamata di AEM Forms tramite servizi Web](#invoking-aem-forms-using-web-services).)

### Creazione di un assembly client .NET che utilizza dati tramite HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Per creare un assembly client che utilizza dati tramite HTTP, seguire la procedura specificata in [Richiamare AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding). Tuttavia, modificare l&#39;URL nella classe proxy in modo da includere `?blob=http` anziché `?blob=base64`. Questa azione assicura che i dati vengano trasmessi tramite HTTP. Nella classe proxy, individua la seguente riga di codice:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

e cambiarlo in:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Riferimento all&#39;assembly .NET clienMyApplication/EncryptDocumentt**

Inserire il nuovo assembly client .NET nel computer in cui si sta sviluppando l&#39;applicazione client. Dopo aver inserito l&#39;assembly client .NET in una directory, è possibile fare riferimento a esso da un progetto. Fai riferimento alla libreria `System.Web.Services` dal progetto. Se non si fa riferimento a questa libreria, non è possibile utilizzare l&#39;assembly client .NET per richiamare un servizio.

1. Nel menu **Progetto**, seleziona **Aggiungi riferimento**.
1. Fare clic sulla scheda **.NET**.
1. Fare clic su **Sfoglia** e individuare il file DocumentService.dll.
1. Fare clic su **Seleziona** e quindi su **OK**.

**Richiamo di un servizio tramite un assembly client .NET che utilizza dati BLOB tramite HTTP**

È possibile richiamare il servizio `MyApplication/EncryptDocument` (creato in Workbench) utilizzando un assembly client .NET che utilizza dati tramite HTTP. Per richiamare il servizio `MyApplication/EncryptDocument`, effettuare le seguenti operazioni:

1. Creare l&#39;assembly client .NET.
1. Fare riferimento all&#39;assembly client Microsoft .NET. Creazione di un progetto Microsoft .NET client. Fare riferimento all&#39;assembly client Microsoft .NET nel progetto client. Fare riferimento anche a `System.Web.Services`.
1. Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `MyApplication_EncryptDocumentService` richiamando il relativo costruttore predefinito.
1. Impostare la proprietà `Credentials` dell&#39;oggetto `MyApplication_EncryptDocumentService` con un oggetto `System.Net.NetworkCredential`. All&#39;interno del costruttore `System.Net.NetworkCredential`, specificare un nome utente di AEM Forms e la password corrispondente. Impostare i valori di autenticazione per consentire all&#39;applicazione client .NET di scambiare messaggi SOAP con AEM Forms.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per trasmettere dati al processo `MyApplication/EncryptDocument`.
1. Assegnare un valore stringa al membro dati `remoteURL` dell&#39;oggetto `BLOB` che specifica la posizione URI di un documento PDF da passare al servizio `MyApplication/EncryptDocument`.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `MyApplication_EncryptDocumentService` e passando l&#39;oggetto `BLOB`. Questo processo restituisce un documento PDF crittografato in un oggetto `BLOB`.
1. Creare un oggetto `System.UriBuilder` utilizzando il relativo costruttore e passando il valore del membro dati `remoteURL` dell&#39;oggetto `BLOB` restituito.
1. Converte l&#39;oggetto `System.UriBuilder` in oggetto `System.IO.Stream`. La Guida introduttiva di C# che segue questo elenco illustra come eseguire questa attività.
1. Creare una matrice di byte e popolarla con i dati nell&#39;oggetto `System.IO.Stream`.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

### Richiamare un servizio utilizzando le classi proxy Java e i dati BLOB su HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Puoi richiamare un servizio AEM Forms utilizzando le classi proxy Java e i dati BLOB su HTTP. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando le classi proxy Java, effettuare le seguenti operazioni:

1. Creare classi proxy Java utilizzando JAX-WS che utilizza il servizio WSDL `MyApplication/EncryptDocument`. Utilizza il seguente endpoint WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Per informazioni, vedere [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms.*

1. Crea un pacchetto delle classi proxy Java create utilizzando JAX-WS in un file JAR.
1. Includi il file JAR del proxy Java e i file JAR nel seguente percorso:

   &lt;Directory di installazione>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   nel percorso della classe del progetto client Java.

1. Creare un oggetto `MyApplicationEncryptDocumentService` utilizzando il relativo costruttore.
1. Creare un oggetto `MyApplicationEncryptDocument` richiamando il metodo `getEncryptDocument` dell&#39;oggetto `MyApplicationEncryptDocumentService`.
1. Imposta i valori di connessione necessari per richiamare AEM Forms assegnando valori ai seguenti membri dati:

   * Assegnare l&#39;endpoint WSDL e il tipo di codifica al campo `ENDPOINT_ADDRESS_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando BLOB tramite la codifica HTTP, specificare il seguente valore URL:

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Assegnare l&#39;utente di AEM Forms al campo `USERNAME_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`.
   * Assegnare il valore della password corrispondente al campo `PASSWORD_PROPERTY` dell&#39;oggetto `javax.xml.ws.BindingProvider`.

   L&#39;esempio di codice seguente mostra questa logica dell&#39;applicazione:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Popolare l&#39;oggetto `BLOB` richiamando il relativo metodo `setRemoteURL`. Passa un valore stringa che specifica la posizione URI di un documento PDF da passare al servizio `MyApplication/EncryptDocument`.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `MyApplicationEncryptDocument` e passando l&#39;oggetto `BLOB` che contiene il documento PDF. Questo processo restituisce un documento PDF crittografato in un oggetto `BLOB`.
1. Creare una matrice di byte per memorizzare il flusso di dati che rappresenta il documento PDF crittografato. Richiama il metodo `getRemoteURL` dell&#39;oggetto `BLOB` (utilizza l&#39;oggetto `BLOB` restituito dal metodo `invoke`).
1. Creare un oggetto `java.io.File` utilizzando il relativo costruttore. Questo oggetto rappresenta il documento PDF crittografato.
1. Creare un oggetto `java.io.FileOutputStream` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File`.
1. Richiama il metodo `write` dell&#39;oggetto `java.io.FileOutputStream`. Passare la matrice di byte contenente il flusso di dati che rappresenta il documento PDF crittografato.

## Richiamare AEM Forms utilizzando DIME {#invoking-aem-forms-using-dime}

È possibile richiamare i servizi AEM Forms utilizzando SOAP con allegati. AEM Forms supporta sia gli standard di servizio web MIME che DIME. DIME consente di inviare allegati binari, ad esempio documenti PDF, insieme a richieste di chiamata anziché codificare l&#39;allegato. Nella sezione *Richiamare AEM Forms utilizzando DIME* viene illustrato come richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument` utilizzando DIME.

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

Questo processo non è basato su un processo AEM Forms esistente. Per seguire gli esempi di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>La chiamata delle operazioni del servizio AEM Forms tramite DIME è obsoleta. Si consiglia di usare MTOM. (Vedi [Chiamata di AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)

### Creazione di un progetto .NET che utilizza DIME {#creating-a-net-project-that-uses-dime}

Per creare un progetto .NET che possa richiamare un servizio Forms utilizzando DIME, eseguire le operazioni seguenti:

* Installare Web Services Enhancements 2.0 nel computer di sviluppo.
* Creare un riferimento Web al servizio Forms FormsAEM dall&#39;interno del progetto .NET.

**Installazione dei miglioramenti dei servizi Web 2.0**

Installare Web Services Enhancements 2.0 nel computer di sviluppo e integrarlo con Microsoft Visual Studio .NET. È possibile scaricare i miglioramenti ai servizi Web 2.0 dall&#39;[Area download Microsoft.](https://www.microsoft.com/downloads/search.aspx)

Da questa pagina Web cercare Miglioramenti servizi Web 2.0 e scaricarlo sul computer di sviluppo. Questo download inserisce nel computer un file denominato Microsoft WSE 2.0 SPI.msi. Eseguire il programma di installazione e seguire le istruzioni in linea.

>[!NOTE]
>
>I miglioramenti ai servizi Web 2.0 supportano DIME. La versione supportata di Microsoft Visual Studio è 2003 quando si utilizzano i miglioramenti dei servizi Web 2.0. I miglioramenti dei servizi Web 3.0 non supportano DIME, ma MTOM.

**Creazione di un riferimento Web a un servizio AEM Forms**

Dopo aver installato i miglioramenti dei servizi Web 2.0 nel computer di sviluppo e aver creato un progetto Microsoft .NET, creare un riferimento Web al servizio Forms. Ad esempio, per creare un riferimento Web al processo `MyApplication/EncryptDocument` e presupporre che Forms sia installato nel computer locale, specificare il seguente URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Dopo aver creato un riferimento Web, sono disponibili i due tipi di dati proxy seguenti da utilizzare nel progetto .NET: `EncryptDocumentService` e `EncryptDocumentServiceWse`. Per richiamare il processo `MyApplication/EncryptDocument` utilizzando DIME, utilizzare il tipo `EncryptDocumentServiceWse`.

>[!NOTE]
>
>Prima di creare un riferimento Web al servizio Forms, accertarsi di fare riferimento a Miglioramenti dei servizi Web 2.0 nel progetto. Vedere &quot;Installazione dei miglioramenti ai servizi Web 2.0&quot;.

**Riferimento alla libreria WSE**

1. Nel menu Progetto, selezionate Aggiungi riferimento (Add Reference).
1. Nella finestra di dialogo Aggiungi riferimento selezionare Microsoft.Web.Services2.dll.
1. Selezionare System.Web.Services.dll.
1. Fare clic su Seleziona e quindi su OK.

**Creare un riferimento Web a un servizio Forms**

1. Scegliere Aggiungi riferimento Web dal menu Progetto.
1. Nella finestra di dialogo URL, specifica l’URL del servizio Forms.
1. Fate clic su Vai (Go), quindi su Aggiungi riferimento (Add Reference).

>[!NOTE]
>
>Assicurarsi di abilitare il progetto .NET per l&#39;utilizzo della libreria WSE. In Esplora progetti fare clic con il pulsante destro del mouse sul nome del progetto e selezionare Abilita WSE 2.0. Accertatevi che la casella di controllo nella finestra di dialogo visualizzata sia selezionata.

**Richiamo di un servizio tramite DIME in un progetto .NET**

È possibile richiamare un servizio Forms utilizzando DIME. Considerare il processo `MyApplication/EncryptDocument` che accetta un documento PDF non protetto e restituisce un documento PDF crittografato con password. Per richiamare il processo `MyApplication/EncryptDocument` utilizzando DIME, effettuare le seguenti operazioni:

1. Creare un progetto Microsoft .NET che consente di richiamare un servizio Forms utilizzando DIME. Accertati di includere Web Services Enhancements 2.0 e crea un riferimento Web al servizio AEM Forms.
1. Dopo aver impostato un riferimento Web al processo `MyApplication/EncryptDocument`, creare un oggetto `EncryptDocumentServiceWse` utilizzando il relativo costruttore predefinito.
1. Impostare il membro dati `Credentials` dell&#39;oggetto `EncryptDocumentServiceWse` con un valore `System.Net.NetworkCredential` che specifica il nome utente e la password di AEM Form.
1. Creare un oggetto `Microsoft.Web.Services2.Dime.DimeAttachment` utilizzando il relativo costruttore e passando i seguenti valori:

   * Valore stringa che specifica un valore GUID. È possibile ottenere un valore GUID richiamando il metodo `System.Guid.NewGuid.ToString`.
   * Valore stringa che specifica il tipo di contenuto. Poiché questo processo richiede un documento PDF, specificare `application/pdf`.
   * Valore di enumerazione `TypeFormat`. Specificare `TypeFormat.MediaType`.
   * Valore stringa che specifica la posizione del documento PDF da passare al processo AEM Forms.

1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Aggiungere l&#39;allegato DIME all&#39;oggetto `BLOB` assegnando il valore del membro dati `Id` dell&#39;oggetto `Microsoft.Web.Services2.Dime.DimeAttachment` al membro dati `attachmentID` dell&#39;oggetto `BLOB`.
1. Richiama il metodo `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` e passa l&#39;oggetto `Microsoft.Web.Services2.Dime.DimeAttachment`.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `EncryptDocumentServiceWse` e passando l&#39;oggetto `BLOB` che contiene l&#39;allegato DIME. Questo processo restituisce un documento PDF crittografato in un oggetto `BLOB`.
1. Ottenere il valore dell&#39;identificatore dell&#39;allegato ottenendo il valore del membro dati `attachmentID` dell&#39;oggetto `BLOB` restituito.
1. Scorrere gli allegati in `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` e utilizzare il valore dell&#39;identificatore dell&#39;allegato per ottenere il documento PDF crittografato.
1. Ottenere un oggetto `System.IO.Stream` ottenendo il valore del membro dati `Stream` dell&#39;oggetto `Attachment`.
1. Creare una matrice di byte e passare tale matrice di byte al metodo `Read` dell&#39;oggetto `System.IO.Stream`. Questo metodo popola la matrice di byte con un flusso di dati che rappresenta il documento PDF crittografato.
1. Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta un percorso di file PDF. Questo oggetto rappresenta il documento PDF crittografato.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto della matrice di byte nel file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

### Creazione di classi proxy Java Apache Axis che utilizzano DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

È possibile utilizzare lo strumento Apache Axis WSDL2Java per convertire un servizio WSDL in classi proxy Java in modo da poter richiamare le operazioni del servizio. Utilizzando Apache Ant, è possibile generare i file della libreria Axis da un WSDL del servizio AEM Forms che consente di richiamare il servizio. (Vedi [Creazione di classi proxy Java tramite l&#39;asse Apache](#creating-java-proxy-classes-using-apache-axis).)

Lo strumento Apache Axis WSDL2Java genera file JAVA che contengono metodi utilizzati per inviare richieste SOAP a un servizio. Le richieste SOAP ricevute da un servizio vengono decodificate dalle librerie generate dall&#39;asse e restituite ai metodi e agli argomenti.

Per richiamare il servizio `MyApplication/EncryptDocument` (creato in Workbench) utilizzando i file di libreria generati da Axis e DIME, effettuare le seguenti operazioni:

1. Creare classi proxy Java che utilizzano il servizio WSDL `MyApplication/EncryptDocument` utilizzando l&#39;asse Apache. (Vedi [Creazione di classi proxy Java tramite l&#39;asse Apache](#creating-java-proxy-classes-using-apache-axis).)
1. Includi le classi proxy Java nel percorso della classe.
1. Creare un oggetto `MyApplicationEncryptDocumentServiceLocator` utilizzando il relativo costruttore.
1. Creare un oggetto `URL` utilizzando il relativo costruttore e passando un valore stringa che specifica la definizione WSDL del servizio AEM Forms. Assicurarsi di specificare `?blob=dime` alla fine dell&#39;URL dell&#39;endpoint SOAP. Ad esempio, utilizza

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Creare un oggetto `EncryptDocumentSoapBindingStub` richiamandone il costruttore e passando l&#39;oggetto `MyApplicationEncryptDocumentServiceLocator` e l&#39;oggetto `URL`.
1. Impostare il nome utente e la password di AEM Forms richiamando i metodi `setUsername` e `setPassword` dell&#39;oggetto `EncryptDocumentSoapBindingStub`.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recuperare il documento PDF da inviare al servizio `MyApplication/EncryptDocument` creando un oggetto `java.io.File`. Passa un valore stringa che specifica la posizione del documento PDF.
1. Creare un oggetto `javax.activation.DataHandler` utilizzando il relativo costruttore e passando un oggetto `javax.activation.FileDataSource`. È possibile creare l&#39;oggetto `javax.activation.FileDataSource` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File` che rappresenta il documento di PDF.
1. Creare un oggetto `org.apache.axis.attachments.AttachmentPart` utilizzando il relativo costruttore e passando l&#39;oggetto `javax.activation.DataHandler`.
1. Allegare l&#39;allegato richiamando il metodo `addAttachment` dell&#39;oggetto `EncryptDocumentSoapBindingStub` e passando l&#39;oggetto `org.apache.axis.attachments.AttachmentPart`.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. Compilare l&#39;oggetto `BLOB` con il valore dell&#39;identificatore dell&#39;allegato richiamando il metodo `setAttachmentID` dell&#39;oggetto `BLOB` e passando il valore dell&#39;identificatore dell&#39;allegato. Questo valore può essere ottenuto richiamando il metodo `getContentId` dell&#39;oggetto `org.apache.axis.attachments.AttachmentPart`.
1. Richiama il processo `MyApplication/EncryptDocument` richiamando il metodo `invoke` dell&#39;oggetto `EncryptDocumentSoapBindingStub`. Passa l&#39;oggetto `BLOB` che contiene l&#39;allegato DIME. Questo processo restituisce un documento PDF crittografato in un oggetto `BLOB`.
1. Ottenere il valore dell&#39;identificatore dell&#39;allegato richiamando il metodo `getAttachmentID` dell&#39;oggetto `BLOB` restituito. Questo metodo restituisce un valore stringa che rappresenta il valore di identificazione dell&#39;allegato restituito.
1. Recuperare gli allegati richiamando il metodo `getAttachments` dell&#39;oggetto `EncryptDocumentSoapBindingStub`. Questo metodo restituisce una matrice di `Objects` che rappresenta gli allegati.
1. Scorrere gli allegati (l&#39;array `Object`) e utilizzare il valore dell&#39;identificatore dell&#39;allegato per ottenere il documento PDF crittografato. Ogni elemento è un oggetto `org.apache.axis.attachments.AttachmentPart`.
1. Ottenere l&#39;oggetto `javax.activation.DataHandler` associato all&#39;allegato richiamando il metodo `getDataHandler` dell&#39;oggetto `org.apache.axis.attachments.AttachmentPart`.
1. Ottenere un oggetto `java.io.FileStream` richiamando il metodo `getInputStream` dell&#39;oggetto `javax.activation.DataHandler`.
1. Creare una matrice di byte e passare tale matrice di byte al metodo `read` dell&#39;oggetto `java.io.FileStream`. Questo metodo popola la matrice di byte con un flusso di dati che rappresenta il documento PDF crittografato.
1. Creare un oggetto `java.io.File` utilizzando il relativo costruttore. Questo oggetto rappresenta il documento PDF crittografato.
1. Creare un oggetto `java.io.FileOutputStream` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File`.
1. Richiama il metodo `write` dell&#39;oggetto `java.io.FileOutputStream` e passa la matrice di byte contenente il flusso di dati che rappresenta il documento PDF crittografato.

**Consulta anche**

[Guida introduttiva: Richiamare un servizio utilizzando DIME in un progetto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Utilizzo dell’autenticazione basata su SAML {#using-saml-based-authentication}

AEM Forms supporta varie modalità di autenticazione dei servizi web quando si richiamano i servizi. Una modalità di autenticazione specifica sia un nome utente che un valore di password utilizzando un’intestazione di autorizzazione di base nella chiamata del servizio web. AEM Forms supporta anche l’autenticazione basata su asserzione SAML. Quando un’applicazione client richiama un servizio AEM Forms utilizzando un servizio web, può fornire le informazioni di autenticazione in uno dei seguenti modi:

* Passaggio delle credenziali come parte dell&#39;autorizzazione di base
* Passaggio del token del nome utente come parte dell&#39;intestazione WS-Security
* Passaggio di un&#39;asserzione SAML come parte dell&#39;intestazione WS-Security
* Passaggio del token Kerberos come parte dell&#39;intestazione WS-Security

AEM Forms non supporta l’autenticazione standard basata su certificati, ma supporta invece l’autenticazione basata su certificati in una forma diversa.

>[!NOTE]
>
>Il servizio web inizia rapidamente in Programmazione con AEM Forms e specifica i valori nome utente e password per eseguire l’autorizzazione.

L’identità degli utenti di AEM Forms può essere rappresentata tramite un’asserzione SAML firmata utilizzando una chiave segreta. Il codice XML seguente mostra un esempio di asserzione SAML.

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

Questa asserzione di esempio viene rilasciata per un utente amministratore. Questa asserzione contiene i seguenti elementi rilevanti:

* È valido per una certa durata.
* Viene emesso per un utente particolare.
* È dotato di firma digitale. Quindi qualsiasi modifica apportata potrebbe rompere la firma.
* Può essere presentato ad AEM Forms come token di identità dell’utente simile al nome utente e alla password.

Un&#39;applicazione client può recuperare l&#39;asserzione da qualsiasi API AEM Forms AuthenticationManager che restituisce un oggetto `AuthResult`. È possibile ottenere un&#39;istanza `AuthResult` eseguendo uno dei due metodi seguenti:

* Autenticazione dell’utente tramite uno dei metodi di autenticazione esposti dall’API AuthenticationManager. In genere si utilizzano il nome utente e la password, ma è anche possibile utilizzare l’autenticazione del certificato.
* Utilizzo del metodo `AuthenticationManager.getAuthResultOnBehalfOfUser`. Questo metodo consente a un&#39;applicazione client di ottenere un oggetto `AuthResult` per qualsiasi utente di AEM Forms.

Un utente di AEM Forms può essere autenticato utilizzando un token SAML ottenuto. Questa asserzione SAML (frammento xml) può essere inviata come parte dell&#39;intestazione WS-Security con la chiamata al servizio Web per l&#39;autenticazione utente. In genere, un&#39;applicazione client ha autenticato un utente ma non ha memorizzato le credenziali utente. (Oppure l&#39;utente ha effettuato l&#39;accesso al client tramite un meccanismo diverso dall&#39;utilizzo di un nome utente e di una password.) In questa situazione, l’applicazione client deve richiamare AEM Forms e rappresentare un utente specifico che è autorizzato a richiamare AEM Forms.

Per rappresentare un utente specifico, richiamare il metodo `AuthenticationManager.getAuthResultOnBehalfOfUser` utilizzando un servizio Web. Questo metodo restituisce un&#39;istanza `AuthResult` che contiene l&#39;asserzione SAML per l&#39;utente.

Quindi, utilizza tale asserzione SAML per richiamare qualsiasi servizio che richiede l’autenticazione. Questa azione comporta l’invio dell’asserzione come parte dell’intestazione SOAP. Quando viene effettuata una chiamata al servizio web con questa asserzione, AEM Forms identifica l’utente come quello rappresentato da tale asserzione. In altre parole, l’utente specificato nell’asserzione è l’utente che sta richiamando il servizio.

### Utilizzo delle classi dell’asse Apache e dell’autenticazione basata su SAML {#using-apache-axis-classes-and-saml-based-authentication}

È possibile richiamare un servizio AEM Forms da classi proxy Java create utilizzando la libreria Axis. (Vedi [Creazione di classi proxy Java tramite l&#39;asse Apache](#creating-java-proxy-classes-using-apache-axis).)

Quando si utilizza AXIS che utilizza l’autenticazione basata su SAML, registrare il gestore di richieste e risposte con Axis. Apache Axis richiama il gestore prima di inviare una richiesta di chiamata ad AEM Forms. Per registrare un gestore, creare una classe Java che estenda `org.apache.axis.handlers.BasicHandler`.

**Creare un AssertionHandler con l&#39;asse**

La seguente classe Java, denominata `AssertionHandler.java`, mostra un esempio di classe Java che estende `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**Registra il gestore**

Per registrare un gestore con Axis, creare un file client-config.wsdd. Per impostazione predefinita, Axis cerca un file con questo nome. Il codice XML seguente è un esempio di file client-config.wsdd. Per ulteriori informazioni, consultate la documentazione sugli assi.

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**Richiama un servizio AEM Forms**

Esempio Nell&#39;esempio di codice riportato di seguito viene richiamato un servizio AEM Forms utilizzando l&#39;autenticazione basata su SAML.

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### Utilizzo di un assembly client .NET e dell&#39;autenticazione basata su SAML {#using-a-net-client-assembly-and-saml-based-authentication}

È possibile richiamare un servizio Forms utilizzando un assembly client .NET e l&#39;autenticazione basata su SAML. Per eseguire questa operazione, è necessario utilizzare il Web Service Enhancements 3.0 (WSE). Per informazioni sulla creazione di un assembly client .NET che utilizza WSE, vedere [Creazione di un progetto .NET che utilizza DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>La sezione DIME utilizza WSE 2.0. Per utilizzare l&#39;autenticazione basata su SAML, seguire le stesse istruzioni specificate nell&#39;argomento DIME. Tuttavia, sostituire WSE 2.0 con WSE 3.0. Installare Web Services Enhancements 3.0 nel computer di sviluppo e integrarlo con Microsoft Visual Studio .NET. È possibile scaricare i miglioramenti dei servizi Web 3.0 dall&#39;[Area download Microsoft](https://www.microsoft.com/downloads/search.aspx).

L’architettura WSE utilizza i tipi di dati Policy, Assertions e SecurityToken. Per una chiamata al servizio web, specifica brevemente un criterio. Un criterio può avere più asserzioni. Ogni asserzione può contenere filtri. Un filtro viene richiamato in determinate fasi di una chiamata al servizio web e, in quel momento, può modificare la richiesta di SOAP. Per informazioni dettagliate, consulta la documentazione sui miglioramenti dei servizi Web 3.0.

**Crea asserzione e filtro**

Nell&#39;esempio di codice C# seguente vengono create classi di filtro e di asserzione. In questo esempio di codice viene creato SamlAssertionOutputFilter. Questo filtro viene richiamato dal framework WSE prima che la richiesta SOAP venga inviata ad AEM Forms.

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**Crea token SAML**

Creare una classe per rappresentare l&#39;asserzione SAML. L&#39;attività principale eseguita da questa classe consiste nel convertire i valori dei dati da stringa a xml e nel mantenere uno spazio vuoto. Questo xml di asserzione viene successivamente importato nella richiesta SOAP.

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**Richiama un servizio AEM Forms**

Esempio Nell&#39;esempio di codice C# riportato di seguito viene richiamato un servizio Forms utilizzando l&#39;autenticazione basata su SAML.

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Considerazioni correlate quando si utilizzano i servizi web {#related-considerations-when-using-web-services}

Talvolta si verificano problemi quando si richiamano determinate operazioni dei servizi AEM Forms utilizzando i servizi web. L&#39;obiettivo di questa discussione è quello di identificare tali problemi e fornire una soluzione, se disponibile.

### Richiamare le operazioni del servizio in modo asincrono {#invoking-service-operations-asynchronously}

Se si tenta di richiamare in modo asincrono un&#39;operazione del servizio AEM Forms, ad esempio l&#39;operazione Genera `htmlToPDF` di PDF, si verifica un `SoapFaultException`. Per risolvere il problema, creare un file XML di associazione personalizzata che associa l&#39;elemento `ExportPDF_Result` e altri elementi in classi diverse. Il codice XML seguente rappresenta un file di associazione personalizzato.

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

Utilizzare questo file XML quando si creano file proxy Java utilizzando JAX-WS. (Vedi [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Fare riferimento a questo file XML durante l&#39;esecuzione dello strumento JAX-WS (wsimport.exe) utilizzando l&#39;opzione della riga di comando - `b`. Aggiornare l&#39;elemento `wsdlLocation` nel file XML di binding per specificare l&#39;URL di AEM Forms.

Per garantire il funzionamento della chiamata asincrona, modificare il valore dell&#39;URL del punto finale e specificare `async=true`. Ad esempio, per i file proxy Java creati con JAX-WS, specificare quanto segue per `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

Nell&#39;elenco seguente vengono specificati altri servizi che richiedono un file di associazione personalizzato quando viene richiamato in modo asincrono:

* PDFG3D
* Gestione attività
* Application Manager
* Gestione directory
* Distiller
* Rights Management
* Gestione documenti

### Differenze nei server applicazioni J2EE {#differences-in-j2ee-application-servers}

A volte una libreria proxy creata utilizzando un server applicazioni J2EE specifico non richiama correttamente AEM Forms ospitato su un server applicazioni J2EE diverso. Considera una libreria proxy generata utilizzando AEM Forms distribuita su WebSphere. Questa libreria proxy non può richiamare correttamente i servizi AEM Forms distribuiti sul server applicazioni JBoss.

Alcuni tipi di dati complessi di AEM Forms, ad esempio `PrincipalReference`, vengono definiti in modo diverso quando AEM Forms viene distribuito su WebSphere rispetto all&#39;Application Server JBoss. Le differenze tra i JDK utilizzati dai diversi servizi applicativi J2EE sono il motivo per cui esistono differenze nelle definizioni WSDL. Di conseguenza, utilizzare le librerie proxy generate dallo stesso server applicazioni J2EE.

### Accesso a più servizi tramite servizi web {#accessing-multiple-services-using-web-services}

A causa di conflitti di spazio dei nomi, gli oggetti dati non possono essere condivisi tra più WSDL di servizio. Diversi servizi possono condividere tipi di dati e, pertanto, i servizi condividono la definizione di questi tipi nei WSDL. Ad esempio, non è possibile aggiungere due assembly client .NET contenenti un tipo di dati `BLOB` allo stesso progetto client .NET. Se si tenta di eseguire questa operazione, si verifica un errore di compilazione.

L&#39;elenco seguente specifica i tipi di dati che non possono essere condivisi tra più WSDL di servizio:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Per evitare questo problema, si consiglia di qualificare completamente i tipi di dati. Si consideri ad esempio un&#39;applicazione .NET che fa riferimento sia al servizio Forms che al servizio Signature utilizzando un riferimento al servizio. Entrambi i riferimenti al servizio conterranno una classe `BLOB`. Per utilizzare un&#39;istanza `BLOB`, qualificare completamente l&#39;oggetto `BLOB` quando viene dichiarato. Questo approccio è illustrato nell’esempio di codice seguente. Per informazioni su questo esempio di codice, vedere [Forms interattivo con firma digitale](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

Nell&#39;esempio di codice C# riportato di seguito viene firmato un modulo interattivo di cui è stato eseguito il rendering dal servizio Forms. L&#39;applicazione client dispone di due riferimenti di servizio. L&#39;istanza `BLOB` associata al servizio Forms appartiene allo spazio dei nomi `SignInteractiveForm.ServiceReference2`. Analogamente, l&#39;istanza `BLOB` associata al servizio di firma appartiene allo spazio dei nomi `SignInteractiveForm.ServiceReference1`. Il modulo interattivo firmato viene salvato come file PDF denominato *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify an XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify an XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### Servizi che iniziano con la lettera I produce file proxy non validi {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Il nome di alcune classi proxy generate da AEM Forms non è corretto quando si utilizzano Microsoft .Net 3.5 e WCF. Questo problema si verifica quando vengono create classi proxy per IBMFilenetContentRepositoryConnector, IDPSchedulerService o qualsiasi altro servizio il cui nome inizia con la lettera I. Ad esempio, il nome del client generato se è presente IBMFileNetContentRepositoryConnector è `BMFileNetContentRepositoryConnectorClient`. Lettera I mancante nella classe proxy generata.
