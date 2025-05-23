---
title: Personalizzazione della console Siti web (interfaccia classica)
description: La console di amministrazione dei siti Web può essere estesa per visualizzare colonne personalizzate
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 445cb8c3-e0c4-44f8-a140-9e7215e3b73a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# Personalizzazione della console Siti web (interfaccia classica){#customizing-the-websites-console-classic-ui}

## Aggiunta di una colonna personalizzata alla console Siti Web (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

La console di amministrazione dei siti Web può essere estesa per visualizzare colonne personalizzate. La console è basata su un oggetto JSON che può essere esteso creando un servizio OSGI che implementa l&#39;interfaccia `ListInfoProvider`. Tale servizio modifica l’oggetto JSON inviato al client per generare la console.

Questo tutorial dettagliato spiega come visualizzare una nuova colonna nella console di amministrazione dei siti Web implementando l&#39;interfaccia `ListInfoProvider`. È costituito dai seguenti passaggi:

1. [Creazione del servizio OSGI](#creating-the-osgi-service) e distribuzione del bundle che lo contiene nel server AEM.
1. (facoltativo) [Verifica del nuovo servizio](#testing-the-new-service) tramite l&#39;emissione di una chiamata JSON per richiedere l&#39;oggetto JSON utilizzato per generare la console.
1. [Visualizzazione della nuova colonna](#displaying-the-new-column) tramite l&#39;estensione della struttura dei nodi della console nell&#39;archivio.

>[!NOTE]
>
>Questo tutorial può essere utilizzato anche per estendere le seguenti console di amministrazione:
>
>* la console Digital Assets
>* la console Community
>

### Creazione del servizio OSGI {#creating-the-osgi-service}

L&#39;interfaccia `ListInfoProvider` definisce due metodi:

* `updateListGlobalInfo`, per aggiornare le proprietà globali dell&#39;elenco
* `updateListItemInfo`, per aggiornare una singola voce di elenco.

Gli argomenti per entrambi i metodi sono:

* `request`, l&#39;oggetto di richiesta HTTP Sling associato,
* `info`, l&#39;oggetto JSON da aggiornare, che è rispettivamente l&#39;elenco globale o la voce di elenco corrente,
* `resource`, una risorsa Sling.

Di seguito è riportato un esempio di implementazione:

* Aggiunge una proprietà *starred* per ogni elemento, ovvero `true` se il nome della pagina inizia con *e*, altrimenti `false`.

* Aggiunge una proprietà *starredCount*, che è globale per l&#39;elenco e contiene il numero di elementi dell&#39;elenco di cui è stata eseguita la visualizzazione.

Per creare il servizio OSGI:

1. In CRXDE Lite, [crea un bundle](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Aggiungi il codice di esempio seguente.
1. Crea il bundle.

Il nuovo servizio è operativo.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* L’implementazione deve decidere, in base alla richiesta e/o alla risorsa fornite, se aggiungere o meno le informazioni all’oggetto JSON.
>* Se l&#39;implementazione di `ListInfoProvider` definisce una proprietà esistente nell&#39;oggetto di risposta, il relativo valore viene sovrascritto da quello fornito.
>
>  È possibile utilizzare [classificazione servizio](https://docs.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) per gestire l&#39;ordine di esecuzione di più implementazioni `ListInfoProvider`.

### Test del nuovo servizio {#testing-the-new-service}

Quando apri la console di amministrazione dei siti web e esplori il sito, il browser emette una chiamata Ajax per ottenere l’oggetto JSON utilizzato per generare la console. Quando ad esempio si passa alla cartella `/content/geometrixx`, la seguente richiesta viene inviata al server AEM per generare la console:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Per assicurarti che il nuovo servizio sia in esecuzione dopo aver distribuito il bundle che lo contiene:

1. Puntare il browser al seguente URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. La risposta deve visualizzare le nuove proprietà come segue:

![schermata_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visualizzazione della nuova colonna {#displaying-the-new-column}

L&#39;ultimo passaggio consiste nell&#39;adattare la struttura dei nodi della console di amministrazione dei siti Web per visualizzare la nuova proprietà per tutte le pagine di Geometrixx sovrapponendo `/libs/wcm/core/content/siteadmin`. Procedere come segue:

1. In CRXDE Lite creare la struttura dei nodi `/apps/wcm/core/content` con nodi di tipo `sling:Folder` per riflettere la struttura `/libs/wcm/core/content`.

1. Copiare il nodo `/libs/wcm/core/content/siteadmin` e incollarlo sotto `/apps/wcm/core/content`.

1. Copiare il nodo `/apps/wcm/core/content/siteadmin/grid/assets` in `/apps/wcm/core/content/siteadmin/grid/geometrixx` e modificarne le proprietà:

   * Rimuovi **testoPagina**

   * Imposta **pathRegex** su `/content/geometrixx(/.*)?`
In questo modo la configurazione della griglia viene attivata per tutti i siti Web Geometrixx.

   * Imposta **storeProxySuffix** su `.pages.json`

   * Modificare la proprietà multivalore **storeReaderFields** e aggiungere il valore `starred`.

   * Per attivare la funzionalità MSM, aggiungere i seguenti parametri MSM alla proprietà multistringa **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Aggiungi un nodo `starred` (di tipo **nt:unstructured**) sotto `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` con le seguenti proprietà:

   * **dataIndex**: `starred` di tipo String

   * **intestazione**: `Starred` di tipo String

   * **xtype**: `gridcolumn` di tipo String

1. (facoltativo) Rilasciare le colonne che non si desidera visualizzare in `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` è un percorso personalizzato che, per impostazione predefinita, punta a `/libs/wcm/core/content/siteadmin`.
Per reindirizzarlo alla versione di siteadmin in `/apps/wcm/core/content/siteadmin`, definire la proprietà `sling:vanityOrder` in modo che abbia un valore superiore a quello definito in `/libs/wcm/core/content/siteadmin`. Il valore predefinito è 300, quindi qualsiasi valore più alto è adatto.

1. Passa alla console di amministrazione dei siti Web e passa al sito Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. La nuova colonna denominata **Starred** è disponibile e visualizza le informazioni personalizzate nel modo seguente:

![schermata_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Se più configurazioni della griglia corrispondono al percorso richiesto definito dalla proprietà **pathRegex**, viene utilizzato il primo e non il più specifico, il che significa che l&#39;ordine delle configurazioni è importante.

### Pacchetto di esempio {#sample-package}

Il risultato di questa esercitazione è disponibile nel pacchetto [Personalizzazione della console di amministrazione dei siti Web](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) in Condivisione pacchetti.
