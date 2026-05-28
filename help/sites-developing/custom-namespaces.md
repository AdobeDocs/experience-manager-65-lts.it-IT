---
title: Spazi dei nomi personalizzati
description: Scopri come definire e distribuire spazi dei nomi personalizzati in AEM 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 475a77e8e4ff0ecd19a939fd3b3c9294adf24997
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 8%

---


# Spazi dei nomi personalizzati{#custom-namespaces}

Scopri come definire e distribuire [spazi dei nomi](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/4.5_Namespaces.html?lang=it) personalizzati in AEM 6.5 LTS.

Gli spazi dei nomi personalizzati sono parte facoltativa di una proprietà JCR prima di un `:`. AEM utilizza diversi spazi dei nomi, ad esempio:

+ `jcr` per le proprietà di sistema JCR
+ `cq` per le proprietà AEM (precedentemente note come Adobe CQ)
+ `dam` per le proprietà AEM specifiche delle risorse DAM
+ `dc` per le proprietà Dublin Core

... e molti altri.

Gli spazi dei nomi possono essere utilizzati per indicare l’ambito e l’intento di una proprietà. La creazione di uno spazio dei nomi personalizzato, spesso il nome dell’azienda, consente di identificare chiaramente nodi o proprietà specifici per l’implementazione di AEM e contengono dati specifici per la tua azienda.

Gli spazi dei nomi personalizzati vengono gestiti negli script [Sling Repository Initialization (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html) e distribuiti come configurazioni OSGi nel pacchetto di configurazione del progetto (ad esempio, `ui.config`).

## Risorse {#resources}

+ [Documentazione sull’inizializzazione dell’archivio Sling (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## Codice {#code}

Il codice seguente viene utilizzato per configurare uno spazio dei nomi `wknd`.

### Configurazione OSGi RepositoryInitializer

`/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~wknd-examples-namespaces.cfg.json`

```json
{
    "scripts": [
        "register namespace (wknd) https://site.wknd/1.0"
    ]
}
```

Questo consente di utilizzare in AEM le proprietà personalizzate che utilizzano lo spazio dei nomi `wknd`, come indicato dal primo parametro dopo l&#39;istruzione `register namespace`. Per definizioni di script più avanzate, vedere gli esempi nella [documentazione relativa all&#39;inizializzazione dell&#39;archivio Sling (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios).
