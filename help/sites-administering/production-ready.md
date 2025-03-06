---
title: Esecuzione di AEM in modalità pronta per la produzione
description: Scopri come eseguire AEM in modalità pronta per la produzione.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 99724bd6-41b4-4491-9958-1f5d9e1f5050
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 4%

---

# Esecuzione di AEM in modalità pronta per la produzione{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe introduce la nuova modalità di esecuzione `"nosamplecontent"` volta ad automatizzare i passaggi necessari per preparare un&#39;istanza AEM per la distribuzione in un ambiente di produzione.

La nuova modalità di esecuzione non solo configurerà automaticamente l’istanza in modo da rispettare le best practice di sicurezza descritte nell’elenco di controllo della sicurezza, ma rimuoverà anche tutte le applicazioni e le configurazioni di Geometrixx di esempio nel processo.

>[!NOTE]
>
>Poiché, per motivi pratici, la modalità pronta per la produzione di AEM coprirà solo la maggior parte delle attività necessarie per proteggere un&#39;istanza, ti consigliamo vivamente di consultare l&#39;[elenco di controllo per la sicurezza](/help/sites-administering/security-checklist.md) prima di andare &quot;live&quot; con il tuo ambiente di produzione.
>
>Inoltre, tieni presente che l’esecuzione di AEM in modalità pronta per la produzione disabilita efficacemente l’accesso a CRXDE Lite. Se ne hai bisogno a scopo di debug, consulta [Abilitazione di CRXDE Lite in AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Per eseguire AEM in modalità pronta per la produzione, è sufficiente aggiungere `nosamplecontent` agli argomenti di avvio esistenti tramite l&#39;opzione di modalità di esecuzione `-r`:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Ad esempio, puoi utilizzare Production ready per avviare un’istanza di authoring con persistenza MongoDB simile alla seguente:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Modifica parte della modalità pronta per la produzione {#changes-part-of-the-production-ready-mode}

In particolare, quando AEM viene eseguito in modalità pronta per la produzione, vengono eseguite le seguenti modifiche di configurazione:

1. Il bundle di supporto **CRXDE** ( `com.adobe.granite.crxde-support`) è disabilitato per impostazione predefinita in modalità pronta per la produzione. Può essere installato in qualsiasi momento dall’archivio Maven pubblico di Adobe. La versione 3.0.0 è richiesta per AEM 6.1.

1. Il bundle **Apache Sling Simple WebDAV Access to repositories** ( `org.apache.sling.jcr.webdav`) sarà disponibile solo nelle istanze **author**.

1. Gli utenti appena creati devono modificare la password al primo accesso. Questo non si applica all’utente amministratore.
1. **Generate debug info** disabilitato per **Apache Sling JavaScript Handler**.

1. **Il contenuto mappato** e **Genera informazioni di debug** sono disabilitati per **Apache Sling JSP Script Handler**.

1. Il filtro WCM per CQ **Day** è impostato su `edit` per **author** e `disabled` per **publish** istanze.

1. **Adobe Granite HTML Library Manager** è configurato con le impostazioni seguenti:

   1. **Minimizza:** `enabled`
   1. **Debug:** `disabled`
   1. **Gzip:** `enabled`
   1. **Intervallo:** `disabled`

1. **Apache Sling GET Servlet** è impostato per supportare le configurazioni sicure per impostazione predefinita, come segue:

| **Configurazione** | **Autore** | **Pubblica** |
|---|---|---|
| Rendering TXT | disabilitato | disabilitato |
| Rappresentazione HTML | disabilitato | disabilitato |
| Rappresentazione JSON | abilitato | abilitato |
| Rappresentazione XML | disabilitato | disabilitato |
| json.maximumresults | 1000 | 100 |
| Indice automatico | disabilitato | disabilitato |
