---
title: Sviluppare AEM Commerce
description: Scopri come generare un progetto AEM abilitato per il commerce utilizzando l’archetipo di progetto AEM. Scopri come generare e distribuire il progetto in un ambiente di sviluppo locale.
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
solution: Experience Manager,Commerce
role: Admin, Developer
exl-id: 22fcdadf-12c0-4545-a854-76345806386f
source-git-commit: 5995dda0aac101e6c0d506ac5bba786674b0735b
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 18%

---

# Sviluppare AEM Commerce {#develop}

Lo sviluppo di progetti AEM Commerce basati su Commerce integration framework (CIF) per AEM segue le stesse regole e best practice di altri progetti AEM. Rivedi prima quanto segue:

- [Guida utente allo sviluppo in AEM](/help/sites-developing/getting-started.md)
- [Concetti di base di AEM](/help/sites-developing/the-basics.md)
- [Sviluppo AEM - Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)

## Sviluppo locale per AEM Commerce {#local}

Si consiglia di utilizzare un ambiente di sviluppo locale con i progetti CIF.

>[!NOTE]
>
>Le istruzioni seguenti sono utili per configurare un ambiente di sviluppo AEM locale per AEM Commerce utilizzando CIF (con particolare attenzione per AEM 6.5 LTS). Se utilizzi AEM as a Cloud Service, consulta la documentazione di [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/content-and-commerce/introduction#).

Il componente aggiuntivo AEM Commerce per AEM, noto come componente aggiuntivo CIF, è disponibile anche per lo sviluppo locale e fornito come pacchetto AEM. Può essere scaricato dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html) come feature pack.

### Software richiesto

È necessario installare localmente quanto segue:

- AEM 6.5 LTS locale
- [Java 17/Java 21](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o versione successiva)
- [Nodo LTS](https://nodejs.org/it/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accesso al componente aggiuntivo CIF

Il componente aggiuntivo CIF può essere scaricato dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html), cercare `AEM Commerce add-on`.

>[!TIP]
>
>Assicurati di utilizzare sempre la versione più recente del componente aggiuntivo CIF.

### Configurazione locale

Per lo sviluppo di progetti CIF locali utilizzando AEM e il componente aggiuntivo CIF, effettuare le seguenti operazioni:

1. Decomprimi il file AEM.jar per creare la cartella `crx-quickstart` ed esegui:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crea una cartella `crx-quickstart/install`.

1. Copiare il pacchetto del componente aggiuntivo CIF scaricato dal portale di distribuzione software nella cartella `crx-quickstart/install`.

>[!TIP]
>
>In alternativa, installa il pacchetto del componente aggiuntivo CIF utilizzando Gestione pacchetti.

1. Avvia quickstart di AEM

Verificare la configurazione tramite la console OSGI: `http://localhost:4502/system/console/osgi-installer`. L’elenco deve includere i bundle relativi al componente aggiuntivo CIF, il pacchetto di contenuti e le configurazioni OSGI. Assicurati che tutti i bundle siano avviati.

## Configurazione del progetto {#project}

Esistono due modi per avviare il progetto AEM Commerce utilizzando CIF.

### Usare AEM Project Archetype

Il [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) è lo strumento principale per Bootstrap un progetto preconfigurato per iniziare a utilizzare CIF. I Componenti core CIF e tutte le configurazioni richieste possono essere inclusi in un progetto generato con un’opzione aggiuntiva.

>[!TIP]
>
>Usa [AEM Project Archetype 25 o versioni successive](https://github.com/adobe/aem-project-archetype/releases) per generare il progetto.

Consulta le [istruzioni d’uso](https://github.com/adobe/aem-project-archetype#usage) di AEM Project Archetype per la generazione di un progetto AEM. Per includere CIF nel progetto, utilizzare l&#39;opzione `includeCommerce`.

Ad esempio:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

Puoi utilizzare i Componenti core di CIF in qualsiasi progetto. Includi il pacchetto `all` fornito oppure utilizza il pacchetto di contenuti CIF e i bundle OSGi correlati singolarmente. Aggiungere manualmente componenti core CIF a un progetto utilizzando le dipendenze seguenti:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Utilizza AEM Venia reference store

Una seconda opzione per avviare un progetto CIF è clonare e utilizzare [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store è un esempio di applicazione di vetrina di riferimento che illustra l’utilizzo dei componenti core CIF di AEM. Si tratta di un insieme di esempi di best practice e di un potenziale punto di partenza per sviluppare le tue funzionalità.

Inizia a usare Venia Reference Store clonando l&#39;[archivio Git](https://github.com/adobe/aem-cif-guides-venia) e inizia a personalizzare il progetto in base alle tue esigenze.

>[!NOTE]
>
>Il progetto Venia Reference Store contiene due profili di build per AEM as a Cloud Service e AEM 6.5. Controlla il [file readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) del progetto per vedere come vengono utilizzati. Per AEM 6.5 utilizzare il profilo `classic`.

### Collegare AEM al sistema Commerce

Per collegare il progetto al sistema commerce, AEM deve essere configurato con l’endpoint GraphQL del sistema commerce.

Entrambi, un progetto generato da [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) o [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia), include già una configurazione predefinita che deve essere regolata.

Sostituire il valore di `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con l&#39;endpoint GraphQL del sistema commerce utilizzato dal progetto.

Il componente aggiuntivo AEM Commerce e i componenti core CIF si connettono all’endpoint Commerce GraphQL tramite il server AEM. Oppure direttamente dal browser. Per impostazione predefinita, i componenti core CIF lato client e gli strumenti di creazione dei componenti aggiuntivi CIF si connettono a `/api/graphql`. Se necessario, è possibile regolarlo tramite la configurazione di CIF Cloud Service (vedi sotto).

Il componente aggiuntivo CIF fornisce un servlet proxy GraphQL in `/api/graphql`. Se non prevedi di utilizzare un Dispatcher AEM locale, è consigliabile configurare anche il servlet proxy di GraphQL.

Passare a http://localhost:4502/system/console/configMgr e creare una configurazione OSGI per il servizio `Adobe CIF GraphQL Proxy Configuration`. Utilizza lo stesso endpoint GraphQL del sistema commerce utilizzato per il client GraphQL di cui sopra.

## Risorse aggiuntive

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
