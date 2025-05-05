---
title: Consentire ad AEM di effettuare ricerche nei documenti PDF protetti da Document Security
description: Scopri come abilitare la ricerca nativa di AEM per eseguire ricerche full-text sui documenti PDF protetti da DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: ad86398d-0dc9-4168-b409-4d231b8d586b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Consentire ad AEM di effettuare ricerche nei documenti PDF protetti da Document Security{#enable-aem-to-search-document-security-protected-pdf-documents}

La funzione di ricerca di AEM consente di cercare e individuare le risorse di AEM ed eseguire ricerche testuali in vari formati di documenti di uso comune, ad esempio file di testo normale, documenti di Microsoft Office e documenti di PDF. È inoltre possibile estendere la ricerca nativa per eseguire ricerche full-text su [documenti PDF protetti con AEM Document Security](../../forms/using/admin-help/document-security.md). Per consentire ad AEM di eseguire ricerche full-text su tali documenti, effettua le seguenti operazioni:

1. Stabilire una connessione sicura
1. Indicizzare un esempio di documento PDF protetto tramite policy

## Prerequisiti {#prerequisites}

* Se utilizzi AEM Forms su OSGi:

   * Installa il pacchetto [Indicizzatore di Document Security di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) nel server AEM Forms.

   * Assicurati che un AEM Forms sul server JEE sia in esecuzione e che la sicurezza dei documenti sia installata nel corrispondente AEM Forms sul server JEE. Per indicizzare il documento protetto è necessario AEM Form sul server JEE.

* Se utilizzi solo AEM Forms sul server JEE, il pacchetto di indicizzazione è già installato.
* Assicurati che tutti i bundle siano attivi e funzionanti. Se non tutti i bundle sono attivi, attendi che tutti i bundle siano attivi.

   * Per AEM Forms su OSGi, i bundle sono elencati in https://&#39;[server]:[porta]&#39;/system/console/bundles.
   * Per AEM Forms su JEE, i bundle sono elencati in https://&#39;[server]:[porta]&#39;/[percorso-contesto]/sistema/console/bundle. Ad esempio, https://localhost:8080/lc/system/console/bundles.

* Aggiungere il pacchetto *sun.util.calendar* al inserisco nell&#39;elenco Consentiti di. Per aggiungere il pacchetto al inserisco nell&#39;elenco Consentiti di, attenersi alla procedura descritta di seguito.

   1. Apri AEM Web Console. URL: https://&#39;[server]:[porta]&#39;/system/console/configMgr.
   1. Individuare e aprire **Configurazione firewall deserializzazione**.

   1. Aggiungere il pacchetto sun.util.calendar al campo delle classi o dei prefissi del pacchetto Inseriti nell&#39;elenco Consentiti e fare clic su **Salva**.

### Stabilire una connessione sicura tra gli stack AEM Forms JEE e OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Per stabilire la connessione sicura, è possibile utilizzare uno dei metodi seguenti:

* Configurare il bundle Adobe LiveCycle Client SDK con le credenziali di amministratore AEM Forms su JEE
* Configurare il bundle Adobe LiveCycle Client SDK utilizzando l&#39;autenticazione reciproca

#### Configurare il bundle Adobe LiveCycle Client SDK con le credenziali di amministratore AEM Forms su JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri AEM Web Console. URL: https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individua e apri il **pacchetto SDK client Adobe LiveCycle**. Specifica il valore per i campi seguenti:

   * **URL server:** Specifica l&#39;URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia il server con il parametro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** Specifica il nome utente dell&#39;account AEM Forms su JEE da utilizzare per avviare chiamate dal server AEM. L’account specificato deve disporre delle autorizzazioni necessarie per avviare i servizi documentali sul server AEM Forms su JEE.
   * **Password**: specifica la password dell&#39;account AEM Forms su JEE indicato nel campo Nome utente.

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti da Document Security.

#### Configurare il bundle Adobe LiveCycle Client SDK utilizzando l&#39;autenticazione reciproca {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Abilita l’autenticazione reciproca per AEM Forms su JEE. Per informazioni dettagliate, vedere [CAC e autenticazione reciproca](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Apri AEM Web Console. URL: https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Individua e apri il bundle **Adobe LiveCycle Client SDK**. Specifica il valore per le seguenti proprietà:

   * **URL server**: specifica l&#39;URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia il server AEM con il parametro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Abilita SSL bidirezionale**: abilita l&#39;opzione Abilita SSL bidirezionale.
   * **URL file registro chiavi**: specificare l&#39;URL del file registro chiavi.
   * **URL file TrustStore**: specificare l&#39;URL del file truststore.
   * **Password registro chiavi**: specificare la password per il file registro chiavi.
   * **TrustStorePassword**: specificare la password per il file truststore.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF protetti da Document Security

### Indicizzare un esempio di documento PDF protetto tramite policy {#index-a-sample-policy-protected-pdf-document}

1. Accedi ad AEM Assets come amministratore.
1. Crea una cartella in AEM Digital Asset Manager e carica i documenti PDF protetti tramite policy nella cartella appena creata.

   Ora è possibile eseguire ricerche nei documenti protetti tramite policy utilizzando la funzione di ricerca di AEM.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.
