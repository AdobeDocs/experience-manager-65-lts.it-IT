---
title: Integrazione della soluzione Create Correspondence con il tuo portale personalizzato
description: Scopri come integrare l’interfaccia utente per la creazione di corrispondenza con il portale personalizzato
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 496b125b-b091-4843-ba9f-2479dbeba07b
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 4%
---
# Integrazione della soluzione `Create Correspondence` con il portale personalizzato{#integrating-create-correspondence-ui-with-your-custom-portal}

## Panoramica {#overview}

In questo articolo viene descritto come integrare la soluzione `Create Correspondence` con l&#39;ambiente.

## Chiamata basata su URL {#url-based-invocation}

Un modo per chiamare l&#39;applicazione `Create Correspondence` da un portale personalizzato consiste nel preparare l&#39;URL con i seguenti parametri di richiesta:

* l’identificatore per il modello di lettera (utilizzando il parametro cmLetterId).

* URL dei dati XML recuperati dall&#39;origine dati desiderata (utilizzando il parametro cmDataUrl).

Ad esempio, il portale personalizzato prepara l’URL come\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, che potrebbe essere il href da un collegamento sul portale.

>[!NOTE]
>
>Una chiamata di questo tipo non è sicura in quanto i parametri necessari vengono passati come richiesta GET esponendo lo stesso (chiaramente visibile) nell’URL.

>[!NOTE]
>
>Prima di chiamare l&#39;applicazione `Create Correspondence`, salvare e caricare i dati per chiamare l&#39;interfaccia utente `Create Correspondence` in corrispondenza dell&#39;URL dati specificato. Questo processo può essere eseguito direttamente dal portale personalizzato o tramite un altro processo back-end.

## Chiamata basata su dati in linea {#inline-data-based-invocation}

Un altro modo più sicuro per chiamare l&#39;applicazione `Create Correspondence` consiste nell&#39;accedere all&#39;URL all&#39;indirizzo https://&#39;[server]:[porta]&#39;/[contextPath]/aem/forms/createcorrespondence.html. Eseguire questo URL durante l&#39;invio di parametri e dati per chiamare l&#39;applicazione `Create Correspondence` come richiesta POST, nascondendoli all&#39;utente finale. Questo flusso di lavoro consente inoltre di passare i dati XML per l&#39;applicazione `Create Correspondence` in linea (come parte della stessa richiesta, utilizzando il parametro `cmData`). Questo flusso di lavoro non era possibile o ideale nell’approccio precedente.

### Parametri per specificare la lettera {#parameters-for-specifying-letter}

| **Nome** | **Tipo** | **Descrizione** |
| --- | --- | --- |
| cmLetterInstanceId | Stringa | Identificatore per l’istanza della lettera. |
| cmLetterId | Stringa | Nome del modello Lettera. |

L&#39;ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per il caricamento della lettera.

### Parametri per specificare l&#39;origine dati XML {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descrizione</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>Dati XML da un file di origine utilizzando protocolli di base quali cq, ftp, http o file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Stringa</td> 
   <td>Utilizzo dei dati XML disponibili nell'istanza della lettera.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Per riutilizzare i dati di test allegati in un dizionario dati.</td> 
  </tr>
 </tbody>
</table>

L&#39;ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per il caricamento dei dati XML.

### Altri parametri {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descrizione</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Booleano</td> 
   <td>True per aprire la lettera in modalità anteprima<br /> </td> 
  </tr>
  <tr>
   <td>Casuale</td> 
   <td>Marca temporale</td> 
   <td>Per risolvere i problemi di memorizzazione nella cache del browser.</td> 
  </tr>
 </tbody>
</table>

Se si utilizza il protocollo http o cq per `cmDataURL`, l&#39;URL di `http/cq` deve essere accessibile in modo anonimo.
