---
title: Guida introduttiva JavaAPI Service di Application Manager (SOAP)
description: Guida introduttiva JavaAPI Service di Application Manager (SOAP)
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: 4b7d417f-6480-479e-9b8d-bcf2c9790a97
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Guida introduttiva JavaAPI Service di Application Manager (SOAP) {#application-manager-service-javaapi-quick-start-soap}

Java API Quick Start(SOAP) è disponibile per il servizio Application Manager.

[Guida introduttiva: Distribuzione di applicazioni tramite API Java (SOAP)](application-manager-service-java-api.md#quick-start-soap-mode-deploying-applications-using-the-java-api)

[Guida rapida: rimozione di un’applicazione tramite API Java (SOAP)](application-manager-service-java-api.md#quick-start-soap-mode-removing-an-application-using-the-java-api)

>[!NOTE]
>
>Le API di Application Manager supportano solo i file LCA di AEM Forms. Non supporta i file LCA di LiveCycle ES2 e ES4.

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>La Guida introduttiva di Java API (SOAP) nella programmazione con AEM Forms si basa su Forms se si utilizza un altro sistema operativo, ad esempio Unix, per sostituire i percorsi specifici di Windows con i percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Guida rapida (modalità SOAP): distribuzione di applicazioni tramite l’API Java {#quick-start-soap-mode-deploying-applications-using-the-java-api}

Esempio Nell&#39;esempio di codice Java seguente viene importata un&#39;applicazione basata su un file LCA esistente denominato *EncryptDocument.lca*.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     * 3. activation.jar (required for SOAP mode)
     * 4. axis.jar (required for SOAP mode)
     * 5. commons-codec-1.3.jar (required for SOAP mode)
     * 6. commons-collections-3.2.jar  (required for SOAP mode)
     * 7. commons-discovery.jar (required for SOAP mode)
     * 8. commons-logging.jar (required for SOAP mode)
     * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 11. jaxrpc.jar (required for SOAP mode)
     * 12. log4j.jar (required for SOAP mode)
     * 13. mail.jar (required for SOAP mode)
     * 14. saaj.jar (required for SOAP mode)
     * 15. wsdl4j.jar (required for SOAP mode)
     * 16. xalan.jar (required for SOAP mode)
     * 17. xbean.jar (required for SOAP mode)
     * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-workflow-client-sdk.jar
     * 20. adobe-applicationmanager-client-sdk.jar
 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     */
 
 import java.io.FileInputStream;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.applicationmanager.application.ApplicationStatus;
 import com.adobe.idp.applicationmanager.client.ApplicationManager;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class DeployApplication {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Get the AEM Forms application to deploy
             FileInputStream fileApp = new FileInputStream("C:\\Adobe\EncryptDocument.lca");
             Document lcApp = new Document(fileApp);
 
             //Create an ApplicationManager object
             ApplicationManager appManager = new ApplicationManager(myFactory);
 
             //Import the application into the production server
             ApplicationStatus appStatus = appManager.importApplicationArchive(lcApp);
             int status = appStatus.getStatusCode();
 
             //Determine if the application was successfully deployed
             if (status==1)
                     System.out.println("The application was successfully deployed");
             else
                     System.out.println("The application was not successfully deployed. The status is "+status);
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## Guida rapida (modalità SOAP): rimozione di un’applicazione tramite l’API Java {#quick-start-soap-mode-removing-an-application-using-the-java-api}

Nell&#39;esempio di codice Java seguente viene rimossa un&#39;applicazione denominata *EncryptDocument*.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     * 3. activation.jar (required for SOAP mode)
     * 4. axis.jar (required for SOAP mode)
     * 5. commons-codec-1.3.jar (required for SOAP mode)
     * 6. commons-collections-3.2.jar  (required for SOAP mode)
     * 7. commons-discovery.jar (required for SOAP mode)
     * 8. commons-logging.jar (required for SOAP mode)
     * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 11. jaxrpc.jar (required for SOAP mode)
     * 12. log4j.jar (required for SOAP mode)
     * 13. mail.jar (required for SOAP mode)
     * 14. saaj.jar (required for SOAP mode)
     * 15. wsdl4j.jar (required for SOAP mode)
     * 16. xalan.jar (required for SOAP mode)
     * 17. xbean.jar (required for SOAP mode)
     * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-workflow-client-sdk.jar
     * 20. adobe-applicationmanager-client-sdk.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     */
 
 
 import java.util.*;
 
 import com.adobe.idp.applicationmanager.application.Application;
 import com.adobe.idp.applicationmanager.application.ApplicationId;
 
 import com.adobe.idp.applicationmanager.client.ApplicationManager;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RemoveApplication {
 
     public static void main(String[] args) {
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ComponentRegistryClient object
             ApplicationManager appManager = new ApplicationManager(myFactory);
 
             //Get all the deployed applications
             List allApps = appManager.getApplications();
 
             //Iterate through the applications
             Iterator iter= allApps.iterator();
             while (iter.hasNext()) {
 
              //Cast each element to an Application object
              Application myApplication  = (Application)iter.next();
              ApplicationId appID = myApplication.getApplicationId();
              String appName = appID.getApplicationName();
 
              System.out.println("The name of the AEM Forms application is "+ appID.getApplicationName());
              //Determine the name of the application
              if (appName.compareTo("EncryptDocument")==0)
              {
                  //Remove the application
                 appManager.removeApplication(appID);
                 System.out.println("The  "+ appID.getApplicationName() +" application was removed.");
              }
         }
         }
         catch(Exception e)
             {
             e.printStackTrace();
             }
     }
 }
 
```
