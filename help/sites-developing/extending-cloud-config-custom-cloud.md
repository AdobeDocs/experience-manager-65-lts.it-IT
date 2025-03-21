---
title: Creazione di un Cloud Service personalizzato
description: Il set predefinito di Cloud Services può essere esteso con tipi di Cloud Service personalizzati
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7ae41982-8438-41a6-91f9-3b3b6755a39b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 5%

---

# Creazione di un Cloud Service personalizzato{#creating-a-custom-cloud-service}

Il set predefinito di Cloud Services può essere esteso con tipi di Cloud Service personalizzati. Questo consente di inserire un markup personalizzato nella pagina in modo strutturato. Questa funzione è utile principalmente per i provider di analisi di terze parti, ad esempio Google Analytics, Chartbeat e così via. I servizi cloud vengono ereditati dalle pagine padre alle pagine figlie con la possibilità di interrompere l’ereditarietà a qualsiasi livello.

>[!NOTE]
>
>Questa guida dettagliata per la creazione di un Cloud Service è un esempio di utilizzo di Google Analytics. Tutto potrebbe non essere applicabile al tuo caso d’uso.

1. In CRXDE Lite, creare un nodo in `/apps`:

   * **Nome**: `acs`
   * **Tipo**: `nt:folder`

1. Crea un nodo in `/apps/acs`:

   * **Nome**: `analytics`
   * **Tipo**: `sling:Folder`

1. Crea due nodi in `/apps/acs/analytics`:

   * **Nome**: componenti
   * **Tipo**: `sling:Folder`

   e

   * **Nome**: modelli
   * **Tipo**: `sling:Folder`

1. Fare clic con il pulsante destro del mouse su `/apps/acs/analytics/components`. Seleziona **Crea...** seguito da **Crea componente...** La finestra di dialogo visualizzata consente di specificare:

   * **Etichetta**: `googleanalyticspage`
   * **Titolo**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Gruppo**: `.hidden`

1. Fai clic due volte su **Avanti** e specifica:

   * **Elementi padre consentiti:** `acs/analytics/templates/googleanalytics`

   Fai clic due volte su **Avanti** e fai clic su **OK**.

1. Aggiungi una proprietà a `googleanalyticspage`:

   * **Nome:** `cq:defaultView`
   * **Valore:** `html`

1. Creare un file denominato `content.jsp` in `/apps/acs/analytics/components/googleanalyticspage` con il contenuto seguente:

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. Crea un nodo in `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nome**: `dialog`
   * **Tipo**: `cq:Dialog`
   * **Proprietà**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valore**: `Google Analytics Config`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valore**: `dialog`

1. Crea un nodo in `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nome**: `items`
   * **Tipo**: `cq:Widget`
   * **Proprietà**:

      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valore**: `tabpanel`

1. Crea un nodo in `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nome**: `items`
   * **Tipo**: `cq:WidgetCollection`

1. Crea un nodo in `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nome**: scheda1
   * **Tipo**: `cq:Panel`
   * **Proprietà**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valore**: `Config`

1. Crea un nodo in `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nome**: elementi
   * **Tipo**: `nt:unstructured`
   * **Proprietà**:

      * **Nome**: `fieldLabel`
      * **Tipo**: Stringa
      * **Valore**: ID account

      * **Nome**: `fieldDescription`
      * **Tipo**: `String`
      * **Valore**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nome**: `name`
      * **Tipo**: `String`
      * **Valore**: `./accountID`
      * **Nome**: `validateOnBlur`
      * **Tipo**: `String`
      * **Valore**: `true`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valore**: `textfield`

1. Copiare `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` in `/apps/acs/analytics/components/googleanalyticspage/body.jsp` e modificare `libs` in `apps` alla riga 34 e rendere il riferimento allo script alla riga 79 un percorso completo.
1. Crea un modello in `/apps/acs/analytics/templates/`:

   * con **Tipo risorsa** = `acs/analytics/components/googleanalyticspage`
   * con **etichetta** = `googleanalytics`
   * con **Titolo**= `Google Analytics Configuration`
   * con **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * con **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * con **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (nel nodo modello, non nel nodo jcr:content)
   * con **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (in jcr:content)

1. Creare un componente: `/apps/acs/analytics/components/googleanalytics`.

   Aggiungi il seguente contenuto a `googleanalytics.jsp`:

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   Questo dovrebbe generare il markup personalizzato in base alle proprietà di configurazione.

1. Passare a `http://localhost:4502/miscadmin#/etc/cloudservices` e creare una pagina:

   * **Titolo**: `Google Analytics`
   * **Nome**: `googleanalytics`

   Tornare in CRXDE Lite e in `/etc/cloudservices/googleanalytics` aggiungere la seguente proprietà a `jcr:content`:

   * **Nome**: `componentReference`
   * **Tipo**: `String`
   * **Valore**: `acs/analytics/components/googleanalytics`

1. Passare alla pagina Servizio appena creata ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) e fare clic su **+** per creare una configurazione:

   * **Configurazione padre**: `/etc/cloudservices/googleanalytics`
   * **Titolo:** `My First GA Config`

   Scegli **Configurazione Google Analytics** e fai clic su **Crea**.

1. Immettere un **ID account**, ad esempio `AA-11111111-1`. Fai clic su **OK**.
1. Passa a una pagina e aggiungi la configurazione appena creata nelle proprietà della pagina, nella scheda **Cloud Services**.
1. Alla pagina verrà aggiunto il markup personalizzato.
