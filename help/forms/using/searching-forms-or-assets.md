---
title: Ricerca di moduli e risorse
description: Puoi cercare moduli e risorse nella tua istanza di AEM utilizzando la funzione di ricerca di AEM. La ricerca di base e avanzata consente di individuare rapidamente le risorse.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 1e3c4724-9dbd-4e39-a0fc-efe7fd8906cd
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Ricerca di moduli e risorse{#searching-for-forms-and-assets}

È possibile cercare i moduli o le risorse dei moduli utilizzando una stringa di testo o una stringa di testo insieme a caratteri jolly. Potete anche restringere la ricerca utilizzando i criteri disponibili in varie categorie nel pannello Ricerca.

Quando selezioni uno o più criteri e specifichi anche una stringa di testo, l’intersezione del testo e dei criteri viene restituita come risultato della ricerca. I risultati della ricerca sono validi quanto il modulo e i metadati della risorsa forniti.

Fai clic su ![aem6forms_search](assets/aem6forms_search.png) per mostrare o nascondere il pannello di ricerca.

## Ricerca di base {#basic-search}

Una ricerca di base è la ricerca predefinita, eseguita senza specificare alcun filtro. AEM Forms esegue una ricerca full-text sulle proprietà dei metadati.

Per eseguire una ricerca di base, immetti la query di ricerca nel campo di testo e premi Invio. È inoltre possibile immettere il carattere jolly (&#42;) in modo che corrisponda a un numero qualsiasi di caratteri.

Adobe Experience Manager cerca il testo immesso nelle proprietà dei metadati e restituisce i risultati corrispondenti. Se si digitano più parole, l&#39;operazione di ricerca corrisponderà al testo completo per la ricerca.

Per quanto riguarda la ricerca di base, tieni presente quanto segue:

* La ricerca viene eseguita utilizzando le proprietà dei metadati del modulo e della risorsa.
* Se si digitano più parole, l&#39;operazione di ricerca corrisponderà al testo completo per la ricerca.
* La ricerca non fa distinzione tra maiuscole e minuscole. Ad esempio, quando digiti `geometrixx`, le risorse con titoli `Geometrixx`, `GEOMETRIXX` e `GeoMetRixx` vengono visualizzate nei risultati della ricerca.

* Le corrispondenze parziali di una parola non sono supportate. Per eseguire ricerche utilizzando stringhe parziali, utilizzare il carattere jolly &#42;. Tuttavia, se la query di ricerca corrisponde a una parola completa, viene visualizzata la maschera o la risorsa corrispondente.
* Gli spazi aggiuntivi vengono rispettati e non vengono tagliati durante la ricerca. `My form`, ad esempio, non è la stessa query di ricerca di `My form`.

* Se i dati e i valori visualizzati dei campi nelle proprietà dei metadati sono diversi, non è possibile utilizzare i valori visualizzati come parametri di ricerca. Ad esempio, non è possibile eseguire ricerche in base a uno stato, ad esempio Modificato o Pubblicato, poiché queste proprietà vengono memorizzate in un formato diverso.

## Ricerca avanzata {#advanced-search}

Nei criteri di ricerca, oltre alla query puoi specificare alcuni parametri di ricerca per rendere la ricerca di base più efficiente e mirata.

![Campo di ricerca e parametri o filtri per il modulo AEM e la ricerca di risorse](assets/search_forms_assets.png)

Campo di ricerca e parametri o filtri per la ricerca di risorse e moduli in AEM

### Percorso risorsa {#asset-path}

Utilizzando il filtro percorso risorsa, puoi limitare i risultati della ricerca alla directory corrente. Se l&#39;opzione Cerca nella directory corrente non è selezionata, i risultati della ricerca contengono le risorse della directory di base. Se la pagina corrente non è una directory e l’opzione &quot;cerca nella directory corrente&quot; è selezionata, la ricerca restituisce le risorse presenti nella directory principale.

### Modifica risorsa {#asset-modification}

Seleziona una delle seguenti opzioni per eseguire ricerche in tutte le risorse modificate in un determinato periodo di tempo.

| **Opzione** | **Descrizione** |
|---|---|
| Due ore fa | Cerca in tutte le risorse modificate nelle ultime due ore. |
| Una settimana fa | Cerca in tutte le risorse modificate nell&#39;ultima settimana. |
| Un mese fa | Cerca in tutte le risorse modificate nell&#39;ultimo mese. |
| Un anno fa | Cerca in tutte le risorse modificate nell&#39;ultimo anno. |

### Stato risorsa {#asset-status}

Puoi cercare le risorse utilizzando uno dei seguenti stati:

* **Pubblicato**: cerca tutte le risorse pubblicate e non modificate dopo la pubblicazione.

* **Non pubblicato**: cerca tutte le risorse che non sono mai state pubblicate.

* **Modificato**: cerca tutte le risorse modificate o non pubblicate dopo la pubblicazione.

### Tipo risorsa {#asset-type}

Puoi selezionare un numero qualsiasi di tipi di risorse. La ricerca restituisce l’unione di tutti i tipi di risorse selezionati.

<table>
 <tbody>
  <tr>
   <th>Opzione</th> 
   <th>Descrizione</th> 
  </tr>
  <tr>
   <td>Modello modulo<br /> </td> 
   <td>Cerca in tutti i modelli di modulo.<br /> </td> 
  </tr>
  <tr>
   <td>PDF Form</td> 
   <td>Cerca in tutti i documenti di PDF.</td> 
  </tr>
  <tr>
   <td>Documento</td> 
   <td>Cerca in tutti i documenti.</td> 
  </tr>
  <tr>
   <td>Modulo adattivo<br /> </td> 
   <td>Cerca in tutti i moduli adattivi.</td> 
  </tr>
  <tr>
   <td>Risorsa</td> 
   <td>Cerca in tutte le risorse.<br /> </td> 
  </tr>
 </tbody>
</table>

### Tag {#tags}

I tag sono etichette allegate alle risorse per l’identificazione. Durante la ricerca, seleziona un numero qualsiasi di tag dal menu a discesa o aggiungi tag personalizzati, se necessario. Un risultato di ricerca contiene l&#39;intersezione dei tag selezionati.
