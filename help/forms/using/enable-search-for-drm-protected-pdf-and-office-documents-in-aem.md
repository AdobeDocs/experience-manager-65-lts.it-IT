---
title: Consentire ad AEM di effettuare ricerche nei documenti PDF e Microsoft Office protetti da Document Security
description: Scopri come abilitare la ricerca nativa di AEM per eseguire ricerche full-text sui documenti PDF protetti da DRM.
noindex: true
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 5e9d3f3c-8fc4-4d01-9f1e-62d3c29ab9e5
source-git-commit: cd6caaf9de907488db14df2a6396fa60efa2d42c
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Consentire ad AEM di effettuare ricerche nei documenti PDF e Microsoft Office protetti da Document Security{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager fornisce un’interfaccia utente per cercare e individuare varie risorse memorizzate in AEM. La ricerca nativa consente di cercare e individuare le risorse di AEM ed eseguire ricerche di testo in vari formati di documenti di uso comune, ad esempio file di testo normale, documenti di Microsoft Office e documenti di PDF. È inoltre possibile estendere e abilitare la ricerca nativa per eseguire ricerche full-text su documenti PDF e Microsoft Office protetti da DRM.

Per consentire ad AEM di effettuare ricerche nei documenti PDF e Microsoft Office protetti da Document Security, effettua le seguenti operazioni:

## Prima di iniziare {#before-you-start}

* Installa e configura AEM Forms Document Security.
* Aggiungere il pacchetto sun.util.calendar al inserisco nell&#39;elenco Consentiti di della configurazione del firewall di deserializzazione **.** La configurazione è elencata in `https://'[server]:[port]'/system/console/configMgr`.
* Assicurati che tutti i bundle di AEM siano attivi e funzionanti. I bundle sono elencati in `https://'[server]:[port]'/system/console/bundles`. Se non tutti i bundle sono attivi, attendi e controlla lo stato dei bundle dopo per alcuni minuti.

## Stabilire una connessione sicura all’interno del flusso di lavoro di AEM Forms (AEM Forms on JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Una connessione sicura consente un flusso ininterrotto di informazioni tra AEM Forms su JEE e i servizi OSGi in esecuzione sullo stesso server. Per stabilire una connessione sicura, utilizzare uno dei metodi seguenti:

* Configurare il bundle AEM Forms Client SDK con le credenziali di amministratore AEM Forms su JEE
* Configurare il bundle AEM Forms Client SDK utilizzando l’autenticazione reciproca

### Configurare il bundle AEM Forms Client SDK con le credenziali di amministratore AEM Forms su JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Apri Gestione configurazione di AEM e accedi come amministratore. L&#39;URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cerca e apri il bundle AEM Forms Client SDK. Specifica il valore per le seguenti proprietà:

   * **URL server:** Specifica l&#39;URL HTTP di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia il server AEM Forms su JEE con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms sul file keystore JEE>.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.
   * **Nome utente:** Specifica il nome utente dell&#39;account AEM Forms su JEE da utilizzare per avviare chiamate da AEM Forms sul server JEE. L’account specificato deve disporre delle autorizzazioni per richiamare Document Services sul server AEM Forms su JEE.
   * **Password**: specifica la password dell&#39;account AEM Forms su JEE indicato nel campo Nome utente.

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti protetti da PDF e Microsoft Office.

### Configurare il bundle AEM Forms Client SDK utilizzando l’autenticazione reciproca {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Abilita l’autenticazione reciproca per AEM Forms su JEE.
1. Apri Gestione configurazione di AEM e accedi come amministratore. L&#39;URL predefinito è https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Cerca e apri il bundle AEM Forms Client SDK. Specifica il valore per le seguenti proprietà:

   * **URL server:** Specifica l&#39;URL HTTPS di AEM Forms sul server JEE. Per abilitare la comunicazione su https, riavvia il server AEM Forms su JEE con il parametro -Djavax.net.ssl.trustStore=&lt;percorso di AEM Forms sul file keystore JEE>.
   * **Abilita SSL bidirezionale**: abilita l&#39;opzione Abilita SSL bidirezionale.
   * **URL file registro chiavi**: specificare l&#39;URL del file registro chiavi.
   * **URL file TrustStore**: specificare l&#39;URL del file truststore.
   * **Password registro chiavi**: specificare la password per il file registro chiavi.
   * **TrustStorePassword**: specificare la password per il file truststore.
   * **Nome servizio**: aggiungere RightsManagementService all&#39;elenco dei servizi specificati.

   Fai clic su **Salva**. AEM è abilitato per la ricerca di documenti PDF e Microsoft Office protetti da Document Security

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

## Indicizzare un esempio di documento PDF o Microsoft Office protetto tramite policy {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Accedi ad AEM Assets come amministratore.
1. Crea una cartella in AEM Digital Asset Manager e carica un documento PDF o Microsoft Office protetto tramite policy nella cartella appena creata. Ora è possibile cercare il contenuto dei documenti protetti tramite policy utilizzando la funzione di ricerca di AEM. Deve restituire il documento contenente il testo cercato.
