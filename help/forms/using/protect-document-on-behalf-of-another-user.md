---
title: Proteggere un documento per conto di un altro utente
description: Scopri come AEM Forms Document Security Java&trade; SDK offre API per un account utente per proteggere un documento per conto di un altro utente.
geptopics: SG_AEMFORMS/categories/working_with_document_security
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 56280931-c88b-46ea-bee6-f5a5494d715a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Proteggere un documento per conto di un altro utente {#protect-a-document-on-behalf-of-another-user}

AEM Forms Document Security Java™ SDK fornisce API per consentire a un account utente di proteggere un documento per conto di un altro utente senza dover ottenere le autorizzazioni necessarie per modificarlo. È possibile utilizzare le API in un processo di flusso di lavoro o a livello di programmazione come servizio documenti. Le nuove API sono:

* **protectDocumentUse** l&#39;API ProtectDocument che consente di applicare un criterio a un documento per conto di

  un altro account utente. Le autorizzazioni dell’account utente utilizzato per applicare la policy rimangono limitate alla protezione del documento. Non è possibile aprire e visualizzare il documento. RMSecureDocumentResult protectDocument(Document inDoc, String documentName, String policySetName, String policyName, RMLocale locale, boolean bExactMatchForNames)

* **createLicenseUse** l&#39;API CreateLicense che consente di creare una licenza per un criterio per conto di un altro account utente. PublishLicenseDTO createLicense(String policyId, String documentName, booleano logSecureDocEvent)
* **protectDocumentWithCoverPageUse** l&#39;API ProtectDocumentWithCoverPage per consentire l&#39;applicazione di una policy e l&#39;aggiunta di una pagina di copertina a un documento per conto di un altro utente. Le autorizzazioni dell’account utente utilizzato per applicare la policy rimangono limitate alla protezione del documento. Non è possibile aprire e visualizzare il documento. RMSecureDocumentResult protectDocumentWithCoverPage(Document inDoc, String documentName, String policySetName, String policyName, Document coverDoc, booleano bExactMatchForNames)

## Utilizzo delle API per proteggere un documento per conto di un altro utente {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

Eseguire le operazioni seguenti per proteggere un documento per conto di un altro utente e senza disporre delle autorizzazioni necessarie per modificarlo:

1. Crea un set di criteri. Ad esempio, PolicySet1.
1. Crea un criterio nel set di criteri appena creato. Ad esempio, Policy1 in PolicySet1.
1. Crea un utente con il ruolo Utente finale di Rights Management. Ad esempio, Utente1. Fornire le autorizzazioni per visualizzare i documenti protetti tramite Policy1 all&#39;utente appena creato.
1. Crea un ruolo. Ad esempio, Ruolo1. Fornisci l’autorizzazione Richiesta servizio al ruolo appena creato. Crea un utente con il ruolo appena creato. Ad esempio, Utente2. È possibile utilizzare User2 o un amministratore per creare una connessione SDK e richiamare il servizio protectDocument.

   Ora è possibile eseguire il codice di esempio seguente per proteggere un documento senza fornire le autorizzazioni per la modifica del documento all&#39;utente che lo protegge:

   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.Properties;
   
   import com.adobe.edc.common.dto.PublishLicenseDTO;
   import com.adobe.edc.sdk.SDKException;
   import com.adobe.idp.Document;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
   import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
   import com.adobe.livecycle.rightsmanagement.client.DocumentManager;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient2;
   
   public class PublishAsProtectAPI {
   
   private static final String unprotectedFileName = "C:\\unprotected.pdf";
   private static final String protectedFileName = "C:\\protect.pdf";
   private static final String coverFileName = "C:\\CoverPage.pdf";
   private static final String POLICY_ID = "2EF66008-5E2D-1034-9B06-00000A292C18"; 
   
   public static void main(String[] args) {
   
   try {
   
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,"http://localhost:8080");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,"password");
   
   // Create a ServiceClientFactory instance
   ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
   testProtectDocument(factory);
   testProtectDocumentWithCoverPage(factory);
   testProtectDocumentJavaPPL(factory);
   
   } 
   catch (Exception ex) {
   ex.printStackTrace(); }
   }
   
   private static void testProtectDocument(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocument(inPDF, "test", "newPolicySet", "latest", "DefaultDom", "administrator", null, true);
   System.out.println("Total Time taken for protectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static void testProtectDocumentWithCoverPage(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   FileInputStream coverIS = new FileInputStream(coverFileName);
   Document inCoverPDF = new Document(coverIS);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocumentWithCoverPage(inPDF, "test", "newPolicySet", "latestPolicy", inCoverPDF, true);
   System.out.println("Total Time taken for Page0ProtectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static PublishLicenseDTO testProtectDocumentJavaPPL (ServiceClientFactory factory) throws SDKException, FileNotFoundException, IOException {
   // Create a RightsManagementClient object
   RightsManagementClient2 rmClient2 = new RightsManagementClient2(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient2.getDocumentManager();
   long startTime = System.currentTimeMillis();
   PublishLicenseDTO license = documentManager.createLicense(POLICY_ID, "Out.pdf", true);
   System.out.println("Create License totalTime = " + (System.currentTimeMillis() - startTime));
   startTime = System.currentTimeMillis();
   // Reference a PDF document to which a policy is applied
   InputStream inputFileStream = new FileInputStream(unprotectedFileName);
   // Apply a policy to the PDF document
   InputStream protectPDF = rmClient2.getRightsManagementEncryptionService().protectDocument(inputFileStream, license);
   // Save the policy-protected PDF document
   File myFile = new File(protectedFileName);
   // write the inputStream to a FileOutputStream
   FileOutputStream outputStream = new FileOutputStream(myFile);
   int read = 0;
   byte[] bytes = new byte[1024];
   while ((read = protectPDF.read(bytes)) != -1) {
   outputStream.write(bytes, 0, read);
   }
   System.out.println("protectPDFDocument totalTime = " + (System.currentTimeMillis() - startTime));
   outputStream.close();
   inputFileStream.close();
   System.out.println("Document Protected Successfully");
   return license;
   }
   }
   ```
