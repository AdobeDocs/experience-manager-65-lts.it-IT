---
title: Modifica della combinazione di colori dell'interfaccia
description: Come modificare in modo selettivo la combinazione di colori delle parti dell’interfaccia utente di AEM Forms Workspace.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: f15ead5f-d48c-401c-98c5-b58f93776f82
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Modifica della combinazione di colori dell&#39;interfaccia {#changing-the-color-scheme-of-the-interface}

Puoi modificare la combinazione di colori delle parti dell’interfaccia utente dell’area di lavoro di AEM Forms in base alle tue esigenze. Di seguito sono riportati alcuni esempi di personalizzazioni rappresentative delle combinazioni di colori. Oltre ai passaggi descritti in questo articolo, consulta [Passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).

## Barra di navigazione superiore {#top-navigation-bar}

### Utilizzo dell&#39;immagine di sfondo {#using-background-image}

Per aggiornare la barra di navigazione nella parte superiore dell’area di lavoro di AEM Forms.

1. Create un&#39;immagine di sfondo per aggiornare il colore. Denomina il file come newBackground.jpg.
1. Caricare il file di immagine di sfondo nella cartella /apps/ws/images utilizzando un client WebDAV.

   >[!NOTE]
   >
   >Per ulteriori informazioni, vedere [Accesso WebDAV](/help/sites-administering/webdav-access.md).

1. Fai riferimento alla nuova immagine di sfondo in /apps/ws/css/newStyle.css aggiungendo il seguente stile.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Utilizzo della proprietà color nel CSS {#using-color-property-in-css}

1. Aggiungi il seguente stile in newStyle.css in /apps/ws/css

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Componente categoria {#category-component}

Il componente Categoria visualizza le varie categorie delle attività nel pannello a sinistra. Per modificarne il colore, definisci il colore di sfondo nell&#39;elemento `.category` del file CSS.

## Componente attività {#task-component}

Le attività vengono visualizzate nel pannello centrale denominato Componente Elenco attività. Per modificarne il colore, modificare lo stile associato al selettore attività nel foglio di stile.
