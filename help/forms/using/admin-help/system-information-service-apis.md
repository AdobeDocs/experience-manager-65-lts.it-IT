---
title: API del servizio informativo del sistema
description: Questo documento fornisce informazioni dettagliate sulle API fornite dal servizio informativo del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 93124f35-0323-4f51-9167-9bfcadc819e2
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 100%

---

# API del servizio informativo del sistema {#system-information-service-apis}

Il servizio informativo del sistema fornisce un set di API REST per recuperare le informazioni. La tabella seguente fornisce informazioni dettagliate sulle API:

<table>
 <thead>
  <tr>
   <th><p>Nome</p></th>
   <th><p>URL</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://‘[server]:[port]’/rest/services/SystemInfo.properties’</p></td>
   <td><p>Questa API è un wrapper per l’API Java <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a>. Recupera la configurazione dell’ambiente di lavoro corrente. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera tutte le variabili di ambiente del sistema operativo host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Scarica un file zip contenente i registri del server applicazioni. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera tutto il contenuto del file config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera lo stato e i parametri di configurazione dei servizi AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.italDetails</p></td>
   <td><p>Recupera il tempo di operatività del server, gli argomenti JVM, la memoria di sistema, la dimensione heap, il nome del sistema operativo, il numero di thread attivi e il conteggio di thread. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Recupera i valori delle seguenti proprietà:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Recupera informazioni dettagliate sul database.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Recupera le informazioni sulla versione e sulla licenza dei componenti AEM Forms installati. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Scarica i file di configurazione del server applicazioni host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera il conteggio e la traccia dello stack dei thread attivi. Accetta i seguenti parametri:</p>
    <ul>
     <li><p>iterations= [n]: specifica il numero di iterazioni. Sostituisci n con un numero. </p></li>
     <li><p>Delay= [n]: specifica il numero di millisecondi di attesa prima di avviare l’iterazione successiva. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Questa API è un wrapper per tutte le API del servizio di informazioni di sistema. Internamente, esegue tutte le API di informazioni di sistema e scarica le informazioni in formato zip. </p><p><i><strong>nota</strong>: SystemInfo.info non fornisce il conteggio e la traccia dello stack dei thread attivi. </i></p></td>
  </tr>
 </tbody>
</table>
