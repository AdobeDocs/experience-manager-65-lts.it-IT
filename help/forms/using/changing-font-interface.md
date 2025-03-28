---
title: Modifica del tipo di carattere nell'interfaccia
description: Come modificare selettivamente i caratteri nell'interfaccia utente.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: e27ff9df-41d0-4eef-b04e-a3eefea3c9ab
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Modifica del tipo di carattere nell&#39;interfaccia{#changing-the-font-on-the-interface}

Puoi modificare il font visualizzato nell’area di lavoro di AEM Forms. I font utilizzati in una sezione specifica dell&#39;interfaccia utente sono definiti nella sezione corrispondente del foglio di stile. È possibile modificare i caratteri nell&#39;interfaccia utente in modo selettivo.

Segui i [passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md) e, a seconda delle tue esigenze, segui i passaggi per personalizzare CSS, HTML o entrambi.

1. Modificate o aggiungete la famiglia font in uno stile esistente.
1. Modifica o aggiungi la famiglia di caratteri in linea per l&#39;elemento HTML.
1. Aggiungi uno stile e utilizzalo per l’elemento HTML.

Ad esempio, per modificare il tipo di carattere del testo di ancoraggio della barra di navigazione superiore in Courier New, effettuare le seguenti operazioni:

1. Accedere a CRXDE Lite accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Effettua una delle seguenti operazioni:

   1. Per modificare la famiglia di caratteri in uno stile esistente, aggiungi quanto segue nel file newStyle.css in /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. Per aggiungere la famiglia di caratteri in linea per l&#39;elemento HTML, copiare il file `/libs/ws/js/runtime/templates/appnavigation.html` in `/apps/ws/js/runtime/templates/appnavigation.html`.

      Aggiornare il file /apps/ws/js/runtime/templates/appnavigation.html come segue:

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Aprire il file /apps/ws/js/registry.js per la modifica e sostituire `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` con `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. Per aggiungere uno stile che definisca la famiglia font, aggiungi quanto segue nel file newStyle.css in /apps/ws/css.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      Per aggiungere la famiglia di caratteri in linea per l&#39;elemento HTML, aggiungi quanto segue nel file appnavigation.html in /apps/ws/js/runtime/templates.

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Riavvia l’area di lavoro e cancella la cache del browser per rendere visibili le modifiche.

![cambia_font_prima](assets/change_font_before.png)

Barra di navigazione superiore prima della personalizzazione dei caratteri

![cambia_font_dopo](assets/change_font_after.png)

Barra di navigazione superiore dopo la personalizzazione del font della prima scheda
