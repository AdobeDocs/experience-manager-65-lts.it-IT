---
title: Servizio di crittografia Java&trade; API QuickStart(SOAP)
description: Scopri come crittografare, rimuovere la crittografia basata su password/certificato, sbloccare e determinare il tipo di crittografia per i documenti PDF utilizzando Java&trade; API in modalità SOAP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: 4ad47959-fe48-4cff-9a54-9a9749cf3d6f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Guida introduttiva all&#39;API Java™ del servizio di crittografia (SOAP) {#encryption-service-java-api-quickstart-soap}

[Guida rapida (modalità SOAP): crittografia di un documento PDF tramite Java](encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Quick Start (modalità SOAP): rimozione della crittografia basata su password tramite Java](encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

[Guida rapida (modalità SOAP): crittografia di un documento PDF con un certificato tramite Java](encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Quick Start (modalità SOAP): rimozione della crittografia basata su certificati tramite Java](encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Guida rapida (modalità SOAP): sblocco di un documento PDF crittografato tramite Java](encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)

[Guida rapida (modalità SOAP): determinazione del tipo di crittografia tramite Java](encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

Le operazioni di AEM Forms possono essere eseguite utilizzando l’API fortemente tipizzata di AEM Forms e la modalità di connessione deve essere impostata su SOAP.

>[!NOTE]
>
>Gli avvii rapidi nella programmazione con AEM Form si basano sul server Forms distribuito su JBoss® Application Server e sul sistema operativo Microsoft® Windows. Tuttavia, se si utilizza un altro sistema operativo, ad esempio UNIX®, sostituire i percorsi specifici di Windows con percorsi supportati dal sistema operativo applicabile. Analogamente, se si utilizza un altro server applicazioni J2EE, assicurarsi di specificare proprietà di connessione valide. Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Guida rapida (modalità SOAP): crittografia di un documento PDF tramite l’API Java™ {#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente viene crittografato un documento PDF denominato *Loan.pdf* con un valore di password di `OpenPassword`. La password primaria è `PermissionPassword`. Il documento PDF protetto è stato salvato come file PDF denominato *EncryptLoan.pdf*. (Vedi [Crittografia dei documenti di PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.ArrayList;
 import java.util.List;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class PasswordEncryptPDFSoap{
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an EncryptionServiceClient object
         EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
         //Specify the PDF document to encrypt with a password
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Create a PasswordEncryptionOptionSpec object that stores encryption run-time values
         PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();
 
         //Specify the PDF document resource to encrypt
         passSpec.setEncryptOption(PasswordEncryptionOption.ALL);
 
         //Specify the permission associated with the password
         //These permissions enable data to be extracted from a password
         //protected PDF form
         List<PasswordEncryptionPermission> encrypPermissions = new ArrayList<PasswordEncryptionPermission>();
         encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_ADD);
         encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_MODIFY);
         passSpec.setPermissionsRequested(encrypPermissions);
 
         //Specify the Acrobat version
         passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);
 
         //Specify the password values
         passSpec.setDocumentOpenPassword("OpenPassword");
         passSpec.setPermissionPassword("PermissionPassword");
 
         //Encrypt the PDF document
         Document encryptDoc = encryptClient.encryptPDFUsingPassword(inDoc,passSpec);
 
         //Save the password-encrypted PDF document
         File outFile = new File("C:\\Adobe\EncryptLoan.pdf");
         encryptDoc.copyToFile (outFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## Quick Start (modalità SOAP): rimozione della crittografia basata su password tramite l’API Java™ {#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente viene rimossa la crittografia basata su password da un documento di PDF denominato *EncryptLoan.pdf*. Il valore della password primaria utilizzato per rimuovere la crittografia basata su password è *PermissionPassword*. Il documento PDF non protetto è stato salvato come file PDF denominato *noEncryptionLoan.pdf*. (Vedi [Rimozione della crittografia password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#removing-password-encryption).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class RemovePasswordFromPDFSOAP {
 
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
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the encrypted PDF from which to remove password-based encryption
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Remove password-based encryption from the PDF document
             Document encryptDoc = encryptClient.removePDFPasswordSecurity(inDoc,"PermissionPassword");
 
             //Save the unsecured PDF document
             File outFile = new File("C:\\Adobe\noEncryptionLoan.pdf");
             encryptDoc.copyToFile (outFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## Guida rapida (modalità SOAP): crittografia di un documento PDF con un certificato tramite l’API Java™ {#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente viene crittografato un documento PDF denominato *Loan.pdf* con un certificato denominato *Encryption.cer*. Il documento PDF crittografato è stato salvato come file PDF denominato *EncryptLoanCert.pdf*. (Vedi [Crittografia di documenti PDF con certificati](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.ArrayList;
 import java.util.List;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class PKIEncryptPDFSoap {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Specify the PDF document to encrypt with a certificate
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Set the List that stores PKI information
             List pkiIdentities = new ArrayList();
 
             //Set the Permission List
             List permList = new ArrayList();
             permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;
 
             //Create a Recipient object to store certificate information
             Recipient recipient = new Recipient();
 
             //Specify the private key that is used to encrypt the document
             FileInputStream fileInputStreamCert = new FileInputStream("C:\\Adobe\Encryption.cer");
             Document privateKey = new Document (fileInputStreamCert);
             recipient.setX509Cert(privateKey);
 
             //Create an EncryptionIdentity object
             CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
             encryptionId.setPerms(permList);
             encryptionId.setRecipient(recipient);
 
             //Add the EncryptionIdentity to the list
             pkiIdentities.add(encryptionId);
 
             //Set encryption run-time options
             CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
             certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
             certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_7);
 
             //Encrypt the PDF document with a certificate
             Document encryptDoc = encryptClient.encryptPDFUsingCertificates(inDoc,pkiIdentities, certOptionsSpec);
 
             //Save the encrypted PDF document
             File outFile = new File("C:\\Adobe\EncryptLoanCert.pdf");
             encryptDoc.copyToFile (outFile);
 
             }catch (Exception e) {
                 e.printStackTrace();
             }
     }
 }
 
```

## Quick Start (modalità SOAP): rimozione della crittografia basata su certificati tramite l’API Java™ {#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente viene rimossa la crittografia basata su certificati da un documento di PDF denominato *EncryptLoanCert.pdf*. L&#39;alias della chiave pubblica utilizzato per rimuovere la crittografia è `Encryption`. Il documento PDF non protetto è stato salvato come file PDF denominato *noEncryptionLoan.pdf*. (Vedi [Rimozione della crittografia basata su certificato](/help/forms/developing/encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
     * <install directory>/jboss/bin/client/jboss/bin/client
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class RemovePKIFromPDFSOAP {
 
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
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the encrypted PDF document
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoanCert.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Remove certificate-based encryption from the PDF document
             Document encryptDoc = encryptClient.removePDFCertificateSecurity(inDoc, "Encryption");
 
             //Save the unsecured PDF document
             File outFile = new File("C:\\Adobe\noEncryptionLoan.pdf");
             encryptDoc.copyToFile (outFile);
 
         }catch (Exception e) {
                 e.printStackTrace();
             }
     }
 }
```

## Guida rapida (modalità SOAP): sblocco di un documento PDF crittografato tramite l’API Java™ {#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente viene sbloccato un documento PDF crittografato con password denominato *EncryptLoan.pdf*. (Vedi [Sblocco di documenti PDF crittografati](/help/forms/developing/encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if Forms Server is not deployed
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class UnlockPDFSOAP {
 
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
 
             //Create an EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the password-encrypted PDF document to unlock
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Specify the password to open the password-encrypted PDF document
             String openPassword = "OpenPassword" ;
 
             //Unlock the password-encrypted PDF document
             Document unlockedDoc = encryptClient.unlockPDFUsingPassword(inDoc,openPassword);
 
         }catch (Exception e) {
                 System.out.println("The following error occurred during this operation " +e.getMessage());
         }
     }
 }
 
```

## Quick Start (modalità SOAP): determinazione del tipo di crittografia tramite l’API Java™ {#quick-start-soap-mode-determining-encryption-type-using-the-java-api}

Nell&#39;esempio di codice Java™ seguente viene determinato il tipo di crittografia che protegge un documento di PDF denominato *EncryptLoan.pdf*. (Vedere [Determinazione del tipo di crittografia](/help/forms/developing/encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.encryption.client.*;
 
 public class GetEncryptionTypeSOAP {
 
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
 
             //Create a EncryptionServiceClient object
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Get the PDF document
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\EncryptLoan.pdf");
             Document inDoc = new Document (fileInputStream);
 
             //Determine the type of encryption of the PDF document
             EncryptionTypeResult encryptTypeResult = encryptClient.getPDFEncryption(inDoc);
 
             if (encryptTypeResult.getEncryptionType() == EncryptionType.PASSWORD)
                 System.out.println("The PDF document is protected with password-based encryption");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.POLICY_SERVER)
                 System.out.println("The PDF document is protected with policy");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.CERTIFICATE)
                 System.out.println("The PDF document is protected with certificate-based encryption");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.OTHER)
                 System.out.println("The PDF document is protected with another type of encryption");
             else if (encryptTypeResult.getEncryptionType() == EncryptionType.NONE)
                 System.out.println("The PDF document is not protected.");
         }catch (Exception e) {
                 e.printStackTrace();
         }
     }
 }
 
 
 
```
