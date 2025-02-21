---
title: Implementazione delle best practice
description: Scopri come distribuire e gestire Adobe Experience Manager (AEM) nel modo più efficiente ed efficace possibile.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: ac26c0163309b6cb6c0cfde2098a8cc05955d03f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---

# Implementazione delle best practice{#deploying-best-practices}

Le best practice per l’implementazione descrivono come distribuire o gestire Adobe Experience Manager (AEM) nel modo più efficiente ed efficace possibile. Questo elenco crescente di argomenti include diverse aree in AEM.

Nelle seguenti aree è disponibile la documentazione relativa all’implementazione e alla manutenzione delle best practice e delle raccomandazioni:

* [Oak](#oak)
* [Interfaccia](#ui)
* [Prestazioni](#performance)

Per le best practice sull’amministrazione, lo sviluppo o l’authoring, consulta una delle seguenti sezioni:

* [Amministrazione delle best practice](/help/sites-administering/administer-best-practices.md)
* [Sviluppo di best practice](/help/sites-developing/best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)

I documenti specifici sono descritti e collegati nelle tabelle seguenti.

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) è un archivio di contenuti gerarchici scalabile ed efficiente alla base di AEM.

<table>
 <tbody>
  <tr>
   <td><p>Scalabilità, prestazioni e disaster recovery</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Prestazioni e scalabilità</a></td>
   <td>Un white paper che illustra l'agilità tecnica, le prestazioni elevate e le funzionalità di disaster recovery</td>
  </tr>
  <tr>
   <td>Distribuzioni consigliate di Oak</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Distribuzioni consigliate</a></td>
   <td>Descrive gli scenari di distribuzione</td>
  </tr>
  <tr>
   <td>Topologia di Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Best practice per la topologia Mongo</a></td>
   <td>Descrive la topologia mongo - quando utilizzare quale topologia.</td>
  </tr>
  <tr>
   <td>Opzioni archivio dati</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configurazione di nodi e archivi dati</a></td>
   <td>In questo documento vengono illustrate le best practice per l’archiviazione di dati binari e nodi di contenuto. Include informazioni sull’utilizzo dell’archivio dati Amazon S3.</td>
  </tr>
  <tr>
   <td>Cerca in Oak</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Procedure consigliate per query e indicizzazione</a><br /> </td>
   <td>Vengono descritte le procedure consigliate per l'indicizzazione del contenuto.</td>
  </tr>
 </tbody>
</table>

## Interfaccia {#ui}

Le best practice relative all’interfaccia utente sono descritte qui:

[Raccomandazioni in merito all’interfaccia utente per clienti](/help/sites-deploying/ui-recommendations.md)

AEM dispone attualmente di due interfacce: classica e touch nella stessa versione. Pertanto, i clienti devono prendere una decisione su quale utilizzare durante l’implementazione del progetto. Questo documento ha lo scopo di aiutare a trovare la scelta giusta.

## Prestazioni {#performance}

Le best practice sulle prestazioni sono elencate qui:

<table>
 <tbody>
  <tr>
   <td>Best practice per Assurance di qualità</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Best practice per Assurance di qualità</a></td>
   <td>Panoramica standardizzata dei problemi relativi alla definizione di un concetto di test specifico per i test delle prestazioni nell'ambiente <em>publish</em>. Questo è di interesse soprattutto per gli ingegneri QA, i project manager e gli amministratori di sistema.</td>
  </tr>
  <tr>
   <td>Utilizzo di Dispatcher con una rete CDN</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilizzo di Dispatcher con una rete CDN</a></td>
   <td>Una rete CDN (Content Delivery Network), come Akamai Edge Delivery o Amazon Cloud Front, consente di distribuire contenuto da una posizione vicina all’utente finale.</td>
  </tr>
  <tr>
   <td>Ottimizzazione delle prestazioni</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Ottimizzazione delle prestazioni</a></td>
   <td>Un problema chiave è il tempo impiegato dal sito web per rispondere alle richieste dei visitatori.</td>
  </tr>
  <tr>
   <td>Test delle prestazioni</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Best practice per i test delle prestazioni</a></td>
   <td>Descrive le best practice per l'esecuzione di test delle prestazioni in una distribuzione AEM.<br /> </td>
  </tr>
 </tbody>
</table>
