---
title: Implementazione di riferimento We.Retail
description: We.Retail è un'anteprima tecnologica di un'implementazione di riferimento che illustra il modo consigliato di impostare una presenza online con AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 71a49353-5273-46ee-a1ff-5bbfe5b6b0b4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 7%

---

# Implementazione di riferimento We.Retail{#we-retail-reference-implementation}

## Introduzione {#introduction}

We.Retail è un&#39;implementazione di riferimento e un contenuto di esempio che illustra il modo consigliato di impostare una presenza online con Adobe Experience Manager.

We.Retail utilizza le più recenti tecnologie Adobe Experience Manager (AEM), come HTL, layout reattivi, modelli modificabili, componenti core e molto altro.

Anche se illustra un settore verticale, la configurazione del sito può essere applicata a qualsiasi settore verticale e solo le funzioni del catalogo e del carrello dei prodotti sono specifiche per il settore retail.

## Funzioni {#features}

Come implementazione di riferimento standard di AEM, We.Retail presenta alcune delle funzioni più potenti di AEM.

| **Funzionalità** | **Descrizione** | **Interessato?** |
|---|---|---|
| [Struttura del sito globalizzata](/help/sites-administering/tc-bp.md) | We.Retail include master di lingua che vengono copiati live nei siti specifici del paese. | [Prova!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Layout reattivo](/help/sites-authoring/responsive-layout.md) | Tutte le pagine dispongono di un layout dinamico per adattarsi dinamicamente alle dimensioni dello schermo e del dispositivo. | [Prova!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Modelli modificabili](/help/sites-developing/page-templates-editable.md) | Tutte le pagine sono basate su modelli modificabili, che consentono agli utenti non sviluppatori di adattare e personalizzare i modelli. | [Prova!](/help/sites-developing/we-retail-editable-templates.md) |
| [Lingua modello HTML](https://experienceleague.adobe.com/it/docs/experience-manager-htl/content/overview) | Tutti i componenti sono basati su HTL |  |
| [Componenti di base](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/introduction) | Tutti i componenti sono basati sui nuovi componenti core e sono più utilizzabili e configurabili dall’utente, pronti all’uso | [Prova!](/help/sites-developing/we-retail-core-components.md) |
| [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) | La sezione Esperienze We.Retail presenta la potenza di riutilizzare i contenuti tramite frammenti di contenuto. | [Prova!](/help/sites-developing/we-retail-content-fragments.md) |
| [Frammenti esperienza](/help/sites-authoring/experience-fragments.md) | Un frammento di esperienza è un gruppo di uno o più componenti, inclusi il contenuto e il layout, a cui è possibile fare riferimento all’interno delle pagine. | [Prova!](/help/sites-developing/we-retail-experience-fragments.md) |

## Guida introduttiva {#getting-started}

We.Retail viene distribuito come contenuto di esempio di AEM. Per utilizzare, è sufficiente [avviare AEM come si farebbe normalmente](/help/sites-deploying/deploy.md#getting-started), assicurandosi che il contenuto di esempio non sia disabilitato.

>[!CAUTION]
>
>Non installare We.Retail sulle istanze di produzione. Le istanze di produzione devono essere avviate in `nosamplecontent` [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail si basa sulla tecnologia AEM più recente e pertanto non supporta l&#39;authoring dell&#39;[interfaccia utente classica](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md).

### Ultima versione {#latest-version}

Anche se We.Retail è distribuito con la versione di AEM, è possibile che gli aggiornamenti al contenuto e alle relative funzioni vengano apportati dopo tale versione. È quindi possibile [scaricare l&#39;ultima versione da GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases), quindi [caricarla](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [installarla](/help/sites-administering/package-manager.md#installing-packages) come pacchetto nell&#39;istanza AEM.

### Primi passi {#first-steps}

1. Dopo l&#39;avvio di AEM (e/o l&#39;installazione di We.Retail), il sito **We.Retail** è disponibile nella [console Sites](/help/sites-authoring/basic-handling.md#global-navigation).
1. Ad esempio, è possibile aprire la pagina seguente, che deve essere visualizzata come illustrato nell&#39;[appendice](#appendix) seguente:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail e Geometrixx {#we-retail-geometrixx}

Geometrixx e le sue molte incarnazioni servivano come contenuto campione nelle versioni precedenti di AEM. A partire dalla versione 6.3, We.Retail è il contenuto di esempio consegnato con AEM e funge da nuova implementazione di riferimento standard.

We.Retail è tecnicamente più robusto e sfrutta la tecnologia AEM più recente per essere più flessibile e scalabile, presentando al contempo le nuove funzioni del prodotto.

### Caratteristiche a confronto {#feature-comparison}

La tabella seguente offre una panoramica delle principali funzioni disponibili in We.Retail rispetto a Geometrixx.

* **Disponibile** significa che nel contenuto di esempio sono presenti esempi della funzionalità.
* **Non disponibile** significa che alcuni esempi della funzionalità non sono disponibili nel contenuto di esempio, ma non significa che la funzionalità stessa non lo sia.

| **Funzionalità** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Struttura globale del sito | I master di lingua vengono copiati in tempo reale nei siti specifici del paese | Non disponibile |
| Frammenti di contenuto | Disponibile | Non disponibile |
| Frammenti di esperienza | Disponibile | Non disponibile |
| Layout reattivo | Per tutte le pagine | Solo Geometrixx Medie |
| Modelli modificabili | Per tutte le pagine | Non disponibile |
| HTL | Tutti i componenti | Limitato |
| Targeting | Per tutte le pagine | Solo Geometrixx Outdoors |
| Manoscritti | Non disponibile | Disponibile |
| Visualizzatore carosello, download e componenti per grafici | Non disponibile | Disponibile |
| Controllo colonna | Sostituito dal contenitore di layout | Disponibile |
| Moduli | Non disponibile | Disponibile |
| Campaign | Nessun esempio di e-mail | Disponibile |

>[!NOTE]
>
>L’elenco si prefigge di essere completo, ma non deve essere considerato esaustivo.

## Contribuisci {#contribute}

We.Retail è stato rilasciato come progetto open-source e l&#39;ultima versione del codice sorgente può essere scaricata da GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub.

* [Apri progetto aem-sample-we-retail su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Scarica il progetto come [file ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)

La versione più recente può anche essere [scaricata direttamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0) come pacchetto installabile.

In caso di problemi, segnala un [problema GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Puoi effettuare il forking o contribuire con [richieste pull](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Anteprima {#preview}

Anteprima della pagina di benvenuto di We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
