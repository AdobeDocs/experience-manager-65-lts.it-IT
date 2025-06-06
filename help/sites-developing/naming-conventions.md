---
title: Convenzioni di denominazione dei nodi nel Java Content Repository
description: I nodi nell’archivio sono soggetti alle convenzioni di denominazione dell’archivio dei contenuti Java
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 36025dac-890e-45ba-adea-a230a5231a0b
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Convenzioni di denominazione {#naming-conventions}

I nodi dell&#39;archivio sono soggetti alle convenzioni di denominazione dell&#39;[archivio dei contenuti Java](/help/sites-developing/the-basics.md#java-content-repository). Tuttavia, AEM impone ulteriori convenzioni per il nome dei nodi della pagina.

## Convenzioni di denominazione delle pagine {#naming-conventions-for-pages}

Queste convenzioni di denominazione vengono implementate a vari livelli:

* JcrUtil: implementazione AEM delle [utilità JCR](#jcr-utilities).
* PageManager: [Page Manager](#page-manager) fornisce metodi per le operazioni a livello di pagina.
* In base all’interfaccia utente in uso:

   * [Interfaccia utente touch standard](#standard-ui)
   * [Interfaccia classica](#classic-ui)

### Utilità JCR {#jcr-utilities}

[JcrUtil](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) è l&#39;implementazione AEM delle utilità JCR. Di particolare interesse per la convalida dei nomi sono le mappature di caratteri che controlla e le convalide seguenti:

* `isValidName`

   * Controlla se il nome non è vuoto e contiene solo caratteri validi.
   * Può essere utilizzato per verificare se un nome proposto è valido.

* `createValidName`

   * In questo modo viene creata un&#39;etichetta valida da una stringa arbitraria.
   * Può essere utilizzato per creare un nome da un titolo.

### Gestione pagine {#page-manager}

[PageManager](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html) fornisce metodi per le operazioni a livello di pagina, basati su [JCRUtil](#jcr-utilities).

### Interfaccia standard {#standard-ui}

L’interfaccia utente standard touch:

* Convalida il nome in base alle restrizioni imposte da PageManager quando:

   * viene fornito il titolo della pagina da convertire nel nome del nodo
   * viene fornito un nome di nodo esplicito

### Interfaccia classica {#classic-ui}

L’interfaccia utente classica impone restrizioni più severe:

* Convalida il nome quando un nome di nodo esplicito:

   * viene fornito il titolo della pagina da convertire nel nome del nodo
   * viene fornito un nome di nodo esplicito

* Caratteri validi (solo questi caratteri sono effettivamente validi quando una pagina viene creata dall&#39;interfaccia utente classica, anche se `PageManagerImpl` consentirebbe caratteri aggiuntivi):

   * Da &#39;a&#39; a &#39;z&#39;
   * Da &#39;A&#39; a &#39;Z&#39;
   * Da &#39;0&#39; a &#39;9&#39;
   * _ (trattino basso)
   * `-` (trattino/segno meno)
