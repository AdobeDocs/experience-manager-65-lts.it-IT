---
title: Componenti e servizi Java&trade; APIQuick Start (SOAP)
description: Scopri come manipolare in modo programmatico componenti e servizi di AEM Forms utilizzando Java&trade; API Quick Start (SOAP).
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: 5a69b9e7-10f1-4637-9a29-228e12863333
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Guida introduttiva all’API Java™ per componenti e servizi (SOAP) {#components-and-services-java-apiquick-start-soap}

Java™ API Quick Start (SOAP) è disponibile per componenti e servizi.


[Guida rapida (modalità SOAP): distribuzione di un componente tramite Java](components-services-java-api-quick.md#quick-start-soap-mode-deploying-a-component-using-the-java-api)

[Quick Start (modalità SOAP): impostazione del contesto di esecuzione di un servizio utilizzando Java](components-services-java-api-quick.md#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api)

[Quick Start (modalità SOAP): disabilitazione della sicurezza del servizio tramite Java](components-services-java-api-quick.md#quick-start-soap-mode-disabling-service-security-using-the-java-api)

[Quick Start (modalità SOAP): avvio di un servizio utilizzando Java](components-services-java-api-quick.md#quick-start-soap-mode-starting-a-service-using-the-java-api)

[Guida rapida (modalità SOAP): modifica dei valori di configurazione del servizio tramite Java](components-services-java-api-quick.md#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api)

[Guida rapida (modalità SOAP): rimozione di componenti tramite Java](components-services-java-api-quick.md#quick-start-soap-mode-removing-components-using-the-java-api)


Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>Non è possibile manipolare componenti e servizi a livello di programmazione utilizzando i servizi Web.

>[!NOTE]
>
>Gli avvii rapidi nella programmazione con i moduli di AEM si basano sul server Forms distribuito su JBoss® e sul sistema operativo Windows. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX®, sostituire i percorsi specifici di Windows con i percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

>[!NOTE]
>
>Se si dispone di un componente personalizzato e si utilizzano protocolli SOAP o EJB per richiamare DSC sullo stesso server locale e tali chiamate smettono di funzionare dopo un aggiornamento, utilizzare la strategia di chiamata in-VM. Utilizzare il metodo di chiamata DSC in-VM con ServiceClientFactory predefinito e non creare ServiceClientFactory utilizzando i protocolli SOAP o EJB.

## Guida rapida (modalità SOAP): distribuzione di un componente tramite l’API Java™ {#quick-start-soap-mode-deploying-a-component-using-the-java-api}

Nell&#39;esempio Java™ seguente viene distribuito un componente basato su un file JAR denominato *adobe-emailSample-dsc.jar*.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode)
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
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
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class DeployComponents { 
  
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
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Reference a JAR file that represents the component to deploy 
         //    FileInputStream componentFile = new FileInputStream("C:\\Adobe\adobe-emailSample-dsc.jar");  
              
             FileInputStream componentFile = new FileInputStream("C:\\A22\Bank.jar");  
             Document component = new Document(componentFile);  
              
             //Install the component 
             Component myComponent = componentReg.install(component); 
             componentReg.start(myComponent); 
              
             System.out.println("The component has been deployed");  
             } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## Quick Start (modalità SOAP): impostazione del contesto di esecuzione di un servizio utilizzando l’API Java™ {#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente il contesto di esecuzione di RunAs Invoker viene impostato su un servizio di esempio denominato *EncryptDocument*.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar  
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
        * The JBoss files must be kept in the jboss\bin\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * 
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
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start sets the Run-As Invoker to a service named EncryptDocument 
     */ 
 public class SetRunAsConfiguration { 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument service 
         ServiceConfiguration _config  = _src.getHeadActiveConfiguration("EncryptDocument"); 
          
         //Set the RUN_AS_INVOKER execution context 
         ModifyServiceConfigurationInfo _configModifyInfo = new ModifyServiceConfigurationInfo(); 
         _configModifyInfo.setServiceId(_config.getServiceId()); 
         _configModifyInfo.setMajorVersion(_config.getMajorVersion()); 
         _configModifyInfo.setMinorVersion(_config.getMinorVersion()); 
         _configModifyInfo.setRunAsConfiguration(ServiceConfiguration.RUN_AS_INVOKER); 
         _config = _src.modifyConfiguration(_configModifyInfo); 
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## Quick Start (modalità SOAP): disabilitazione della sicurezza del servizio tramite l’API Java™ {#quick-start-soap-mode-disabling-service-security-using-the-java-api}

Esempio Nell&#39;esempio di codice Java™ riportato di seguito viene disattivata la protezione dal servizio EncryptDocument di esempio e dai servizi richiamati all&#39;interno di questo servizio, ovvero i servizi Imposta valore e Crittografia.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
* 
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to 
        * your local development environment and then include the 3 JBoss JAR files in your class path 
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
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start disables security from the EncryptDocument process 
     * and each service that is in this process 
     */ 
 public class DisableSecurity{ 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                      
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument process and each service that is  
         //invoked from within the EncryptDocument process 
         ServiceConfiguration encryptDocumentService  = _src.getHeadActiveConfiguration("EncryptDocument"); 
         ServiceConfiguration setValueService  = _src.getHeadActiveConfiguration("SetValue"); 
         ServiceConfiguration encryptionService  = _src.getHeadActiveConfiguration("EncryptionService"); 
          
         //Create a ModifyServiceInfo object 
         ModifyServiceInfo si = new ModifyServiceInfo(); 
          
         //Disable security from the EncryptDocument service 
         si.setId(encryptDocumentService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the SetValue service 
         si.setId(setValueService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the EncryptionService 
         si.setId(encryptionService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
              
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## Quick Start (modalità SOAP): avvio di un servizio utilizzando l’API Java™ {#quick-start-soap-mode-starting-a-service-using-the-java-api}

Il codice Java™ seguente avvia un servizio denominato *SendEmailService*.

```java
 package com.adobe.sample.servicemanager; 
  
 /** 
     * This Java Quick Start uses the following JAR files: 
     * 1. adobe-livecycle-client.jar 
     * 2. adobe-usermanager-client.jar 
     * 3. adobe-workflow-client-sdk.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if AEM Forms is not deployed on Jboss) 
     * 6. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     * 7. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 public class StartService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms      
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadActiveConfiguration("SendEmailService"); 
          
             //Start the SendEmailService 
             serviceReg.start(myServiceConfig); 
             } 
              
                 catch(Exception e) 
                 { 
                     e.printStackTrace(); 
                 } 
     } 
 } 
  
 
```

## Quick Start (modalità SOAP): modifica dei valori di configurazione di un servizio utilizzando l’API Java™ {#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api}

Nell&#39;esempio Java™ seguente vengono modificati i valori di configurazione che appartengono al servizio SendEmail.

```java
 /* 
     * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
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
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ConfigParameter; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
  
 public class ModifyService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms     
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadServiceConfiguration("SendEmailService"); 
                              
             //Create a ModifyServiceConfigurationInfo object 
                 ModifyServiceConfigurationInfo modService = new ModifyServiceConfigurationInfo(); 
                      
             //Set configuration values required by the SendEmailService 
             String serviceId = myServiceConfig.getServiceId(); 
             modService.setServiceId(serviceId); 
             modService.setMajorVersion(1); 
             modService.setConfigParameterAsText("smtpHost","mySMTPSERVER"); 
             modService.setConfigParameterAsText("smtpUser","smyUserName");     
             modService.setConfigParameterAsText("smtpPassword","myPassword");     
                      
             //Modify the service's configuration values 
             serviceReg.modifyConfiguration(modService); 
                          
             //Conform the new configuration values 
             ServiceConfiguration serviceConfig = serviceReg.getServiceConfiguration("SendEmailService",1,0); 
             ConfigParameter cp = serviceConfig.getConfigParameter("smtpUser"); 
             String configValue = cp.getTextValue();  
             System.out.println(configValue); 
             } 
      
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```

## Guida rapida (modalità SOAP): rimozione di componenti tramite l’API Java™ {#quick-start-soap-mode-removing-components-using-the-java-api}

Il seguente esempio di codice Java™ rimuove un componente utilizzando l’API Java™.

```java
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-taskmanager-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed 
     * on JBoss) 
     * 6. commons-code-1.3.jar 
     * 7. adobe-workflow-client-sdk.jar 
     * 8. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     * 9. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
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
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class RemoveComponent { 
  
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
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Retrieve the Id of the component to remove from the service container 
             Component myComponent = componentReg.getComponent("com.adobe.livecycle.sample.email.emailSampleComponent", "1.0"); 
              
             //Determine if the component is in a running state 
             if (myComponent.getState()== Component.RUNNING) 
             { 
                 //Stop the component 
                 Component stoppedComponent = componentReg.stop(myComponent); 
                  
                 //Uninstall the component 
                 componentReg.uninstall(stoppedComponent); 
             } 
             else 
                 componentReg.uninstall(myComponent); 
                  
             System.out.println("The component was removed."); 
             } 
              
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```
