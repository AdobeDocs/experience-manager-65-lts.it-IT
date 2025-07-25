---
title: Utilizzo dell’area di lavoro AEM Forms
description: Inizia a usare l’area di lavoro di AEM Forms con questa breve panoramica sui flussi di lavoro dei processi.
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: 7374797f-4154-402b-bb59-075134763c58
source-git-commit: 823923ab074bae1705cc1991e4079897e4c5cac8
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Utilizzo dell’area di lavoro AEM Forms{#working-with-aem-forms-workspace}

## Introduzione {#introduction}

AEM Forms Workspace fa parte di AEM Forms. Workspace facilita il rendering di HTML Forms oltre a PDF forms. Ora è possibile interagire con i processi aziendali dalle interfacce mobili e dalle applicazioni web.

Inoltre, lo spazio di lavoro AEM Forms è altamente personalizzabile utilizzando le metodologie di sviluppo standard di HTML e JavaScript™. Si tratta di un software basato su componenti che si integra facilmente con le altre applicazioni web.

Per ulteriori informazioni, vedere [Introduzione all&#39;area di lavoro di AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Acquisizione di familiarità {#getting-familiar}

Per avere familiarità con il processo end-to-end di creazione di un&#39;applicazione Forms per automatizzare un processo aziendale, seguire la procedura dettagliata. Dopo aver seguito la procedura dettagliata, è possibile creare, gestire e testare un&#39;applicazione utilizzando l&#39;area di lavoro Workbench, Designer e AEM Forms. Per informazioni dettagliate sull&#39;implementazione, vedere [Creazione della prima applicazione AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Panoramica funzionale {#functional-overview}

Puoi utilizzare l’area di lavoro di AEM Forms per eseguire le seguenti attività:

**Avvia un processo aziendale:** l&#39;area di lavoro di AEM Forms classifica i processi in base alla progettazione e alla configurazione dell&#39;organizzazione. Per accedere rapidamente alle categorie, puoi impostare come preferite quelle utilizzate di frequente. Quando si avvia un processo, in genere si compila un modulo per avviare un processo aziendale che costituisce i controlli del flusso di lavoro. Per ulteriori informazioni, vedere [Avvio dei processi](/help/forms/using/starting-processes.md).

**Visualizza e gestisci le attività:** Quando visualizzi gli elenchi delle attività, visualizzi le attività di un processo aziendale assegnate a te o a qualsiasi gruppo a cui appartieni o che sono attività condivise di altri utenti. È possibile aprire, lavorare e completare le attività in base alle esigenze. In genere, per completare un&#39;attività è necessario fornire informazioni, approvare un modulo o rifiutarlo. Per ulteriori informazioni, vedere [Utilizzo degli elenchi attività](/help/forms/using/todo-lists.md).

**Traccia attività**: per tenere traccia delle attività, utilizza la scheda Traccia dell&#39;area di lavoro di AEM Forms. Puoi cercare i processi attivi o completati a cui hai iniziato o partecipato. È possibile visualizzare le attività, le assegnazioni e le maschere che facevano parte del processo. È inoltre possibile avviare nuovi processi utilizzando i dati del modulo di un processo precedentemente avviato. Per ulteriori informazioni, vedere [Processi di tracciamento](/help/forms/using/tracking-processes.md).

## Nuova offerta di AEM Forms Workspace {#new-offering-of-aem-forms-workspace}

**Supporto per l&#39;approvazione in blocco delle attività**:

È possibile approvare più attività dello stesso tipo. Dopo aver selezionato un&#39;attività per l&#39;approvazione, rimangono abilitate solo le attività con lo stesso processo, con gli stessi nomi di attività e le stesse opzioni di instradamento. Per informazioni dettagliate sull&#39;implementazione, vedere [Utilizzo degli elenchi attività](/help/forms/using/todo-lists.md).

## Migrazione da Flex Workspace all’area di lavoro AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace non è supportato per i clienti AEM Forms. Tutti i clienti che utilizzano Flex Workspace devono passare ad AEM Forms Workspace.

Nell’area di lavoro di AEM Forms, i servizi predefiniti di rendering e invio, nel profilo azione predefinito, associati ai moduli XDP sono stati modificati e sono stati introdotti nuovi servizi. Per ulteriori dettagli, vedere [Nuovo servizio di rendering e invio](/help/forms/using/new-render-submit-service.md). Per eseguire la migrazione dei processi esistenti che funzionano con i moduli XDP e utilizzare questi servizi, puoi seguire [questi passaggi](new-render-submit-service.md).

**Mappatura delle personalizzazioni di Flex Workspace con l&#39;area di lavoro di AEM Forms**

La mappatura tra vari tipi di personalizzazioni in entrambe le aree di lavoro è la seguente.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo di personalizzazione </strong></td>
   <td><strong>Personalizzazioni coperte </strong></td>
   <td><strong>Scenario di personalizzazione dell’area di lavoro AEM Forms corrispondente</strong></td>
  </tr>
  <tr>
   <td>Personalizzazione della localizzazione</td>
   <td>
    <ol>
     <li>Modifica delle impostazioni locali di Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Modifica delle impostazioni internazionali dell’area di lavoro di AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizzazione del tema</td>
   <td>
    <ol>
     <li>Sostituzione delle immagini</li>
     <li>Modifica dei colori</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Modifica del logo dell'organizzazione</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Modifica della combinazione di colori</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizzazione del layout</td>
   <td>
    <ol>
     <li>Semplificazione dell'interfaccia utente di Workspace<br /> </li>
     <li>Creazione di una nuova schermata di accesso</li>
     <li>Creazione di un contenitore di approvazione personalizzato</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Utilizzo dei componenti riutilizzabili</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Creazione di una schermata di accesso</a></li>
     <li>Contenitore di approvazione obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Alcune delle funzioni di Flex Workspace che non sono disponibili nell’area di lavoro di AEM Forms includono: messaggi e notifiche, pagina di benvenuto, contenitore di approvazione e opzione per gestire le intestazioni di colonna. Per un elenco completo, vedere [Funzionalità di Flex Workspace non disponibili nell&#39;area di lavoro di AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Sviluppo con AEM Forms Workspace {#developing-with-aem-forms-workspace}

### Architettura {#architecture}

AEM Forms Workspace è un’applicazione web basata su HTML e JavaScript™ ospitata su CRX™. Quando l’URL di Workspace viene aperto in un browser, si accede a una risorsa CRX™ e l’applicazione viene riprodotta come pagina HTML nel browser. Le librerie JavaScript e il codice JavaScript personalizzato gestiscono il comportamento interno ed esterno dell’applicazione, ad esempio l’interfaccia utente, l’interazione con l’utente e la comunicazione con il server AEM Forms. Per ulteriori dettagli, vedere l&#39;area di lavoro di AEM Forms [architettura](/help/forms/using/html-workspace-architecture.md).

### Personalizzazione dell’area di lavoro di AEM Forms {#aem-forms-workspace-customization}

AEM Forms Workspace supporta un’ampia gamma di personalizzazioni per aggiornare il layout dell’interfaccia utente, il suo aspetto, la sua funzionalità e molto altro. Le personalizzazioni implicano l’aggiornamento di uno o più dei seguenti elementi:

* Aspetti dell&#39;interfaccia utente
* Funzionalità con personalizzazioni semantiche
* Riutilizzo dei componenti di HTML in altre applicazioni web

L&#39;articolo [personalizzazione](introduction-customizing-html-workspace.md#types-of-customizations) spiega i tipi di tali personalizzazioni.

### Configurare l’ambiente di sviluppo {#set-up-the-developer-environment}

I risultati finali dell’area di lavoro di AEM Forms includono un pacchetto CRX distribuito su CRX, un archivio SDK contenente il codice sorgente completo, librerie JavaScript di terze parti e script di generazione dell’area di lavoro di AEM Forms. Utilizzali per configurare l’ambiente per sviluppatori in modo da eseguire le personalizzazioni di cui sopra. Per ulteriori dettagli, vedere [Generazione del codice dell&#39;area di lavoro di AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Puoi personalizzare gran parte dell’interfaccia e delle funzionalità di base, ad esempio font, combinazione di colori, logo, schermata di accesso, finestre di dialogo per errori, integrazione con applicazioni di terze parti e riutilizzo di componenti in applicazioni di terze parti. È inoltre possibile migliorare il contenuto visualizzato nella pagina Riepilogo attività, visualizzare le immagini per le azioni di instradamento delle attività e persino modificare i modelli e le visualizzazioni di backbone di basso livello che creano l&#39;applicazione AEM Forms Workspace.

### Rendering HTML di XDP Forms {#html-rendering-of-xdp-forms}

Per impostazione predefinita, per un nuovo processo viene eseguito il rendering di un modulo XDP in formato PDF su un desktop e in formato HTML su un tablet. È sempre possibile eseguire il rendering di un modulo XDP in formato HTML. Per informazioni dettagliate, vedere [Nuovi servizi di rendering e invio](/help/forms/using/new-render-submit-service.md).

La funzionalità [Mobile Forms](/help/forms/using/introduction.md), che funziona con [profili](/help/forms/using/custom-profile.md), abilita il rendering HTML dei moduli XDP. Per impostazione predefinita, il &#39;Rendering nuovo HTML Form&#39; utilizza il profilo `default.html` che è possibile modificare. Puoi anche aggiungere modifiche personalizzate che si verificano prima del rendering di un modulo XDP in formato HTML.
