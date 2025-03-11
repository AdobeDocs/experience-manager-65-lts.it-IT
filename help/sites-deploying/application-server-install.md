---
title: Installazione server applicazioni
description: Scopri come installare Adobe Experience Manager con un server applicazioni.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 09d54b52-485a-453c-a2d0-535adead9e6c
source-git-commit: d716571f490fe4bf3b7e58ea2ca85bbe6703ec0d
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Installazione server applicazioni{#application-server-install}

>[!NOTE]
>
>`JAR` e `WAR` sono i tipi di file in cui è rilasciato Adobe Experience Manager (AEM). Questi formati sono sottoposti a un controllo di qualità per soddisfare i livelli di supporto a cui Adobe si è impegnata.
>

Questa sezione spiega come installare Adobe Experience Manager (AEM) con un server applicazioni. Consulta la sezione [Piattaforme supportate](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) per informazioni sui livelli di supporto specifici forniti per i singoli server applicazioni.

Vengono descritti i passaggi di installazione dei seguenti Application Server:

* [WebSphere](#websphere)
* [Tomcat 11.0.x](#tomcat)

Per ulteriori informazioni sull&#39;installazione di applicazioni Web, sulle configurazioni del server e su come avviare e arrestare il server, consultare la documentazione del server applicazioni appropriato.

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## Descrizione generale {#general-description}

### Comportamento predefinito durante l’installazione di AEM in un server applicazioni {#default-behaviour-when-installing-aem-in-an-application-server}

AEM viene fornito come un singolo file .war da distribuire.

Se implementato, si verifica quanto segue per impostazione predefinita:

* la modalità di esecuzione è `author`
* l&#39;istanza (archivio, ambiente Felix OSGI, bundle e così via) è installata in `${user.dir}/crx-quickstart` dove `${user.dir}` è la directory di lavoro corrente, il percorso a crx-quickstart è denominato `sling.home`

* la radice del contesto è il nome del file .war, ad esempio `aem-65-lts`

#### Configurazione {#configuration}

È possibile modificare il comportamento predefinito nel modo seguente:

* modalità di esecuzione : configura il parametro `sling.run.modes` nel file `WEB-INF/web.xml` del file war di AEM prima della distribuzione

* sling.home: configura il parametro `sling.home` nel file `WEB-INF/web.xml` del file .war di AEM prima della distribuzione

* directory principale del contesto: rinominare il file war di AEM

#### Pubblica installazione {#publish-installation}

Per distribuire un’istanza Publish, devi impostare la modalità di esecuzione su Pubblica:

* Decomprimi il WEB-INF/web.xml dal file .war di AEM
* Cambia il parametro sling.run.modes in publish
* Ripristina il file web.xml nel file .war di AEM
* Distribuire il file .war di AEM

#### Controllo dell’installazione {#installation-check}

Per verificare se è installato tutto, è possibile:

* coda il file `error.log` per verificare che tutto il contenuto sia installato
* verifica in `/system/console` che tutti i bundle siano installati

#### Due istanze sullo stesso server applicazioni {#two-instances-on-the-same-application-server}

A scopo dimostrativo, può essere opportuno installare l’istanza di authoring e pubblicazione in un server applicazioni. Per eseguire questa operazione:

1. Modifica le variabili sling.home e sling.run.modes dell’istanza Publish.
1. Decomprimi il file WEB-INF/web.xml dal file .war di AEM.
1. Modifica il parametro sling.home in un percorso diverso (sono possibili percorsi assoluti e relativi).
1. Modifica sling.run.modes per pubblicare l’istanza Publish.
1. Ripristina il file web.xml.
1. Rinominare i file di guerra in modo che abbiano nomi diversi. Ad esempio, uno rinomina aemauthor.war e l’altro in aempublish.war.
1. Usa impostazioni di memoria superiori. Le istanze AEM predefinite, ad esempio, utilizzano `-Xmx3072m`
1. Distribuisci le due applicazioni web.
1. Dopo l’implementazione, arresta le due applicazioni web.
1. Sia nelle istanze di authoring che in quelle di pubblicazione, assicurati che nei file sling.properties la proprietà felix.service.urlhandlers=false sia impostata su false (per impostazione predefinita è impostata su true).
1. Avvia di nuovo le due applicazioni web.

## Procedure di installazione degli Application Server {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) riportata sopra.

**Preparazione server**

* Consenti alle intestazioni di autenticazione di base di passare:

   * Un modo per consentire ad AEM di autenticare un utente consiste nel disabilitare la sicurezza amministrativa globale del server WebSphere®. A tale scopo, passare a Sicurezza > Sicurezza globale e deselezionare la casella di controllo Abilita sicurezza amministrativa, salvare e riavviare il server.

* imposta `"JAVA_OPTS= -Xmx2048m"`
* Se desideri installare AEM utilizzando context root = /, modifica la directory principale di contesto dell’applicazione web predefinita esistente.

**Distribuisci applicazione Web AEM**

* Scarica il file .war di AEM
* Configurare le configurazioni in web.xml se necessario (vedi sopra nella Descrizione generale)

   * Decomprimi file WEB-INF/web.xml
   * cambiare il parametro sling.run.modes in publish
   * rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario
   * Ripristina file web.xml

* Distribuire il file .war di AEM

   * Scegli una directory principale di contesto (per impostare le modalità di esecuzione sling, seleziona i passaggi dettagliati della procedura guidata di distribuzione, quindi specificala al passaggio 6 della procedura guidata).

* Avviare l’applicazione web AEM

#### Tomcat 11.0.x {#tomcat}

Prima di una distribuzione, leggere la [Descrizione generale](#general-description) riportata sopra.

* **Prepara server Tomcat**

   * Aumentare le impostazioni della memoria VM:

      * In `bin/catalina.bat` (resp `catalina.sh` su UNIX®) aggiungere la seguente impostazione:
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat consente l&#39;accesso non amministratore o manager al momento dell&#39;installazione. Pertanto, è necessario modificare manualmente `tomcat-users.xml` per consentire l&#39;accesso a questi account:

      * Modificare `tomcat-users.xml` per includere l&#39;accesso per l&#39;amministratore e il manager. La configurazione deve essere simile al seguente esempio:

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * Se desideri distribuire AEM con la directory principale del contesto &quot;/&quot;, devi modificare la directory principale del contesto della Web app ROOT esistente:

      * Arresta e annulla la distribuzione di ROOT Web app
      * Rinomina cartella ROOT.war nella cartella webapps di tomcat
      * Avvia di nuovo l&#39;app Web

   * Se installi l’applicazione web AEM utilizzando l’interfaccia grafica di gestione, devi aumentare le dimensioni massime di un file caricato, poiché l’impostazione predefinita consente solo 50 MB di dimensioni di caricamento. Per aprire il file web.xml dell’applicazione web manager,

     `webapps/manager/WEB-INF/web.xml`

     e aumentare le dimensioni max-file-size e max-request-size ad almeno 500 MB, vedi il seguente esempio `multipart-config` di un file `web.xml` di questo tipo.

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **Distribuisci applicazione Web AEM**

   * Scarica il file .war di AEM.
   * Se necessario, effettua le configurazioni in web.xml (vedi sopra nella Descrizione generale).

      * Decomprimi il file WEB-INF/web.xml.
      * Modifica il parametro sling.run.modes in publish.
      * Rimuovi il commento dal parametro iniziale sling.home e imposta il percorso come necessario.
      * Ripristina il file web.xml.

   * Rinomina il file .war di AEM in ROOT.war se desideri distribuirlo come web app principale. Rinominalo in aemauthor.war se vuoi avere aemauthor come directory principale del contesto.
   * Copiatelo nella cartella Webapps di Tomcat.
   * Attendi che AEM sia installato.
