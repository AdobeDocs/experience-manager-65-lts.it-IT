---
title: Best practice per gli sviluppatori di AEM
description: I team tecnici e di consulenza di Adobe hanno sviluppato un set completo di best practice per sviluppatori AEM.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: fc2aa62a-3fc4-491d-aff5-74896998d7d6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%

---

# Best practice{#best-practices}

## Procedure consigliate per gli sviluppatori - Guida introduttiva {#best-practices-for-developers-getting-started}

I team tecnici e di consulenza di Adobe hanno sviluppato un set completo di best practice per sviluppatori AEM. Gli sviluppatori di Adobe si attengono a queste best practice durante lo sviluppo di aggiornamenti di base dei prodotti AEM e del codice cliente per le implementazioni dei clienti.

Prima di iniziare il progetto di sviluppo AEM, rivedi le best practice:

* [Procedure di sviluppo](/help/sites-developing/development-practices.md)
* [Architettura dei contenuti](/help/sites-developing/content-architecture.md)
* [Architettura software](/help/sites-developing/software-architecture.md)
* [Suggerimenti per la codifica](/help/sites-developing/coding-tips.md)
* [Insidie del codice](/help/sites-developing/code-pitfalls.md)
* [Interazione JCR](/help/sites-developing/jcr-integration.md)
* [Bundle OSGi](/help/sites-developing/osgi-bundles.md)
* [Best practice per le API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informazioni aggiuntive sulle best practice {#additional-best-practices-information}

Nelle seguenti aree è disponibile una documentazione specifica per lo sviluppo di best practice:

* [Sites](#sites)
* [Strumenti/HTL](#tooling-htl)

I documenti specifici sono descritti e collegati nelle tabelle seguenti.

Per le best practice sull’amministrazione, la distribuzione e la manutenzione o l’authoring, consulta una delle seguenti sezioni:

* [Amministrazione delle best practice](/help/sites-administering/administer-best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)
* [Implementazione delle best practice](/help/sites-deploying/best-practices.md)

## Sites {#sites}

Per la gestione e l’authoring dei contenuti del sito web, vengono descritte alcune best practice:

<table>
 <tbody>
  <tr>
   <td>Alcune delle teorie alla base dell’interfaccia utente standard touch.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Interfaccia touch: concetti</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Interfaccia touch: struttura</a></p> </td>
   <td>Questi documenti forniscono una panoramica dei concetti e della struttura dell’interfaccia touch.</td>
  </tr>
  <tr>
   <td>Interfaccia touch: personalizzazione delle console </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalizzazione delle console dell’interfaccia touch</a></td>
   <td>Questo documento descrive il modo migliore per estendere le console per l’interfaccia utente touch.</td>
  </tr>
  <tr>
   <td>Interfaccia touch: personalizzazione dell’authoring delle pagine</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalizzazione dell’authoring delle pagine dell’interfaccia utente touch</a></td>
   <td>Descrive come estendere l’authoring delle pagine per l’interfaccia utente touch.</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Sviluppo ed estensione dei flussi di lavoro</a></td>
   <td><p>I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM) e possono rappresentare una grande quantità di elaborazione che si verifica in un ambiente AEM, pertanto si consiglia vivamente di pianificare con attenzione le implementazioni dei flussi di lavoro.</p> </td>
  </tr>
 </tbody>
</table>

## Strumenti/HTL {#tooling-htl}

HTML Template Language (HTL) è un nuovo sistema di modelli di HTML, introdotto con AEM 6.0. Sostituisce JSP ed ESP come sistema di modelli preferito di AEM.

|  |  |  |
|---|---|---|
| Panoramica di HTL | [Panoramica e sintassi HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it) | Questo documento descrive cosa è HTL, come passare ad HTL, un progetto di esempio, la sintassi, le espressioni e le istruzioni |
| Utilizzo dell’API in Java | [API di utilizzo Java HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | Java Use-API per HTL consente a un file HTL di accedere a metodi helper in una classe Java personalizzata. |

>[!NOTE]
>
>Il seguente tutorial in più parti potrebbe essere utile per la best practice per impostare un nuovo progetto AEM, con informazioni dettagliate sui Componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti:
>[Guida introduttiva ad AEM Sites - Esercitazione WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
