---
title: Directory di archiviazione documenti globale
description: La directory GDS (Global Document Storage) è una directory utilizzata per memorizzare i file di lunga durata utilizzati all'interno di un processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 9a93b8f9-33cb-4aec-81e0-a1146bba955a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# Directory di archiviazione documenti globale{#global-document-storage-directory}

La directory *Global Document Storage (GDS)* è una directory utilizzata per memorizzare i file di lunga durata utilizzati in un processo. Questi file includono PDF, criteri e modelli di modulo. I file di lunga durata sono una parte fondamentale dello stato complessivo di molte distribuzioni di AEM Forms. Se alcuni o tutti i documenti di lunga durata vengono persi o danneggiati, il server Forms potrebbe diventare instabile. I documenti di input per le chiamate di processo asincrone sono memorizzati anche nella directory GDS e devono essere disponibili per elaborare le richieste. È importante considerare l&#39;affidabilità del file system che ospita la directory GDS. Utilizzare un array ridondante di dischi indipendenti (RAID) o un&#39;altra tecnologia appropriata per la qualità e il livello di servizio richiesti.

I file di lunga durata possono contenere informazioni utente riservate. Per accedere a queste informazioni potrebbero essere necessarie credenziali speciali utilizzando le API di AEM Forms o le interfacce utente. È importante che la directory GDS sia protetta correttamente tramite il sistema operativo. Solo l&#39;account amministratore utilizzato per eseguire il server applicazioni deve disporre dell&#39;accesso in lettura/scrittura alla directory GDS.

Oltre a selezionare una directory sicura e ad alta disponibilità per GDS, è possibile anche scegliere di abilitare l&#39;archiviazione dei documenti nel database. Si noti che anche se si utilizza il database di AEM Forms per l&#39;archiviazione dei documenti, AEM Forms richiede ancora la directory GDS. (Vedi [Opzioni di backup quando il database viene utilizzato per l&#39;archiviazione dei documenti](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

I dati dell&#39;applicazione AEM Forms risiedono nella directory GDS e nel database di AEM Forms. Nella tabella seguente vengono descritti i dati e le relative posizioni.

<table>
 <thead>
  <tr>
   <th><p>Dati dei moduli di AEM</p></th>
   <th><p>Database</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Dati dell’applicazione (utenti, ruoli, processi, criteri, endpoint, eventi e così via).</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Contenitori di servizi distribuiti</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Gestione documenti </p></td>
   <td><p>No</p></td>
   <td><p>Sì</p></td>
  </tr>
  <tr>
   <td><p>Archivio Forms</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Configurazione del sistema</p></td>
   <td><p>Sì</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Cartelle controllate</p></td>
   <td><p>No</p></td>
   <td><p>Sì</p></td>
  </tr>
 </tbody>
</table>

## Configurazione della directory GDS {#configuring-the-gds-directory}

La posizione della directory GDS può essere configurata manualmente durante il processo di installazione di AEM Forms. Se l&#39;impostazione relativa al percorso rimane vuota durante l&#39;installazione, per impostazione predefinita viene utilizzata una directory nell&#39;installazione del server applicazioni nel modo seguente:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Modificare la posizione GDS predefinita {#change-the-default-gds-location}

È possibile modificare la posizione di GDS nella console di amministrazione al termine dell&#39;installazione di AEM Forms. Riposiziona manualmente i dati per completare il processo.

>[!NOTE]
>
>* Esegui la migrazione dei dati nel modo seguente o si verifica una perdita di dati.
>* Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Accedi alla console di amministrazione e fai clic su Impostazioni > Impostazioni sistema core > Configurazioni.
1. Nella casella Directory Global Document Storage immettere il percorso completo della nuova directory GDS e quindi fare clic su OK.
1. Arrestare immediatamente il server applicazioni.
1. Spostare tutti i file dalla vecchia directory GDS nella nuova posizione, mantenendo la struttura della directory interna.
1. Riavviare il server applicazioni.

## Informazioni sui file di distribuzione {#about-deployment-files}

AEM Forms è costituito da due tipi di file di distribuzione, i contenitori del servizio e i file EAR di Java 2 Platform, Enterprise Edition (J2EE). I file EAR sono costituiti da bundle di applicazioni J2EE standard che contengono le funzionalità di base di AEM Forms. I file EAR specifici del server applicazioni sono i seguenti:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

L’implementazione di AEM Forms comporta la distribuzione dei file EAR assemblati e dei file di supporto nel server applicazioni in cui intendi eseguire la soluzione AEM Forms. Se hai configurato e assemblato più moduli, quelli distribuibili vengono assemblati all’interno dei file EAR distribuibili. Per distribuire questi file, copiarli nella directory *[appserver home]*\server\all\deploy.

I moduli e i file di archivio dei moduli di AEM sono inclusi in file JAR. Poiché non sono file di tipo J2EE, non vengono distribuiti nel server applicazioni. Vengono invece copiati nella directory GDS e un riferimento alla loro posizione viene memorizzato nel database di AEM Forms. Per questo motivo, la directory GDS deve essere condivisa tra tutti i nodi del cluster. Tutti i nodi devono avere accesso alla directory di archiviazione centrale per le DSC.

>[!NOTE]
>
>Prima di distribuire i contenitori di servizi, accertati di aver creato e configurato la directory GDS. (Vedere [Configurazione della directory GDS](global-document-storage-directory.md#configuring-the-gds-directory))
