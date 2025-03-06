---
title: Editor
description: Scopri come tornare all’Editor dell’interfaccia classica.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 54a97ac0-db9e-4903-b395-b1af87cfd151
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---

# Editor{#editor}

Per impostazione predefinita, la possibilità di passare all’interfaccia classica dall’editor è stata disattivata.

Per riattivare l&#39;opzione **Apri nell&#39;interfaccia classica** nel menu **Informazioni pagina**, eseguire la procedura seguente.

1. Utilizzando CRXDE Lite, individua il seguente nodo:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Ad esempio

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Crea una sovrapposizione utilizzando l&#39;opzione **Sovrapponi nodo**, ad esempio:

   * **Percorso**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Posizione sovrapposizione**: `/apps/`
   * **Corrispondenza tipi di nodo**: attivo (selezionare la casella di controllo)

1. Aggiungi la seguente proprietà di testo con più valori al nodo sovrapposto:

   `sling:hideProperties = ["granite:hidden"]`

1. L&#39;opzione **Apri nell&#39;interfaccia classica** è nuovamente disponibile nel menu **Informazioni pagina** durante la modifica delle pagine.

   ![apri nell&#39;interfaccia classica, opzione da informazioni pagina](assets/syui-03-2019-02-27-15-19-48.png)
