---
title: Risoluzione dei problemi di Adobe Experience Manager
description: Scopri come risolvere alcuni problemi che potrebbero verificarsi con Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 802130c3-9cb8-46b7-98c2-fd9e83d18ec3
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---

# Risoluzione dei problemi di Adobe Experience Manager {#troubleshooting-aem}

Nella sezione seguente vengono descritti alcuni problemi che possono verificarsi durante l’utilizzo di AEM (Adobe Experience Manager) e vengono proposte possibili soluzioni.

>[!NOTE]
>
>Se stai risolvendo problemi di authoring in AEM, consulta [Risoluzione dei problemi per gli autori.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>In caso di problemi, vale la pena controllare anche l&#39;elenco di [problemi noti](/help/release-notes/release-notes.md) per la tua istanza (pacchetti di versioni e service pack).

## Risoluzione dei problemi relativi agli amministratori {#troubleshooting-scenarios-for-administrators}

La tabella seguente fornisce una panoramica dei problemi che gli amministratori possono risolvere:

<table>
 <tbody>
  <tr>
   <td><strong>Ruolo</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Amministratore di sistema</td>
   <td><p>Se si fa doppio clic sul file jar Quickstart, questo non ha alcun effetto o il file jar viene aperto con un altro programma (ad esempio, Archive Manager)</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> </td>
   <td><p>La mia applicazione in esecuzione su CRX genera errori di memoria insufficiente</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> </td>
   <td><p>La schermata iniziale di AEM non viene visualizzata nel browser dopo aver fatto doppio clic su AEM CM Quickstart</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> <p>utente amministratore</p> </td>
   <td><p>Creazione di un'immagine thread</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> <p>utente amministratore</p> </td>
   <td><p>Verifica di sessioni JCR non chiuse</p> </td>
  </tr>
 </tbody>
</table>


## Metodi per la risoluzione dei problemi di analisi {#methods-for-troubleshooting-analysis}

### Creazione di un&#39;immagine thread {#making-a-thread-dump}

L’immagine thread è un elenco di tutti i thread Java™ attualmente attivi. Se AEM non risponde correttamente, l’immagine thread può aiutarti a identificare deadlock o altri problemi.

### Utilizzo di Sling Thread Dumper {#using-sling-thread-dumper}

1. Apri la **console Web AEM**, ad esempio in `https://localhost:4502/system/console/`.
1. Selezionare la scheda **Threads** in **Stato**.

![schermata_shot_2012-02-13alle43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utilizzo di jstack (riga di comando) {#using-jstack-command-line}

1. Trova il PID (ID processo) dell’istanza Java™ di AEM.

   È possibile, ad esempio, utilizzare `ps -ef` o `jps`.

1. Esegui:

   `jstack <pid>`

1. Mostra l’immagine thread.

>[!NOTE]
>
>È possibile aggiungere le immagini thread a un file di registro utilizzando il reindirizzamento di output `>>`:
>
>`jstack <pid> >> /path/to/logfile.log`

Per ulteriori informazioni, consulta la [documentazione su come estrarre immagini thread da una JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=it)

### Verifica di sessioni JCR non chiuse {#checking-for-unclosed-jcr-sessions}

Quando viene sviluppata la funzionalità per AEM WCM, è possibile aprire le sessioni JCR (operazione paragonabile all’apertura di una connessione a un database). Se le sessioni aperte non vengono mai chiuse, il sistema potrebbe presentare i seguenti sintomi:

* Il sistema diventa più lento.
* È possibile visualizzare gran parte di CacheManager: resizeAll voci nel file di registro; il seguente numero (size=&lt;x>) mostra il numero di cache, ogni sessione apre diverse cache.
* Di tanto in tanto il sistema esaurisce la memoria (dopo alcune ore, giorni o settimane, a seconda della gravità).

Per avviare l&#39;analisi delle sessioni non chiuse, vedere l&#39;articolo della Knowledge Base [Risolutore risorse non chiuso](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23761).

### Utilizzo della console Web di Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

Lo stato dei bundle OSGi può anche fornire un’indicazione anticipata di possibili problemi.

1. Apri la **console Web AEM**, ad esempio in `https://localhost:4502/system/console/`.
1. Seleziona **Bundle** nella scheda **OSGI**.
1. Seleziona:

   * lo stato dei bundle. In caso contrario, prova ad arrestare e riavviare il bundle. Se il problema persiste, approfondisci ulteriormente utilizzando altri metodi.
   * se uno dei bundle presenta dipendenze mancanti. Per visualizzare tali dettagli, fai clic sul nome del singolo bundle, che è un collegamento (il seguente esempio non presenta alcun problema):

![schermata_shot_2012-02-13alle44706pm](assets/screen_shot_2012-02-13at44706pm.png)
