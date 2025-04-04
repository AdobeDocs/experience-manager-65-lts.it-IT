---
title: Collegamento di AEM Forms con Adobe LiveCycle
description: Il connettore Adobe Experience Manager (AEM) LiveCycle consente di avviare i servizi Acrobat di LiveCycle ES4 dall’interno delle app e dei flussi di lavoro AEM.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
exl-id: f6530bd3-16cd-4d6b-b92b-6c96f01f1939
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# Collegamento di AEM Forms con Adobe LiveCycle {#connecting-aem-forms-with-adobe-livecycle}

Il connettore Adobe Experience Manager (AEM) LiveCycle consente di invocare facilmente i servizi Acrobat di Adobe LiveCycle ES4 dall’interno delle app web e dei flussi di lavoro di AEM. LiveCycle fornisce un SDK client avanzato, che consente alle applicazioni client di avviare i servizi LiveCycle utilizzando le API Java™. Il connettore AEM LiveCycle semplifica l’utilizzo di queste API all’interno dell’ambiente OSGi.

## Connessione del server AEM ad Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector fa parte del pacchetto del componente aggiuntivo [AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Dopo aver installato il pacchetto del componente aggiuntivo AEM Forms, effettua le seguenti operazioni per aggiungere i dettagli del server LiveCycle alla console web di AEM.

1. Nel gestore di configurazione della console web AEM, individua il componente di configurazione Adobe LiveCycle Client SDK.
1. Fai clic sul componente per modificare l’URL, il nome utente e la password del server di configurazione.
1. Rivedi le impostazioni e fai clic su **Salva**.

Anche se le proprietà sono auto-esplicative, quelle importanti sono le seguenti:

* **URL server** - Specifica l&#39;URL del server LiveCycle. Se desideri che LiveCycle e AEM comunichino tramite https, avvia AEM con la seguente JVM

  ```java
  argument
   -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
  ```

  opzione.

* **Nome utente**- Specifica il nome utente dell&#39;account utilizzato per stabilire la comunicazione tra AEM e LiveCycle. L&#39;account è un account utente di LiveCycle che dispone delle autorizzazioni necessarie per avviare Acrobat Services.
* **Password**- Specifica la password.
* **Nome servizio** - Specifica i servizi avviati utilizzando le credenziali utente fornite nei campi Nome utente e Password. Per impostazione predefinita, non vengono passate credenziali durante l&#39;avvio dei servizi LiveCycle.

## Avvio dei servizi documentali {#starting-document-services}

Le applicazioni client possono avviare in modo programmatico i servizi LiveCycle utilizzando un&#39;API Java™, i servizi Web, le funzionalità remote e REST. Per i client Java™, l&#39;applicazione può utilizzare LiveCycle SDK. Il SDK LiveCycle fornisce un&#39;API Java™ per avviare questi servizi in remoto. Ad esempio, per convertire un documento di Microsoft® Word in PDF, il client avvia GeneratePDFService. Il flusso di chiamata è costituito dai seguenti passaggi:

1. Creare un&#39;istanza ServiceClientFactory.
1. Ogni servizio fornisce una classe client. Per avviare un servizio, crea un’istanza client del servizio.
1. Avvia il servizio ed elabora il risultato.

Il connettore AEM LiveCycle semplifica il flusso esponendo queste istanze client come servizi OSGi a cui è possibile accedere utilizzando gli strumenti OSGi standard. Il connettore LiveCycle fornisce le seguenti funzionalità:

* Istanze client come servizio OSGi: i client inclusi nel pacchetto come bundle OSGI sono elencati nella sezione [Elenco dei servizi Acrobat](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Ogni file jar del client registra l’istanza client come servizio OSGi con il registro del servizio OSGi.
* Propagazione credenziali utente: i dettagli di connessione necessari per connettersi al server LiveCycle vengono gestiti da una posizione centrale.
* ServiceClientFactory: per avviare i processi, l&#39;applicazione client può accedere all&#39;istanza ServiceClientFactory.

### Avvio tramite riferimenti al servizio dal registro del servizio OSGi {#starting-via-service-references-from-osgi-service-registry}

Per avviare un servizio esposto da AEM, effettua le seguenti operazioni:

1. Determina le dipendenze Maven. Aggiungi la dipendenza al file jar client richiesto nel file pom.xml maven. Come minimo, aggiungi la dipendenza ai file jar adobe-livecycle-client e adobe-usermanager-client.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   Per avviare un servizio, aggiungi una dipendenza Maven corrispondente al servizio. Per l&#39;elenco delle dipendenze, vedere [Elenco dei servizi Acrobat](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Ad esempio, per il servizio Genera PDF, aggiungi la seguente dipendenza:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Ottenere il riferimento del servizio. Ottieni un handle per l’istanza del servizio. Se si scrive una classe Java™, è possibile utilizzare le annotazioni Declarative Services.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   Lo snippet di codice riportato sopra avvia l’API createPDF di GeneratePdfServiceClient per convertire un documento in PDF. È possibile eseguire una chiamata simile in una JSP utilizzando il codice seguente. La differenza principale consiste nel fatto che il codice seguente utilizza Sling ScriptHelper per accedere a GeneratePdfServiceClient.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### Avvio tramite ServiceClientFactory {#starting-via-serviceclientfactory}

La classe ServiceClientFactory è a volte obbligatoria. Ad esempio, è necessario ServiceClientFactory per chiamare i processi.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Supporto RunAs {#runas-support}

Quasi tutti i servizi Acrobat in LiveCycle richiedono l&#39;autenticazione. Per avviare questi servizi senza fornire credenziali esplicite nel codice, puoi utilizzare una delle seguenti opzioni:

### Configurazione del Inserisco nell&#39;elenco Consentiti di {#allowlist-configuration}

La configurazione del SDK client LiveCycle contiene un&#39;impostazione relativa ai nomi dei servizi. Questa configurazione è un elenco di servizi per i quali la logica di chiamata utilizza credenziali di amministratore predefinite. Ad esempio, se si aggiungono i servizi DirectoryManager (parte dell&#39;API User Management) a questo elenco, qualsiasi codice client può utilizzare direttamente il servizio. Inoltre, il livello di chiamata trasmette automaticamente le credenziali configurate come parte della richiesta inviata al server LiveCycle.

### RunAsManager {#runasmanager}

Come parte dell’integrazione, viene fornito un nuovo servizio RunAsManager. Consente di controllare a livello di programmazione una credenziale da utilizzare per la chiamata al server LiveCycle.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

Se si desidera passare una credenziale diversa, è possibile utilizzare il metodo di overload che accetta un&#39;istanza PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest, proprietà {#invocationrequest-property}

Se si chiama un processo o si utilizza direttamente la classe ServiceClientFactory e si crea un oggetto InvocationRequest, è possibile specificare una proprietà per indicare che il livello di chiamata deve utilizzare credenziali configurate.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Elenco servizi Acrobat {#document-services-list}

### Pacchetto API SDK client Adobe LiveCycle {#adobe-livecycle-client-sdk-api-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dipendenze Maven {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle SDK client Adobe LiveCycle {#adobe-livecycle-client-sdk-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dipendenze Maven {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle TaskManager {#adobe-livecycle-taskmanager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dipendenze Maven {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client flusso di lavoro Adobe LiveCycle {#adobe-livecycle-workflow-client-bundle}

È disponibile il seguente servizio:

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Dipendenze Maven {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle PDF Generator {#adobe-livecycle-pdf-generator-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Dipendenze Maven {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dipendenze Maven {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client assemblatore Adobe LiveCycle {#adobe-livecycle-assembler-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dipendenze Maven {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client di integrazione dei dati di Adobe LiveCycle Form {#adobe-livecycle-form-data-integration-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dipendenze Maven {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Forms {#adobe-livecycle-forms-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Dipendenze Maven {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client di output Adobe LiveCycle {#adobe-livecycle-output-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.output.client.OutputClient

#### Dipendenze Maven {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client estensioni Adobe LiveCycle {#adobe-livecycle-reader-extensions-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Dipendenze Maven {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dipendenze Maven {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client firme Adobe LiveCycle {#adobe-livecycle-signatures-client-bundle}

È disponibile il seguente servizio:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dipendenze Maven {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacchetto client TrustStore Adobe LiveCycle {#adobe-livecycle-truststore-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dipendenze Maven {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Bundle client dell’archivio di Adobe LiveCycle {#adobe-livecycle-repository-client-bundle}

Sono disponibili i seguenti servizi:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dipendenze Maven {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
