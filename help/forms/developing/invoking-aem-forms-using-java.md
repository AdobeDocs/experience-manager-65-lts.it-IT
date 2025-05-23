---
title: Richiamare AEM Forms tramite JavaAPI
description: Utilizzare l'API Java AEM Forms per il protocollo di trasporto RMI per la chiamata remota, il trasporto VM per la chiamata locale, SOAP per la chiamata remota, autenticazione diversa, ad esempio nome utente e password, e richieste di chiamata sincrone e asincrone.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 42c85231-9e65-4c3c-8b86-3efdaa577161
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '5333'
ht-degree: 0%

---

# Richiamare AEM Forms tramite l’API Java {#invoking-aem-forms-using-the-javaapi}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

AEM Forms può essere richiamato utilizzando l’API Java di AEM Forms. Quando utilizzi l’API Java di AEM Forms, puoi utilizzare l’API di richiamo o le librerie client Java. Le librerie client Java sono disponibili per servizi come il servizio Rights Management. Queste API fortemente tipizzate consentono di sviluppare applicazioni Java che richiamano AEM Forms.

Le API di chiamata sono classi incluse nel pacchetto `com.adobe.idp.dsc`. Utilizzando queste classi, è possibile inviare una richiesta di chiamata direttamente a un servizio e gestire una risposta di chiamata restituita. Utilizza l’API di richiamo per richiamare processi di breve o lunga durata creati utilizzando Workbench.

Il modo consigliato per richiamare un servizio a livello di programmazione consiste nell’utilizzare una libreria client Java corrispondente al servizio, anziché all’API di richiamo. Ad esempio, per richiamare il servizio Encryption, utilizzare la libreria client del servizio Encryption. Per eseguire un&#39;operazione del servizio di crittografia, richiamare un metodo appartenente all&#39;oggetto client del servizio di crittografia. È possibile crittografare un documento PDF con una password richiamando il metodo `encryptPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient`.

L’API Java supporta le seguenti funzioni:

* Protocollo di trasporto RMI per chiamata remota
* Trasporto VM per chiamata locale
* SOAP per chiamata remota
* Autenticazione diversa, ad esempio nome utente e password
* Richieste di chiamata sincrone e asincrone

[Inclusione dei file della libreria Java di AEM Forms](#including-aem-forms-java-library-files)

[Richiamare processi a lunga durata incentrati sull&#39;uomo](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Richiamare AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Impostazione delle proprietà di connessione](#setting-connection-properties)

[Passaggio dei dati ai servizi AEM Forms tramite API Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Richiamare un servizio utilizzando una libreria client Java](#invoking-a-service-using-a-java-client-library)

[Richiamare un processo di breve durata utilizzando l’API di richiamo](#invoking-a-short-lived-process-using-the-invocation-api)

[Creazione di un’applicazione web Java che richiama un processo di lunga durata incentrato sull’uomo](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusione dei file della libreria Java di AEM Forms {#including-aem-forms-java-library-files}

Per richiamare in modo programmatico un servizio AEM Forms utilizzando l’API Java, includi i file libreria richiesti (file JAR) nel classpath del progetto Java. I file JAR inclusi nel percorso di classe dell’applicazione client dipendono da diversi fattori:

* Il servizio AEM Forms da richiamare. Un&#39;applicazione client può richiamare uno o più servizi.
* Modalità in cui desideri richiamare un servizio AEM Forms. È possibile utilizzare la modalità EJB o SOAP. (Vedere [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Solo chiavi in mano) Avviare il server AEM Forms con il comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` per specificare un IP server per EJB

* Server applicazioni J2EE in cui viene distribuito AEM Forms.

### File JAR specifici del servizio {#service-specific-jar-files}

Nella tabella seguente sono elencati i file JAR necessari per richiamare i servizi AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>File</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Dove si trova</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso di classe di un'applicazione client Java.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso di classe di un'applicazione client Java.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso di classe di un'applicazione client Java.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk//client-libs/&lt;server app&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Necessario per richiamare il servizio Application Manager.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Assembler. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necessario per richiamare l'API del servizio Backup e ripristino.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Forms con codice a barre. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Convert PDF. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Distiller.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio DocConverter.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Document Management.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necessario per richiamare il servizio di crittografia.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Forms.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio di integrazione dati modulo.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Genera PDF.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Genera PDF 3D.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necessario per richiamare il servizio Gestione processi. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio di output.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Utilità PDF o Utilità XMP.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necessario per richiamare il servizio Acrobat Reader DC extensions.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Archivio.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs\thirdparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Obbligatorio per richiamare il servizio Rights Management.</p><p>Se AEM Forms viene distribuito su JBoss, includi tutti questi file. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p><p>Directory libreria specifica per JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio di firma.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Task Manager. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necessario per richiamare il servizio Archivio fonti attendibili. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modalità di connessione e file JAR dell&#39;applicazione J2EE {#connection-mode-and-j2ee-application-jar-files}

Nella tabella seguente sono elencati i file JAR che dipendono dalla modalità di connessione e dal server applicazioni J2EE in cui viene distribuito AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>File</p> </th>
   <th><p>Descrizione</p> </th>
   <th><p>Dove si trova</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>se AEM Forms viene richiamato utilizzando la modalità SOAP, includi questi file JAR.</p> </td>
   <td><p>&lt;<em>directory di installazione</em>&gt;/sdk/client-libs/third party</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>se AEM Forms è distribuito sul server applicazioni JBoss, includi questo file JAR.</p> <p>Le classi richieste non vengono trovate dal caricatore di classi se jboss-client.jar e i file jar di riferimento non si trovano nello stesso percorso.</p> </td>
   <td><p>Directory libreria client JBoss</p> <p>Se si distribuisce l'applicazione client nello stesso server applicazioni J2EE, non è necessario includere il file.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>se AEM Forms è distribuito su BEA WebLogic Server®, includi questo file JAR.</p> </td>
   <td><p>Directory libreria specifica per WebLogic</p> <p>Se si distribuisce l'applicazione client nello stesso server applicazioni J2EE, non è necessario includere il file.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>se AEM Forms viene distribuito su WebSphere Application Server, includere questi file JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar è richiesto per la chiamata del servizio web).</p> </li>
    </ul> </td>
   <td><p>Directory libreria specifica di WebSphere (<em>[WAS_HOME]</em>/runtime)</p> <p>Se si distribuisce l'applicazione client nello stesso server applicazioni J2EE, non è necessario includere tali file.</p> </td>
  </tr>
 </tbody>
</table>

### Richiamare scenari {#invoking-scenarios}

La tabella seguente specifica gli scenari di chiamata ed elenca i file JAR necessari per richiamare correttamente AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Servizi</p> </th>
   <th><p>Modalità di chiamata</p> </th>
   <th><p>Server applicazioni J2EE</p> </th>
   <th><p>File JAR richiesti</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>servizio Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servizio Forms</p> <p>Servizio estensioni DC Acrobat Reader</p> <p>Servizio di firma</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servizio Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>servizio Forms</p> <p>Servizio estensioni DC Acrobat Reader</p> <p>Servizio di firma</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Aggiornamento dei file JAR {#upgrading-jar-files}

Se aggiorni LiveCycle ad AEM Forms, si consiglia di includere i file JAR di AEM Forms nel percorso della classe del progetto Java. Ad esempio, se utilizzi servizi come Rights Management, riscontrerai un problema di compatibilità se non includi i file JAR di AEM Forms nel percorso della classe.

Supponendo di effettuare l&#39;aggiornamento ad AEM Forms. Per utilizzare un’applicazione Java che richiama il servizio Rights Management, includi le versioni AEM Forms dei seguenti file JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulta anche**

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

[Passaggio dei dati ai servizi AEM Forms tramite API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Richiamare un servizio utilizzando una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Impostazione delle proprietà di connessione {#setting-connection-properties}

Puoi impostare le proprietà di connessione per richiamare AEM Forms quando utilizzi l’API Java. Quando si impostano le proprietà di connessione, specificare se richiamare i servizi in remoto o in locale e specificare la modalità di connessione e i valori di autenticazione. I valori di autenticazione sono necessari se la sicurezza del servizio è abilitata. Tuttavia, se la protezione del servizio è disabilitata, non è necessario specificare i valori di autenticazione.

La modalità di connessione può essere SOAP o EJB. La modalità EJB utilizza il protocollo RMI/IIOP e le prestazioni della modalità EJB sono migliori di quelle della modalità SOAP. La modalità SOAP viene utilizzata per eliminare una dipendenza dal server applicazioni J2EE o quando viene individuato un firewall tra AEM Forms e l&#39;applicazione client. La modalità SOAP utilizza il protocollo https come trasporto sottostante e può comunicare attraverso i limiti del firewall. Se non esiste alcuna dipendenza dal server applicazioni J2EE o un firewall, è consigliabile utilizzare la modalità EJB.

Per richiamare correttamente un servizio AEM Forms, imposta le seguenti proprietà di connessione:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se si utilizza la modalità di connessione EJB, questo valore rappresenta l&#39;URL del server applicazioni J2EE in cui viene distribuito AEM Forms. Per richiamare AEM Forms in modalità remota, specificare il nome del server applicazioni J2EE in cui viene distribuito AEM Forms. Se l&#39;applicazione client si trova nello stesso server applicazioni J2EE, è possibile specificare `localhost`. A seconda del server applicazioni J2EE su cui viene distribuito AEM Forms, specificare uno dei seguenti valori:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se si utilizza la modalità di connessione di SOAP, questo valore rappresenta l&#39;endpoint a cui viene inviata una richiesta di chiamata. Per richiamare AEM Forms in modalità remota, specificare il nome del server applicazioni J2EE in cui viene distribuito AEM Forms. Se l&#39;applicazione client si trova nello stesso server applicazioni J2EE, è possibile specificare `localhost`, ad esempio `http://localhost:8080`.

   * Il valore di porta `8080` è applicabile se l&#39;applicazione J2EE è JBoss. Se il server applicazioni J2EE è IBM® WebSphere®, utilizzare la porta `9080`. Analogamente, se il server applicazioni J2EE è WebLogic, utilizzare la porta `7001`. Questi valori sono i valori di porta predefiniti. Se si modifica il valore della porta, utilizzare il numero di porta applicabile.)

* **DSC_TRANSPORT_PROTOCOL**: se si utilizza la modalità di connessione EJB, specificare `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` per questo valore. Se si utilizza la modalità di connessione SOAP, specificare `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: specifica il server applicazioni J2EE in cui viene distribuito AEM Forms. I valori validi sono `JBoss`, `WebSphere`, `WebLogic`.

   * Se si imposta questa proprietà di connessione su `WebSphere`, il valore `java.naming.factory.initial` verrà impostato su `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se si imposta questa proprietà di connessione su `WebLogic`, il valore `java.naming.factory.initial` verrà impostato su `weblogic.jndi.WLInitialContextFactory`.
   * Analogamente, se si imposta questa proprietà di connessione su `JBoss`, il valore `java.naming.factory.initial` viene impostato su `org.jnp.interfaces.NamingContextFactory`.
   * È possibile impostare la proprietà `java.naming.factory.initial` su un valore che soddisfi i requisiti se non si desidera utilizzare i valori predefiniti.

  >[!NOTE]
  >
  >Anziché utilizzare una stringa per impostare la proprietà di connessione `DSC_SERVER_TYPE`, è possibile utilizzare un membro statico della classe `ServiceClientFactoryProperties`. È possibile utilizzare i valori seguenti: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE` o `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Specifica il nome utente di AEM Forms. Per richiamare correttamente un servizio AEM Forms, l’utente deve disporre del ruolo Utente servizi. Un utente può anche avere un altro ruolo che include l’autorizzazione Richiesta servizio. In caso contrario, viene generata un’eccezione quando si tenta di richiamare un servizio. Se la protezione del servizio è disabilitata, non è necessario specificare questa proprietà di connessione.
* **DSC_CREDENTIAL_PASSWORD:** Specifica il valore della password corrispondente. Se la protezione del servizio è disabilitata, non è necessario specificare questa proprietà di connessione.
* **DSC_REQUEST_TIMEOUT:** Il limite di timeout predefinito per la richiesta SOAP è di 1200000 millisecondi (20 minuti). A volte, una richiesta può richiedere più tempo per completare l’operazione. Ad esempio, una richiesta SOAP che recupera un set di record di grandi dimensioni può richiedere un limite di timeout più lungo. È possibile utilizzare `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` per aumentare il limite di timeout della chiamata della richiesta per le richieste SOAP.

  **nota**: solo le chiamate basate su SOAP supportano la proprietà DSC_REQUEST_TIMEOUT.

Per impostare le proprietà di connessione, eseguire le operazioni seguenti:

1. Creare un oggetto `java.util.Properties` utilizzando il relativo costruttore.
1. Per impostare la proprietà di connessione `DSC_DEFAULT_EJB_ENDPOINT`, richiamare il metodo `setProperty` dell&#39;oggetto `java.util.Properties` e passare i valori seguenti:

   * Valore di enumerazione `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`
   * Valore stringa che specifica l&#39;URL del server applicazioni J2EE che ospita AEM Forms

   >[!NOTE]
   >
   >Se si utilizza la modalità di connessione SOAP, specificare il valore di enumerazione `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` anziché il valore di enumerazione `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`.

1. Per impostare la proprietà di connessione `DSC_TRANSPORT_PROTOCOL`, richiamare il metodo `setProperty` dell&#39;oggetto `java.util.Properties` e passare i valori seguenti:

   * Valore di enumerazione `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`
   * Valore di enumerazione `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`

   >[!NOTE]
   >
   >Se si utilizza la modalità di connessione SOAP, specificare il valore di enumerazione `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL` anziché il valore di enumerazione `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`.

1. Per impostare la proprietà di connessione `DSC_SERVER_TYPE`, richiamare il metodo `setProperty` dell&#39;oggetto `java.util.Properties` e passare i valori seguenti:

   * Valore di enumerazione `ServiceClientFactoryProperties.DSC_SERVER_TYPE`
   * Valore stringa che specifica il server applicazioni J2EE che ospita AEM Forms (ad esempio, se AEM Forms è distribuito su JBoss, specificare `JBoss`).

      1. Per impostare la proprietà di connessione `DSC_CREDENTIAL_USERNAME`, richiamare il metodo `setProperty` dell&#39;oggetto `java.util.Properties` e passare i valori seguenti:

   * Valore di enumerazione `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`
   * Valore stringa che specifica il nome utente necessario per richiamare AEM Forms

      1. Per impostare la proprietà di connessione `DSC_CREDENTIAL_PASSWORD`, richiamare il metodo `setProperty` dell&#39;oggetto `java.util.Properties` e passare i valori seguenti:

   * Valore di enumerazione `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`
   * Valore stringa che specifica il valore password corrispondente

**Impostazione della modalità di connessione EJB per JBoss**

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono impostate le proprietà di connessione per richiamare AEM Forms distribuito su JBoss e utilizzare la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Impostazione della modalità di connessione EJB per WebLogic**

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono impostate le proprietà di connessione per richiamare AEM Forms distribuito su WebLogic e utilizzare la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Impostazione della modalità di connessione EJB per WebSphere**

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono impostate le proprietà di connessione per richiamare AEM Forms distribuito su WebSphere e utilizzare la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Impostazione della modalità di connessione di SOAP**

Esempio Nell’esempio di codice Java seguente le proprietà di connessione vengono impostate in modalità SOAP per richiamare AEM Forms distribuito su JBoss.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Se selezioni la modalità di connessione di SOAP, assicurati di includere ulteriori file JAR nel percorso di classe dell’applicazione client.

**Impostazione delle proprietà di connessione quando la protezione del servizio è disabilitata**

Esempio Nell&#39;esempio di codice Java riportato di seguito vengono impostate le proprietà di connessione necessarie per richiamare AEM Forms distribuito nel server applicazioni JBoss e quando la protezione del servizio è disabilitata.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Tutti gli avvii rapidi Java associati alla programmazione con AEM Forms mostrano le impostazioni di connessione sia EJB che SOAP.

**Impostazione della modalità di connessione di SOAP con limite di timeout della richiesta personalizzato**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Utilizzo di un oggetto Context per richiamare AEM Forms**

È possibile utilizzare un oggetto `com.adobe.idp.Context` per richiamare un servizio AEM Forms con un utente autenticato (l&#39;oggetto `com.adobe.idp.Context` rappresenta un utente autenticato). Quando si utilizza un oggetto `com.adobe.idp.Context`, non è necessario impostare le proprietà `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD`. È possibile ottenere un oggetto `com.adobe.idp.Context` durante l&#39;autenticazione degli utenti utilizzando il metodo `authenticate` dell&#39;oggetto `AuthenticationManagerServiceClient`.

Il metodo `authenticate` restituisce un oggetto `AuthResult` contenente i risultati dell&#39;autenticazione. È possibile creare un oggetto `com.adobe.idp.Context` richiamandone il costruttore. Quindi richiamare il metodo `initPrincipal` dell&#39;oggetto `com.adobe.idp.Context` e passare l&#39;oggetto `AuthResult`, come illustrato nel codice seguente:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Anziché impostare le proprietà `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD`, è possibile richiamare il metodo `setContext` dell&#39;oggetto `ServiceClientFactory` e passare l&#39;oggetto `com.adobe.idp.Context`. Quando si utilizza un utente di AEM Forms per richiamare un servizio, assicurarsi che disponga del ruolo denominato `Services User` necessario per richiamare un servizio AEM Forms.

Esempio Nell&#39;esempio di codice riportato di seguito viene illustrato come utilizzare un oggetto `com.adobe.idp.Context` nelle impostazioni di connessione utilizzate per creare un oggetto `EncryptionServiceClient`.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Per informazioni complete sull&#39;autenticazione di un utente, vedere [Autenticazione degli utenti](/help/forms/developing/users.md#authenticating-users).

### Richiamare scenari {#invoking_scenarios-1}

In questa sezione vengono descritti i seguenti scenari di richiamo:

* Un’applicazione client in esecuzione nella propria Java Virtual Machine (JVM) richiama un’istanza AEM Forms autonoma.
* Un’applicazione client in esecuzione nella propria JVM richiama le istanze AEM Forms in cluster.

### Applicazione client che richiama un’istanza AEM Forms autonoma {#client-application-invoking-a-stand-alone-aem-forms-instance}

Il diagramma seguente mostra un’applicazione client in esecuzione nella propria JVM e che richiama un’istanza AEM Forms autonoma.

In questo scenario, un’applicazione client viene eseguita nella propria JVM e richiama i servizi AEM Forms.

>[!NOTE]
>
>Questo scenario è lo scenario di richiamo su cui si basano tutti gli avvii rapidi.

### Applicazione client che richiama istanze AEM Forms in cluster {#client-application-invoking-clustered-aem-forms-instances}

Il diagramma seguente mostra un’applicazione client in esecuzione nella propria JVM e che richiama istanze AEM Forms in un cluster.

Questo scenario è simile a un’applicazione client che richiama un’istanza autonoma di AEM Forms. Tuttavia, l’URL del provider è diverso. Se un&#39;applicazione client desidera connettersi a un server applicazioni J2EE specifico, è necessario modificare l&#39;URL per fare riferimento al server applicazioni J2EE specifico.

Il riferimento a un server applicazioni J2EE specifico non è consigliato perché la connessione tra l&#39;applicazione client e AEM Forms viene interrotta se il server applicazioni si arresta. È consigliabile che l&#39;URL del provider faccia riferimento a un gestore JNDI a livello di cella, anziché a un server applicazioni J2EE specifico.

Le applicazioni client che utilizzano la modalità di connessione SOAP possono utilizzare la porta del load balancer HTTP per il cluster. Le applicazioni client che utilizzano la modalità di connessione EJB possono connettersi alla porta EJB di un server applicazioni J2EE specifico. Questa azione gestisce il bilanciamento del carico tra i nodi del cluster.

**WebSphere**

Nell&#39;esempio seguente viene illustrato il contenuto di un file jndi.properties utilizzato per connettersi ad AEM Forms distribuito su WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

L&#39;esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi a AEM Forms distribuito su WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

Il seguente esempio mostra il contenuto di un file jndi.properties che viene utilizzato per connettersi a AEM Forms che viene distribuito su JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Rivolgersi all&#39;amministratore per determinare il nome e il numero di porta del server applicazioni J2EE.

**Consulta anche**

[Includere AEM Forms file Java libreria](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Passaggio di dati ai servizi AEM Forms tramite Java API](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Richiamo di un servizio utilizzando un client Java libreria](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Passaggio di dati ai servizi AEM Forms tramite Java API {#passing-data-to-aem-forms-services-using-the-java-api}

In genere, le operazioni dei servizi AEM Forms utilizzano o producono documenti PDF. Quando si richiama un servizio, a volte è necessario passare un documento di PDF (o altri tipi di documenti come i dati XML) al servizio. Analogamente, a volte è necessario gestire un documento PDF restituito dal servizio. La classe Java che consente di passare dati da e verso i servizi AEM Forms è `com.adobe.idp.Document`.

I servizi AEM Forms non accettano un documento PDF come altri tipi di dati, ad esempio un oggetto `java.io.InputStream` o una matrice di byte. È inoltre possibile utilizzare un oggetto `com.adobe.idp.Document` per passare altri tipi di dati, ad esempio dati XML, ai servizi.

Un oggetto `com.adobe.idp.Document` è un tipo serializzabile Java, quindi può essere trasmesso tramite una chiamata RMI. Il lato di ricezione può essere collocato (stesso host, stesso caricatore di classe), locale (stesso host, caricatore di classi diverso) o remoto (host diverso). Il passaggio del contenuto del documento è ottimizzato per ogni caso. Ad esempio, se il mittente e il destinatario si trovano sullo stesso host, il contenuto viene trasmesso su un file system locale. In alcuni casi, i documenti possono essere trasferiti in memoria.

A seconda della dimensione dell&#39;oggetto `com.adobe.idp.Document`, i dati vengono memorizzati nell&#39;oggetto `com.adobe.idp.Document` o memorizzati nel file system del server. Tutte le risorse di archiviazione temporanee occupate dall&#39;oggetto `com.adobe.idp.Document` vengono rimosse automaticamente al momento dell&#39;eliminazione di `com.adobe.idp.Document`. (Vedi [Eliminazione degli oggetti documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

A volte è necessario conoscere il tipo di contenuto di un oggetto `com.adobe.idp.Document` prima di poterlo passare a un servizio. Se ad esempio un&#39;operazione richiede un tipo di contenuto specifico, ad esempio `application/pdf`, è consigliabile determinare il tipo di contenuto. (Vedi [Determinazione del tipo di contenuto di un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

L&#39;oggetto `com.adobe.idp.Document` tenta di determinare il tipo di contenuto utilizzando i dati forniti. Se non è possibile recuperare il tipo di contenuto dai dati forniti (ad esempio, quando i dati sono stati forniti come matrice di byte), impostare il tipo di contenuto. Per impostare il tipo di contenuto, richiamare il metodo `setContentType` dell&#39;oggetto `com.adobe.idp.Document`. (Vedi [Determinazione del tipo di contenuto di un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se i file collaterali risiedono nello stesso file system, la creazione di un oggetto `com.adobe.idp.Document` è più veloce. Se i file collaterali risiedono su file system remoti, è necessario eseguire un&#39;operazione di copia che influisce sulle prestazioni.

Un&#39;applicazione può contenere entrambi i tipi di dati `com.adobe.idp.Document` e `org.w3c.dom.Document`. Assicurarsi tuttavia di aver qualificato completamente il tipo di dati `org.w3c.dom.Document`. Per informazioni sulla conversione di un oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document`, vedere [Guida rapida (modalità EJB): precompilazione di Forms con layout che consentono il flusso tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Per evitare perdite di memoria in WebLogic durante l&#39;utilizzo di un oggetto `com.adobe.idp.Document`, leggere le informazioni del documento in blocchi di 2048 byte o meno. Ad esempio, il codice seguente legge le informazioni del documento in blocchi di 2048 byte:

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Consulta anche**

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di documenti {#creating-documents}

Creare un oggetto `com.adobe.idp.Document` prima di richiamare un&#39;operazione di servizio che richiede un documento di PDF (o altri tipi di documenti) come valore di input. La classe `com.adobe.idp.Document` fornisce costruttori che consentono di creare un documento dai seguenti tipi di contenuto:

* Matrice di byte
* Un oggetto `com.adobe.idp.Document` esistente
* Un oggetto `java.io.File`
* Un oggetto `java.io.InputStream`
* Un oggetto `java.net.URL`

#### Creazione di un documento basato su una matrice di byte {#creating-a-document-based-on-a-byte-array}

Esempio Nell&#39;esempio di codice seguente viene creato un oggetto `com.adobe.idp.Document` basato su una matrice di byte.

**Creazione di un oggetto Document basato su una matrice di byte**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Creazione di un documento basato su un altro documento {#creating-a-document-based-on-another-document}

Esempio Nell&#39;esempio di codice seguente viene creato un oggetto `com.adobe.idp.Document` basato su un altro oggetto `com.adobe.idp.Document`.

**Creazione di un oggetto Document basato su un altro documento**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Creazione di un documento basato su un file {#creating-a-document-based-on-a-file}

Nell&#39;esempio di codice seguente viene creato un oggetto `com.adobe.idp.Document` basato su un file PDF denominato *map.pdf*. Questo file si trova nella radice del disco rigido C. Questo costruttore tenta di impostare il tipo di contenuto MIME dell&#39;oggetto `com.adobe.idp.Document` utilizzando l&#39;estensione del nome file.

Il costruttore `com.adobe.idp.Document` che accetta un oggetto `java.io.File` accetta anche un parametro booleano. Impostando questo parametro su `true`, l&#39;oggetto `com.adobe.idp.Document` elimina il file. Ciò significa che non è necessario rimuovere il file dopo averlo passato al costruttore `com.adobe.idp.Document`.

L&#39;impostazione di questo parametro su `false` indica che si mantiene la proprietà del file. L&#39;impostazione di questo parametro su `true` è più efficiente. Il motivo è che l&#39;oggetto `com.adobe.idp.Document` può spostare il file direttamente nell&#39;area gestita locale anziché copiarlo (operazione più lenta).

**Creazione di un oggetto Document basato su un file PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Creazione di un documento basato su un oggetto InputStream {#creating-a-document-based-on-an-inputstream-object}

Nell&#39;esempio di codice Java seguente viene creato un oggetto `com.adobe.idp.Document` basato su un oggetto `java.io.InputStream`.

**Creazione di un documento basato su un oggetto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creazione di un documento basato su contenuto accessibile da un URL {#creating-a-document-based-on-content-accessible-from-an-url}

Nell&#39;esempio di codice Java seguente viene creato un oggetto `com.adobe.idp.Document` basato su un file PDF denominato *map.pdf*. Il file si trova in un&#39;applicazione Web denominata `WebApp` in esecuzione su `localhost`. Questo costruttore tenta di impostare il tipo di contenuto MIME dell&#39;oggetto `com.adobe.idp.Document` utilizzando il tipo di contenuto restituito con il protocollo URL.

L&#39;URL fornito all&#39;oggetto `com.adobe.idp.Document` viene sempre letto sul lato in cui viene creato l&#39;oggetto `com.adobe.idp.Document` originale, come illustrato in questo esempio:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

Il file c:/temp/input.pdf deve trovarsi sul computer client (non sul computer server). Il computer client corrisponde al luogo in cui viene letto il URL e in cui è stato creato l&#39;oggetto `com.adobe.idp.Document` .

**Creazione di un documento basato su contenuto accessibile da un&#39;URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulta anche**

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione dei documenti restituiti {#handling-returned-documents}

Le operazioni di servizio che restituiscono un documento PDF (o altri tipi di dati, ad esempio i dati XML) come valore di output restituiscono un `com.adobe.idp.Document` oggetto. Una volta ricevuto l&#39;oggetto `com.adobe.idp.Document` , è possibile convertire di esso nei seguenti formati:

* Un `java.io.File` oggetto
* Un `java.io.InputStream` oggetto
* Matrice di byte

La riga di codice seguente converte un oggetto `com.adobe.idp.Document` in un oggetto `java.io.InputStream`. Si supponga che `myPDFDocument` rappresenti un oggetto `com.adobe.idp.Document`:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Analogamente, è possibile copiare il contenuto di un `com.adobe.idp.Document` in un file locale eseguendo le attività seguenti:

1. Creare un oggetto `java.io.File`.
1. Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passa l&#39;oggetto `java.io.File`.

Esempio Nell&#39;esempio di codice riportato di seguito il contenuto di un oggetto `com.adobe.idp.Document` viene copiato in un file denominato *AnotherMap.pdf*.

**Copia del contenuto di un oggetto documento in un file**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulta anche**

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinazione del tipo di contenuto di un documento {#determining-the-content-type-of-a-document}

Determinare il tipo MIME di un oggetto `com.adobe.idp.Document` richiamando il metodo `getContentType` dell&#39;oggetto `com.adobe.idp.Document`. Questo metodo restituisce un valore stringa che specifica il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`. Nella tabella seguente sono descritti i diversi tipi di contenuto restituiti da AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Tipo MIME</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>documento PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML Data Packaging (XDP), utilizzato per i moduli XFA (XML Forms Architecture) esportati</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Segnalibri, allegati o altri documenti XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms Data Format (FDF), utilizzato per i moduli Acrobat esportati</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms Data Format (XFDF), utilizzato per i moduli Acrobat esportati</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Formato dati formattato e XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Formato dati generico</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Tipo MIME non specificato</p></td>
  </tr>
 </tbody>
</table>

Esempio Nell&#39;esempio di codice seguente viene determinato il tipo di contenuto di un oggetto `com.adobe.idp.Document`.

**Determinazione del tipo di contenuto di un oggetto Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulta anche**

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminazione di oggetti documento {#disposing-document-objects}

Quando non è più necessario un oggetto `Document`, è consigliabile eliminarlo richiamando il relativo metodo `dispose`. Ogni oggetto `Document` utilizza un descrittore di file e fino a 75 MB di spazio RAM sulla piattaforma host dell&#39;applicazione. Se un oggetto `Document` non viene eliminato, il processo dell&#39;insieme Java Garage lo elimina. Tuttavia, eliminandola prima utilizzando il metodo `dispose`, è possibile liberare la memoria occupata dall&#39;oggetto `Document`.

**Consulta anche**

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Richiamare un servizio utilizzando una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Richiamare un servizio utilizzando una libreria client Java {#invoking-a-service-using-a-java-client-library}

Le operazioni del servizio AEM Forms possono essere richiamate utilizzando l’API fortemente tipizzata di un servizio, nota come libreria client Java. Una *libreria client Java* è un insieme di classi concrete che forniscono accesso ai servizi distribuiti nel contenitore di servizi. Si crea un&#39;istanza di un oggetto Java che rappresenta il servizio da richiamare anziché creare un oggetto `InvocationRequest` utilizzando l&#39;API di chiamata. L’API di richiamo viene utilizzata per richiamare i processi creati in Workbench, ad esempio quelli di lunga durata. (Vedi [Richiamare Processi A Lunga Durata Incentrati Sull&#39;Uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Per eseguire un&#39;operazione di servizio, richiamare un metodo che appartiene all&#39;oggetto Java. Una libreria client Java contiene metodi che in genere associano uno a uno le operazioni del servizio. Quando utilizzi una libreria client Java, imposta le proprietà di connessione richieste. (Vedere [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)

Dopo aver impostato le proprietà di connessione, creare un oggetto `ServiceClientFactory` utilizzato per creare un&#39;istanza di un oggetto Java che consenta di richiamare un servizio. Ogni servizio che ha una libreria client Java ha un oggetto client corrispondente. Ad esempio, per richiamare il servizio Repository, creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. L&#39;oggetto `ServiceClientFactory` è responsabile della gestione delle impostazioni di connessione necessarie per richiamare i servizi AEM Forms.

Sebbene l&#39;ottenimento di un `ServiceClientFactory` sia in genere veloce, quando si utilizza la fabbrica per la prima volta si verifica un sovraccarico. Questo oggetto è ottimizzato per il riutilizzo e quindi, quando possibile, utilizza lo stesso oggetto `ServiceClientFactory` quando si creano più oggetti client Java. In altre parole, non creare un oggetto `ServiceClientFactory` separato per ogni oggetto libreria client creato.

È presente un&#39;impostazione di User Manager che controlla la durata dell&#39;asserzione SAML all&#39;interno dell&#39;oggetto `com.adobe.idp.Context` che influisce sull&#39;oggetto `ServiceClientFactory`. Questa impostazione controlla tutte le durate del contesto di autenticazione in AEM Forms, incluse tutte le chiamate eseguite utilizzando l’API Java. Per impostazione predefinita, il periodo di tempo in cui un oggetto `ServiceCleintFactory` può essere utilizzato è di due ore.

>[!NOTE]
>
>Per spiegare come richiamare un servizio utilizzando l&#39;API Java, viene richiamata l&#39;operazione `writeResource` del servizio Repository. Questa operazione inserisce una nuova risorsa nel archivio.

È possibile richiamare il servizio Repository utilizzando un client Java libreria ed eseguendo i seguenti passaggi:

1. Includi file JAR client, come adobe-archivio-client.jar, nel percorso della classe del progetto Java. Per informazioni sul percorso di questi file, consultate [Inclusione AEM Forms file](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) libreria Java.
1. Impostare le proprietà di connessione necessarie per richiamare un servizio.
1. Creare un oggetto `ServiceClientFactory` richiamando il metodo `createInstance` statico dell&#39;oggetto `ServiceClientFactory` e passando l&#39;oggetto `java.util.Properties` che contiene le proprietà di connessione.
1. Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. Utilizzare l&#39;oggetto per richiamare le `ResourceRepositoryClient` operazioni del servizio Repository.
1. Crea un oggetto utilizzando il `RepositoryInfomodelFactoryBean` relativo costruttore e passa `null`. Questo oggetto consente di creare un `Resource` oggetto che rappresenta il contenuto aggiunto al archivio.
1. Crea un `Resource` oggetto richiamando il metodo dell&#39;oggetto `RepositoryInfomodelFactoryBean` `newImage` e trasmettendo i seguenti valori:

   * Un valore ID univoco specificando `new Id()`.
   * Un valore UUID univoco specificando `new Lid()`.
   * Nome della risorsa. È possibile specificare il nome del file XDP.

   Eseguire il cast del valore restituito in `Resource`.

1. Creare un oggetto `ResourceContent` richiamando il metodo `newImage` dell&#39;oggetto `RepositoryInfomodelFactoryBean` ed eseguendo il cast del valore restituito in `ResourceContent`. Questo oggetto rappresenta il contenuto aggiunto al repository.
1. Creare un oggetto `com.adobe.idp.Document` passando un oggetto `java.io.FileInputStream` che memorizza il file XDP da aggiungere al repository. (Vedi [Creazione di un documento basato su un oggetto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Aggiungere il contenuto dell&#39;oggetto `com.adobe.idp.Document` all&#39;oggetto `ResourceContent` richiamando il metodo `setDataDocument` dell&#39;oggetto `ResourceContent`. Passa l&#39;oggetto `com.adobe.idp.Document`.
1. Impostare il tipo MIME del file XDP da aggiungere al repository richiamando il metodo `setMimeType` dell&#39;oggetto `ResourceContent` e passando `application/vnd.adobe.xdp+xml`.
1. Aggiungere il contenuto dell&#39;oggetto `ResourceContent` all&#39;oggetto `Resource` richiamando il metodo `setContent` dell&#39;oggetto `Resource` e passando l&#39;oggetto `ResourceContent`.
1. Aggiungere una descrizione della risorsa richiamando il metodo `setDescription` dell&#39;oggetto `Resource` e passando un valore stringa che rappresenta una descrizione della risorsa.
1. Aggiungere la struttura del modulo al repository richiamando il metodo `writeResource` dell&#39;oggetto `ResourceRepositoryClient` e passando i valori seguenti:

   * Valore stringa che specifica il percorso della raccolta di risorse contenente la nuova risorsa
   * L&#39;oggetto `Resource` creato

**Consulta anche**

[Quick Start (modalità EJB): scrittura di una risorsa utilizzando l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Richiamare AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Richiamare un processo di breve durata utilizzando l’API di richiamo {#invoking-a-short-lived-process-using-the-invocation-api}

È possibile richiamare un processo di breve durata utilizzando l’API di chiamata Java. Quando si richiama un processo di breve durata utilizzando l&#39;API di chiamata, si trasmettono i valori dei parametri richiesti utilizzando un oggetto `java.util.HashMap`. Per ogni parametro da passare a un servizio, richiamare il metodo `put` dell&#39;oggetto `java.util.HashMap` e specificare la coppia nome-valore richiesta dal servizio per eseguire l&#39;operazione specificata. Specificare il nome esatto dei parametri che appartengono al processo di breve durata.

>[!NOTE]
>
>Per informazioni sul richiamo di un processo di lunga durata, vedere [Richiamo di processi di lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discussione qui riguarda l&#39;utilizzo dell&#39;API di richiamo per richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

### Richiama il processo MyApplication/EncryptDocument di breve durata utilizzando l’API di chiamata Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Richiama il processo di breve durata `MyApplication/EncryptDocument` utilizzando l&#39;API di chiamata Java:

1. Includi i file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java. (Vedi [Inclusione dei file della libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Creare un oggetto `ServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. Un oggetto `ServiceClient` consente di richiamare un&#39;operazione di servizio. Gestisce attività quali l’individuazione, l’invio e l’instradamento delle richieste di chiamata.
1. Creare un oggetto `java.util.HashMap` utilizzando il relativo costruttore.
1. Richiama il metodo `put` dell&#39;oggetto `java.util.HashMap` per ogni parametro di input da passare al processo di lunga durata. Poiché il processo di breve durata `MyApplication/EncryptDocument` richiede un parametro di input di tipo `Document`, è necessario richiamare il metodo `put` una sola volta, come illustrato nell&#39;esempio seguente.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Creare un oggetto `InvocationRequest` richiamando il metodo `createInvocationRequest` dell&#39;oggetto `ServiceClientFactory` e passando i valori seguenti:

   * Valore stringa che specifica il nome del processo di lunga durata da richiamare. Per richiamare il processo `MyApplication/EncryptDocument`, specificare `MyApplication/EncryptDocument`.
   * Valore stringa che rappresenta il nome dell&#39;operazione di processo. In genere il nome di un&#39;operazione di processo di breve durata è `invoke`.
   * L&#39;oggetto `java.util.HashMap` che contiene i valori dei parametri richiesti dall&#39;operazione del servizio.
   * Un valore booleano che specifica `true`, che crea una richiesta sincrona (questo valore è applicabile per richiamare un processo di breve durata).

1. Inviare la richiesta di chiamata al servizio richiamando il metodo `invoke` dell&#39;oggetto `ServiceClient` e passando l&#39;oggetto `InvocationRequest`. Il metodo `invoke` restituisce un oggetto `InvocationReponse`.

   >[!NOTE]
   >
   >È possibile richiamare un processo di lunga durata passando il valore `false` come quarto parametro del metodo `createInvocationRequest`. Il passaggio del valore `false`*crea una richiesta asincrona.*

1. Recuperare il valore restituito dal processo richiamando il metodo `getOutputParameter` dell&#39;oggetto `InvocationReponse` e passando un valore stringa che specifica il nome del parametro di output. In questa situazione, specificare `outDoc` ( `outDoc` è il nome del parametro di output per il processo `MyApplication/EncryptDocument`). Eseguire il cast del valore restituito su `Document`, come illustrato nell&#39;esempio seguente.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
1. Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getOutputParameter`.

**Consulta anche**

[Guida introduttiva: richiamare un processo di breve durata utilizzando l’API di chiamata](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Richiamare processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusione dei file della libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
