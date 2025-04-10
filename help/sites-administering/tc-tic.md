---
title: Configurazione del framework di integrazione della traduzione
description: Scopri come configurare il Translation Integration Framework in Adobe Experience Manager.
contentOwner: Guillaume Carlino
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b89e2899-35b9-4105-bfa5-ca21dc6f4e14
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 44%

---

# Configurazione del framework di integrazione della traduzione{#configuring-the-translation-integration-framework}

Il Translation Integration Framework si integra con servizi di traduzione di terze parti per orchestrare la traduzione dei contenuti AEM.

* Connessione al fornitore di servizi di traduzione.
* Creare una configurazione del framework di integrazione della traduzione.
* Associa le configurazioni cloud alle pagine.

Per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md).

## Connessione a un fornitore di servizi di traduzione {#connecting-to-a-translation-service-provider}

Crea una configurazione cloud che connette AEM al provider di servizi di traduzione.

AEM include la funzionalità per [connettersi a Microsoft® Translator](/help/sites-administering/tc-msconf.md) per impostazione predefinita. Altri fornitori di tecnologie di traduzione con connettori AEM che sono membri del programma partner Adobe Exchange sono disponibili [qui](https://exchange.adobe.com/apps/browse/ec?page=1&amp;partnerLevel=All&amp;product=AEM&amp;q=experience+manager+translation&amp;sort=RELEVANCE).

Dopo aver installato un pacchetto di connettori, puoi crearne una configurazione cloud. In genere, devi fornire le credenziali per l&#39;autenticazione con il servizio di traduzione. Per informazioni sull’aggiunta di una configurazione cloud per il connettore Microsoft Translator, vedi [Integrazione con Microsoft Translator](/help/sites-administering/tc-msconf.md).

Se necessario, puoi creare più configurazioni cloud per lo stesso connettore. Ad esempio, crea una configurazione per ciascuno degli account o dei progetti che hai con lo stesso fornitore.

Dopo aver configurato una connessione, potete creare la configurazione del Translation Integration Framework che la utilizza.

## Creazione di una configurazione dell’integrazione di traduzione {#creating-a-translation-integration-configuration}

Crea una configurazione del Translation Integration Framework per specificare come tradurre il contenuto. La configurazione include le seguenti informazioni:

* Quale fornitore di servizi di traduzione utilizzare.
* Se deve essere eseguita la traduzione umana o automatica.
* Se tradurre altri contenuti associati a una pagina o a una risorsa, ad esempio i tag.

Dopo aver creato una configurazione del framework, associa la configurazione cloud alle pagine che desideri tradurre. Quando il processo di traduzione viene avviato, il flusso di lavoro di traduzione procede in base alla configurazione del framework associato.

Quando diverse sezioni del sito Web hanno requisiti di traduzione diversi, crea di conseguenza configurazioni di framework multiple. Ad esempio, un sito web multilingue include copie in lingua inglese, spagnola e giapponese. Il proprietario del sito utilizza due diversi fornitori di servizi di traduzione per le versioni in spagnolo e giapponese. Pertanto, sono attive due configurazioni del framework. Ogni configurazione utilizza un provider di servizi di traduzione diverso.

Dopo aver configurato un Translation Integration Framework, puoi [associarlo alle pagine](/help/sites-administering/tc-prep.md) che lo usano.

**Nota:** per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md).

Una singola configurazione del framework controlla come tradurre il contenuto di una pagina e le risorse.
![chlimage_1-386](assets/translation-config-65.jpg)

### Proprietà di configurazione Sites {#sites-configuration-properties}

Le proprietà Sites controllano come viene eseguita la traduzione del contenuto della pagina.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Flusso di lavoro per traduzione</td>
   <td><p>Selezionare il metodo di traduzione eseguito dal framework per il contenuto del sito:</p>
    <ul>
     <li>Traduzione automatica: il provider di traduzione esegue la traduzione utilizzando la traduzione automatica in tempo reale.</li>
     <li>Traduzione umana: il contenuto viene inviato al provider di traduzione per essere tradotto dai traduttori. </li>
     <li>Non tradurre: il contenuto non viene inviato per la traduzione. Questo consente di saltare alcune parti di contenuto che non sarebbero tradotte, ma che potrebbero essere aggiornate con i contenuti più recenti.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provider traduzione</td>
   <td>Seleziona il provider di traduzione per eseguire la traduzione. Un provider viene visualizzato nell’elenco quando è installato il connettore corrispondente.</td>
  </tr>
  <tr>
   <td>Categoria contenuto</td>
   <td>(Solo traduzione automatica) Categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti.</td>
  </tr>
  <tr>
   <td>Traduci stringhe componenti</td>
   <td>Seleziona questa opzione per tradurre le stringhe dei componenti associati alla pagina.</td>
  </tr>
  <tr>
   <td>Traduci tag</td>
   <td>Seleziona per tradurre i tag associati alla pagina.</td>
  </tr>
  <tr>
   <td>Traduci risorse di pagina</td>
   <td><p>Seleziona la modalità di traduzione delle risorse aggiunte ai componenti dal file system o a cui si fa riferimento da Assets:</p>
    <ul>
     <li>Non tradurre: le risorse di pagina non vengono tradotte.</li>
     <li>Utilizzo del flusso di lavoro di traduzione dei siti: Assets viene gestito in base alle proprietà di configurazione nella scheda Sites.</li>
     <li>Utilizzo del flusso di lavoro di traduzione Assets: Assets viene gestito in base alla configurazione delle proprietà nella scheda Assets.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Esegui traduzione automatica</td>
   <td>Seleziona questa opzione per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Quando si seleziona questa opzione, non è possibile rivedere e modificare l’ambito del processo di traduzione.</td>
  </tr>
 </tbody>
</table>

### Proprietà di configurazione Assets {#assets-configuration-properties}

Le proprietà di Assets controllano la modalità di configurazione delle risorse. Per ulteriori informazioni sulla traduzione delle risorse, consulta [Creazione di copie per lingua per Assets](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Flusso di lavoro per traduzione</td>
   <td><p>Seleziona il tipo di traduzione eseguito dal framework per le risorse:</p>
    <ul>
     <li>Traduzione automatica: il provider di traduzione esegue la traduzione immediatamente utilizzando la traduzione automatica.</li>
     <li>Traduzione umana: il contenuto viene inviato automaticamente al provider di traduzione per essere tradotto manualmente. </li>
     <li>Non tradurre: Assets non viene inviato per la traduzione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provider traduzione</td>
   <td>Seleziona il provider di traduzione per eseguire la traduzione. Un provider viene visualizzato nell’elenco quando è installato il connettore corrispondente.</td>
  </tr>
  <tr>
   <td>Categoria contenuto</td>
   <td>(Solo traduzione automatica) Categoria che descrive il contenuto che si sta traducendo. La categoria può influenzare la scelta della terminologia e della formulazione durante la traduzione dei contenuti.</td>
  </tr>
  <tr>
   <td>Traduci risorse</td>
   <td>Seleziona questa opzione per includere le risorse nel progetto di traduzione. </td>
  </tr>
  <tr>
   <td>Traduci metadati</td>
   <td>Seleziona per tradurre i metadati della risorsa.</td>
  </tr>
  <tr>
   <td>Traduci tag</td>
   <td>Seleziona questa opzione per tradurre i tag associati alla risorsa.</td>
  </tr>
  <tr>
   <td>Esegui traduzione automatica</td>
   <td>Seleziona questa opzione per eseguire automaticamente i processi di traduzione dopo la creazione dei progetti di traduzione. Quando si seleziona questa opzione, non è possibile rivedere o modificare l’ambito del processo di traduzione.</td>
  </tr>
 </tbody>
</table>

1. Nella barra laterale, fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell’area Integrazione della traduzione, l’eventuale creazione di configurazioni determina quale collegamento viene visualizzato:

   * Se non è stata creata alcuna configurazione, fare clic su Configura ora.
   * Se le configurazioni esistono già, fai clic su Mostra configurazioni, quindi fai clic sul collegamento + che viene visualizzato accanto a Configurazioni disponibili.

1. Digita un nome per la configurazione, quindi fai clic su Crea.
1. Configura le proprietà nella scheda Sites e Assets, quindi fai clic su OK.

## Configurazione pagine per la traduzione {#configuring-pages-for-translation}

Per configurare la traduzione delle pagine sorgente in altre lingue, associa le pagine alle seguenti configurazioni cloud:

* La configurazione cloud che connette AEM al fornitore di traduzione.
* Il framework di integrazione della traduzione che configura i dettagli della traduzione.

La configurazione cloud del framework di integrazione della traduzione identifica la configurazione cloud da utilizzare per la connessione al provider di servizi. Quando si associa una pagina origine a una configurazione cloud del framework, la pagina deve essere associata alla configurazione cloud del fornitore del servizio utilizzato dalla configurazione cloud del framework.

Quando si associa una pagina a una configurazione cloud, i discendenti della pagina ereditano tale associazione. Ad esempio, se associ la pagina /content/geometrixx/en/products a un framework di integrazione della traduzione, la pagina Products e tutte le pagine sottostanti vengono tradotte in base al framework.

Se necessario, è possibile sovrascrivere tale associazione in una pagina discendente. Ad esempio, il contenuto di un sito web riguarda principalmente l’abbigliamento. Alcune pagine del sito sono tuttavia dedicate alla descrizione dell’azienda. La pagina principale del sito è associata a un framework di integrazione della traduzione che specifica la traduzione automatica utilizzando la categoria Abbigliamento. Il ramo che descrive l’azienda utilizza un framework che esegue la traduzione automatica utilizzando la categoria Generale.

### Associazione di una pagina a un fornitore di traduzione {#associating-a-page-with-a-translation-provider}

Associa una pagina al fornitore di traduzione utilizzato per tradurre tale pagina e le relative pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e fai clic su Visualizza proprietà.
1. Fai clic su Modifica, quindi sulla scheda Cloud Services.
1. Fai clic su Aggiungi configurazione > Integrazione della traduzione.
1. Seleziona il provider di traduzione da utilizzare, quindi fai clic su Fine.

### Associazione di pagine a un framework di integrazione della traduzione {#associating-pages-with-a-translation-integration-framework}

Associa una pagina a un framework di integrazione della traduzione che definisce come eseguire la traduzione della pagina e delle relative pagine discendenti.

1. Nella console Sites, seleziona la pagina da configurare e fai clic su Visualizza proprietà.
1. Fai clic su Modifica, quindi sulla scheda Cloud Services.
1. Fai clic su Aggiungi configurazione > Integrazione della traduzione.
1. Seleziona il framework di integrazione della traduzione da utilizzare, quindi fai clic su Fine.
