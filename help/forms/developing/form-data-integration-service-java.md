---
title: Servizio di integrazione dei dati dei moduli - Guida introduttiva JavaAPI (SOAP)
description: Utilizza il servizio Integrazione dati modulo per importare dati in un modulo PDF ed esportare dati da un modulo PDF utilizzando l’API Java.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: 1f67fad6-263c-4ee4-9986-1b3df53e1a16
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Servizio di integrazione dei dati dei moduli - Guida introduttiva all’API Java (SOAP) {#form-data-integration-service-javaapi-quick-start-soap}

Per il servizio di integrazione dei dati del modulo sono disponibili i seguenti Quick Start.

[Quick Start (modalità SOAP): importazione di dati dai moduli tramite API Java](form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Quick Start (modalità SOAP): esportazione di dati modulo tramite API Java](form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>La Guida introduttiva alla programmazione con AEM Form si basa sul server Forms distribuito su JBoss Application Server e sul sistema operativo Microsoft Windows. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Quick Start (modalità SOAP): importazione di dati dai moduli tramite API Java {#quick-start-soap-mode-importing-form-data-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito i dati vengono importati in un modulo PDF. I dati si trovano in un file XML denominato *Loan_data.xml* e il modulo PDF viene salvato come file PDF denominato *ResultLoanForm.pdf*. (Vedi [Importazione dei dati del modulo](/help/forms/developing/importing-exporting-data.md#importing-form-data).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-formdataintegration-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.formdataintegration.client.*;
 
 public class ImportDataSOAP {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
              //Create a ServiceClientFactory object
              ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormDataIntegrationClient object
             FormDataIntegrationClient dataClient = new FormDataIntegrationClient(myFactory);
 
             //Import XDP XML data into an XFA PDF document
             //Reference an XFA PDF form
             FileInputStream inputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inputPDF = new Document(inputStream);
 
             FileInputStream dataInput = new FileInputStream("C:\\Adobe\Loan_data.xml");
             Document inputDataFile = new Document(dataInput);
 
             //Import data into the form
             Document resultPDF = dataClient.importData(inputPDF,inputDataFile);
 
             //Save the PDF file
             File resultFile = new File("C:\\Adobe\ResultLoanForm.pdf");
             resultPDF.copyToFile(resultFile);
 
         }catch (Exception e) {
              e.printStackTrace();
         }
       }
     }
 
```

## Quick Start (modalità SOAP): esportazione di dati modulo tramite API Java {#quick-start-soap-mode-exporting-form-data-using-the-java-api}

Esempio Nell&#39;esempio di codice Java riportato di seguito i dati vengono esportati da un modulo di PDF. I dati del modulo vengono salvati come file XML denominato *Loan_data.xml*. (Vedi [Esportazione dei dati del modulo](/help/forms/developing/importing-exporting-data.md#exporting-form-data).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-formdataintegration-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.formdataintegration.client.*;
 
 public class ExportDataSOAP {
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
          //Create a ServiceClientFactory object
          ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
          //Create a FormDataIntegrationClient object
          FormDataIntegrationClient dataClient = new FormDataIntegrationClient(myFactory);
 
          //Reference a PDF form from which to export data
          FileInputStream fileInputStream2 = new FileInputStream("C:\\Adobe\LoanForm.pdf");
          Document inputPDF = new Document(fileInputStream2);
 
          //Export data from the form
          Document resultPDF = dataClient.exportData(inputPDF);
 
          //Save the exported form data as an XML file
          File resultFile = new File("C:\\Adobe\Loan_data.xml");
          resultPDF.copyToFile(resultFile);
 
     }catch (Exception e) {
              e.printStackTrace();
         }
     }
 }
```
