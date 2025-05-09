---
title: Aggiornamento del Forms di ricerca personalizzato
description: Questo articolo descrive le modifiche necessarie dopo un aggiornamento per il funzionamento dei moduli di ricerca personalizzati.
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: 9df608f8-cdd0-4820-aab1-eab9fd70f961
source-git-commit: 547d7866346fb148cb66f546d8a2e1141f69f563
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# Aggiornamento del Forms di ricerca personalizzato{#upgrading-custom-search-forms}

In AEM 6.2, la posizione in cui sono memorizzati i Forms di ricerca personalizzati nell’archivio è cambiata. Dopo l&#39;upgrade, vengono spostati dalla loro posizione in 6.1 in:

* /apps/cq/gui/content/facets

in una nuova posizione in:

* /conf/global/settings/cq/search/facets

Per questo motivo, sono necessarie regolazioni manuali dopo un aggiornamento affinché i moduli continuino a funzionare.

Questo vale per il nuovo Search Forms e il Forms predefinito che sono stati personalizzati.

Per ulteriori informazioni, consulta la documentazione su [Facet di ricerca](/help/assets/search-facets.md).

## Modifica della proprietà resourceType {#changing-the-resourcetype-property}

Se non specificato diversamente, la maggior parte delle regolazioni da eseguire dopo l&#39;aggiornamento richiede la modifica della proprietà `sling:resourceType` per il Forms di ricerca personalizzato configurato. Ciò è necessario affinché la proprietà punti alla posizione corretta dello script di rendering.

È possibile modificare la proprietà eseguendo le operazioni seguenti:

1. Apri CRXDE Lite da `https://server:port/crx/de/index.jsp`
1. Individuare il percorso del nodo da regolare, come specificato nell&#39;Elenco di [Forms di ricerca personalizzato](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) di seguito.
1. Fai clic sul nodo. Nel riquadro delle proprietà di destra, fare clic e modificare la proprietà **sling:resourceType**.
1. Infine, salvare le modifiche premendo il pulsante **Salva tutto**.

## Elenco di Forms di ricerca personalizzati {#list-of-custom-search-forms}

Di seguito è riportato un elenco di tutti i Forms di ricerca personalizzati e delle modifiche necessarie dopo l’aggiornamento. Si riferiscono ai nomi in `/conf/global/settings/cq/search/facets/sites/items`.

### Predicato full-text con nome nodo &quot;full-text&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1</td>
   <td>full-text</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

In AEM 6.1, il predicato full-text standard faceva parte del modulo di ricerca. Nella versione 6.2, il campo full-text è stato sostituito da OmniSearch. Questo predicato viene ignorato a livello di programmazione e può essere rimosso.

**Azione:** Rimuovere completamente il nodo.

### Altri predicati full-text {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nella ricerca predefinita Da in 6.1</td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicati browser percorsi {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>percorso</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicati tag {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>tag</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà **resourceType** (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicato di stato pagina {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

Lo stato della pagina è stato sostituito da due predicati di proprietà Options, uno per lo stato di pubblicazione e uno per lo stato di LiveCopy.

**Azioni:**

* Rimuovi il nodo `pagestatuspredicate`
* Copia nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * a `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copia nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * a `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Assicurarsi di impostare la proprietà `listOrder` per il nodo `analyticspredicate` su &quot;**8**&quot;. Ciò è necessario per evitare conflitti.

### Predicati intervallo di date {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Filtro nascosto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Nessun elemento da modificare.

### Predicato di analisi {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicato intervallo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/range predicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

>[!NOTE]
>
>Nota: a differenza della versione 6.1, il predicato Range non esegue più il rendering di un tag nella barra di ricerca.

### Predicato proprietà opzioni {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicato intervallo del cursore {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicato componenti {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicato autore {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicato modelli {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

## Barra di ricerca amministrazione risorse {#assets-admin-search-rail}

I nodi seguenti fanno riferimento ai nomi in `/conf/global/settings/dam/search/facets/assets/items`

### Predicato full-text con nome nodo &quot;full-text&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | full-text |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| Tipo di risorsa in 6.2 | n/d |

Nella versione 6.1, il predicato full-text standard faceva parte del modulo di ricerca. Nella versione 6.2, il campo full-text è stato sostituito da OmniSearch. Questo predicato viene ignorato a livello di programmazione e può essere rimosso.

**Azione:** Rimuovere il nodo sopra indicato.

### Predicati browser percorsi {#path-browser-predicates-1}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | pathbrowser |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicati tipo MIME {#mime-type-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | mimetype |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra).

### Predicati dimensione file {#file-size-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | filesize |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Azione:** Regola `resourceType` come mostrato nella posizione 6.2 precedente.

### Predicati ultima modifica risorsa {#asset-last-modified-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

Azione: regola la proprietà resourceType (aggiungi &quot;/coral&quot; come nella posizione 6.2 indicata sopra).

### Predicato pubblicazione {#publish-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | pubblicazione |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**Azioni:**

* Regola la proprietà `resourceType` (aggiungi &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

* Aggiungi una proprietà `optionPaths` (di tipo String) con il valore: `/libs/dam/options/predicates/publish`

* Aggiungi la proprietà `singleSelect` con valore booleano `true`.

### Predicati di stato {#status-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stato |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

### Predicati di stato scadenza {#expiry-status-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | expirystatus |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

### Predicati di validità dei metadati {#metadata-validity-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | metadati |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

### Predicati di valutazione {#rating-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | valutazione |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

### Predicato orientamento {#orientation-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | orientation |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo di risorsa in 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Azioni:**

* Regola la proprietà `resourceType` (aggiungi &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

* Aggiungere una proprietà `fieldLabel` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungere una proprietà `emptyText` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungere una proprietà `rootPath` con lo stesso valore della proprietà `optionPaths` sullo stesso nodo.

### Predicato stile {#style-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stile |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo di risorsa in 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Azioni:**

* Regola la proprietà `resourceType` (aggiungi &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

* Aggiungere una proprietà `fieldLabel` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungere una proprietà `emptyText` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungere una proprietà `rootPath` con lo stesso valore della proprietà `optionPaths` sullo stesso nodo.

### Predicati formato video {#video-format-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | videoFormat |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)

### Predicato risorse principale {#mainasset-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | risorsa principale |
|---|---|
| Tipo di risorsa in 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo di risorsa in 6.2 | granite/ui/components/coral/foundation/form/hidden |

**Azione:** Regolare la proprietà `resourceType` (aggiungere &quot;**/coral**&quot; come nel percorso 6.2 indicato sopra)
