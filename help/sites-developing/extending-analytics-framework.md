---
title: Personalizzazione del framework Adobe Analytics
description: Scopri come personalizzare il framework Adobe Analytics per Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
exl-id: 6a32bd9d-268d-4d03-b495-47ec6660c138
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 0%

---

# Personalizzazione del framework Adobe Analytics{#customizing-the-adobe-analytics-framework}

Il framework Adobe Analytics determina le informazioni tracciate con Adobe Analytics. Per personalizzare il framework predefinito, puoi utilizzare JavaScript per aggiungere il tracciamento personalizzato, integrare i plug-in di Adobe Analytics e modificare le impostazioni generali nel framework utilizzato per il tracciamento.

## Informazioni sul JavaScript generato per i framework {#about-the-generated-javascript-for-frameworks}

Quando una pagina è associata a un framework Adobe Analytics e la pagina include [riferimenti al modulo Analytics](/help/sites-administering/adobeanalytics.md), per la pagina viene generato automaticamente un file analytics.sitecatalyst.js.

Il JavaScript nella pagina crea un oggetto `s_gi` definito dalla libreria Adobe Analytics s_code.js e assegna valori alle relative proprietà. Il nome dell&#39;istanza dell&#39;oggetto è `s`. Gli esempi di codice presentati in questa sezione fanno diversi riferimenti a questa variabile `s`.

Il codice di esempio seguente è simile al codice di un file analytics.sitecatalyst.js:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Quando si utilizza un codice JavaScript personalizzato per personalizzare il framework, si modifica il contenuto di questo file.

## Configurazione delle proprietà di Adobe Analytics {#configuring-adobe-analytics-properties}

In Adobe Analytics sono disponibili diverse variabili predefinite configurabili in un framework. Per impostazione predefinita, le variabili **charset**, **cookieLifetime**, **currencyCode** e **trackInlineStats** sono incluse nell&#39;elenco **Impostazioni generali di Analytics**.

![aa-22](assets/aa-22.png)

Puoi aggiungere nomi e valori di variabili all’elenco. Queste variabili predefinite ed eventuali variabili aggiunte vengono utilizzate per configurare le proprietà dell&#39;oggetto `s` nel file analytics.sitecatalyst.js. Nell&#39;esempio seguente viene illustrato come la proprietà `prop10` aggiunta del valore `CONSTANT` è rappresentata nel codice JavaScript:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

Per aggiungere variabili all’elenco, utilizza la procedura seguente:

1. Nella pagina del framework di Adobe Analytics, espandi l&#39;area **Impostazioni generali di Analytics**.
1. Sotto l’elenco delle variabili, fai clic su Aggiungi elemento per aggiungere una nuova variabile all’elenco.
1. Nella cella di sinistra immettere un nome per la variabile, ad esempio `prop10`.

1. Nella colonna di destra immettere un valore per la variabile, ad esempio `CONSTANT`.

1. Per rimuovere una variabile, fai clic sul pulsante (-) accanto alla variabile.

>[!NOTE]
>
>Quando immetti variabili e valori, assicurati che siano formattati e digitati correttamente, altrimenti le **chiamate non verranno inviate** con la coppia valore/variabile corretta. Variabili e valori errati possono anche impedire il verificarsi di chiamate.
>
>Rivolgiti al tuo rappresentante Adobe Analytics per assicurarti che queste variabili siano impostate correttamente.

>[!CAUTION]
>
>Alcune delle variabili in questo elenco sono **obbligatorie** per il corretto funzionamento delle chiamate di Adobe Analytics (ad esempio, **currencyCode**, **charSet**).
>
>Pertanto, anche se vengono rimossi dal framework stesso, verranno comunque allegati con un valore predefinito quando viene effettuata la chiamata Adobe Analytics.

### Aggiunta di JavaScript personalizzati a un framework Adobe Analytics {#adding-custom-javascript-to-an-adobe-analytics-framework}

La casella free-from JavaScript nell&#39;area **General Analytics Settings** (Impostazioni generali di Analytics) consente di aggiungere codice personalizzato a un framework Adobe Analytics.

![aa-21](assets/aa-21.png)

Il codice aggiunto viene aggiunto al file analytics.sitecatalyst.js. È quindi possibile accedere alla variabile `s`, che è un&#39;istanza dell&#39;oggetto JavaScript `s_gi` definito in `s_code.js`. Ad esempio, l&#39;aggiunta del codice seguente equivale all&#39;aggiunta di una variabile denominata `prop10` del valore `CONSTANT`, che è l&#39;esempio della sezione precedente:

`s.prop10= 'CONSTANT';`

Il codice nel file [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) (che include il contenuto del file Adobe Analytics `s-code.js`) contiene il seguente codice:

`if (s.usePlugins) s.doPlugins(s)`

La procedura seguente illustra come utilizzare la casella JavaScript per personalizzare il tracciamento di Adobe Analytics. Se il tuo JavaScript deve utilizzare i plug-in di Adobe Analytics, [integrali](/help/sites-administering/adobeanalytics.md) in AEM.

1. Aggiungere il codice JavaScript seguente alla casella in modo che `s.doPlugins` venga eseguito:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Questo codice è necessario se desideri inviare variabili in una chiamata Adobe Analytics che sono state personalizzate in un modo che non può essere fatto tramite l’interfaccia di trascinamento di base O tramite JavaScript in linea nella vista Adobe Analytics.
   >
   >Se le variabili personalizzate sono esterne alla funzione s_doPlugins, verranno inviate come *non definito *nella chiamata di Adobe Analytics

1. Aggiungi il codice JavaScript nella funzione **s_doPlugins**.

L’esempio seguente concatena i dati acquisiti su una pagina in ordine gerarchico, utilizzando un separatore comune di &quot;|&quot;.

Un framework Adobe Analytics presenta le seguenti configurazioni:

* La variabile Adobe Analytics `prop2` è mappata alla proprietà del sito `pagedata.sitesection`.

* La variabile Adobe Analytics `prop3` è mappata alla proprietà del sito `pagedata.subsection`.

* Il codice seguente viene aggiunto alla casella di controllo JavaScript non associato:

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* Quando viene visitata la pagina web che utilizza il framework (o, in modalità di modifica, quando la pagina viene ricaricata o visualizzata in anteprima), vengono eseguite le chiamate ad Adobe Analytics.

Ad esempio, in Adobe Analytics vengono generati i seguenti valori:

![aa-20](assets/aa-20.png)

### Aggiunta di codice personalizzato globale per tutti i framework di Adobe Analytics {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

Fornisci un codice JavaScript personalizzato integrato in tutti i framework di Adobe Analytics. Quando il framework Adobe Analytics di una pagina non contiene [JavaScript in formato libero](/help/sites-administering/adobeanalytics.md) personalizzato, il JavaScript generato dallo script /libs/cq/analytics/components/sitecatalyst/config.js.jsp viene aggiunto al file [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md). Per impostazione predefinita, lo script non ha alcun effetto perché è stato escluso. Il codice imposta anche `s.usePlugins` su `false`:

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Il codice nel file analytics.sitecatalyst.js (che include il contenuto del file Adobe Analytics s_code.js) contiene il seguente codice:

if (s.usePlugins) s.doPlugins(s)

Pertanto, il tuo JavaScript deve impostare `s.usePlugins` su `true` in modo che venga eseguito qualsiasi codice nella funzione `s_doPlugins`. Per personalizzare il codice, sovrapponi il file config.js.jsp con uno che utilizza il tuo JavaScript. Se il tuo JavaScript deve utilizzare i plug-in di Adobe Analytics, [integrali](/help/sites-administering/adobeanalytics.md) in AEM.

>[!NOTE]
>
>Non modificare il file /libs/cq/analytics/components/sitecatalyst/config.js.jsp. Alcune attività di aggiornamento o manutenzione di AEM possono reinstallare il file originale, rimuovendo le modifiche.

1. In CRXDE Lite, crea la struttura di cartelle /apps/cq/analytics/components:

   1. Fai clic con il pulsante destro del mouse sulla cartella /apps e scegli Crea > Crea cartella.
   1. Specificare `cq` come nome della cartella e fare clic su OK.
   1. Creare le cartelle `analytics` e `components`.

1. Fare clic con il pulsante destro del mouse sulla cartella `components` creata e scegliere Crea > Crea componente. Specifica i seguenti valori delle proprietà:

   * Etichetta: `sitecatalyst`
   * Titolo: `sitecatalyst`
   * Super Type: `/libs/cq/analytics/components/sitecatalyst`
   * Gruppo: `hidden`

1. Fare clic ripetutamente su Avanti finché il pulsante OK non viene attivato, quindi scegliere OK.

   Il componente sitecatalyst contiene il file sitecatalyst.jsp creato automaticamente.

1. Fai clic con il pulsante destro del mouse sul file sitecatalyst.jsp e fai clic su Elimina.

1. Fai clic con il pulsante destro del mouse sul componente SiteCatalyst e scegli Crea > Crea file. Specificare il nome `config.js.jsp` e quindi fare clic su OK.

   Il file config.js.jsp viene aperto automaticamente per la modifica.

1. Aggiungere il testo seguente al file, quindi fare clic su Salva tutto:

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   Il codice JavaScript generato dallo script /apps/cq/analytics/components/sitecatalyst/config.js.jsp viene ora inserito nel file analytics.sitecatalyst.js per tutte le pagine che utilizzano un framework Adobe Analytics.

1. Aggiungere il codice JavaScript che si desidera eseguire nella funzione `s_doPlugins` e quindi fare clic su Salva tutto.

>[!CAUTION]
>
>Se nel JavaScript in formato libero del framework di una pagina è presente del testo (anche solo uno spazio vuoto), config.js.jsp viene ignorato.

### Utilizzo dei plug-in di Adobe Analytics in AEM {#using-adobe-analytics-plugins-in-aem}

Ottieni il codice JavaScript per i plug-in di Adobe Analytics e integrali nel framework Adobe Analytics in AEM. Aggiungere il codice a una cartella della libreria client della categoria `sitecatalyst.plugins` in modo che sia disponibile per il codice JavaScript personalizzato.

Se ad esempio si integra il plug-in `getQueryParams`, è possibile chiamare il plug-in dalla funzione `s_doPlugins` del JavaScript personalizzato. Il codice di esempio seguente invia la stringa di query in **&quot;pid&quot;** dall&#39;URL del referente come **eVar1**, quando viene attivata una chiamata Adobe Analytics.

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM installa i seguenti plug-in di Adobe Analytics, in modo che siano disponibili per impostazione predefinita:

* getQueryParam()
* getPreviousValue()
* split()

La cartella della libreria client /libs/cq/analytics/clientlibs/sitecatalyst/plugins include questi plug-in nella categoria sitecatalyst.plugins.

>[!NOTE]
>
>Crea una cartella della libreria client per i plug-in. Non aggiungere plug-in alla cartella `/libs/cq/analytics/clientlibs/sitecatalyst/plugins`. Questa procedura garantisce che il contributo alla categoria `sitecatalyst.plugins` non venga sovrascritto durante le reinstallazioni o le attività di aggiornamento di AEM.

Utilizza la procedura seguente per creare la cartella della libreria client per i plug-in. È necessario eseguire questa procedura una sola volta. Per aggiungere un plug-in alla cartella della libreria client, attenersi alla procedura seguente.

1. In un browser web, apri CRXDE Lite. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Fai clic con il pulsante destro del mouse sulla cartella /apps/my-app/clientlibs e scegli Crea > Crea nodo. Immettere i valori delle proprietà seguenti e quindi fare clic su OK:

   * Nome: un nome per la cartella della libreria client, ad esempio my-plugins

   * Tipo: cq:ClientLibraryFolder

1. Seleziona la cartella della libreria client creata e utilizza la barra delle proprietà in basso a destra per aggiungere la seguente proprietà:

   * Nome: categorie
   * Tipo: String
   * Valore: sitecatalyst.plugins
   * Multiplo: selezionato

   Fare clic su OK nella finestra Modifica per confermare il valore della proprietà.

1. Fare clic con il pulsante destro del mouse sulla cartella della libreria client creata e scegliere Crea > Crea file. Per il nome file, digitare js.txt e quindi fare clic su OK.

1. Fai clic su Salva tutto.

Utilizza la procedura seguente per ottenere il codice del plug-in, archiviarlo nell’archivio AEM e aggiungerlo alla cartella della libreria client.

1. Accedi a [sc.omniture.com](https://sc.omniture.com/login/) con il tuo account Adobe Analytics.
1. Nella pagina di destinazione, vai a Aiuto > Home dell’Aiuto.
1. Nel sommario a sinistra, fai clic su Plug-in di implementazione.
1. Fai clic sul collegamento al plug-in che desideri aggiungere e, all’apertura della pagina, individua il codice sorgente JavaScript per il plug-in, quindi selezionalo e copialo.

1. Fai clic con il pulsante destro del mouse sulla cartella della libreria client e fai clic su Crea > Crea file. Per il nome del file, digitare il nome del plug-in da integrare seguito da .js e quindi fare clic su OK. Ad esempio, se integri il plug-in getQueryParam, assegna al file il nome getQueryParam.js.

   Quando create il file, questo viene aperto per la modifica.

1. Incolla il codice JavaScript del plug-in nel file, fai clic su Salva tutto, quindi chiudi il file.

1. Apri il file js.txt dalla cartella della libreria client.

1. In una nuova riga, aggiungi il nome del file che contiene il plug-in, ad esempio getQueryParam.js. Quindi, fate clic su Salva tutto (Save All) e chiudete il file.

>[!NOTE]
>
>Quando si utilizzano i plug-in, assicurarsi di integrare anche eventuali plug-in di supporto, altrimenti il plug-in JavaScript non riconoscerà le chiamate effettuate alle funzioni nel plug-in di supporto. Ad esempio, il plug-in getPreviousValue() richiede il corretto funzionamento del plug-in split().
>
>È necessario aggiungere il nome del plug-in di supporto anche a **js.txt**.
