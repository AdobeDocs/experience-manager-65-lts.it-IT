---
title: Spazi dei nomi personalizzati
description: Scopri come definire e distribuire spazi dei nomi personalizzati in AEM 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
subfeature_v2:
  - id: cd14456d-a492-4b5c-8a82-1fbd4460dbd2
    internal-label: Java Content Repository
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
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
