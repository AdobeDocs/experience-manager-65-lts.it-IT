---
title: Rimozione dati processo
description: I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. Scopri come eliminare i dati del processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 53ce63a3-704a-4da6-b652-362a436f05a7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Rimozione dati processo {#purging-process-data}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona prassi eliminare i dati del processo quando i record non sono più necessari. AEM Forms fornisce diversi metodi per eliminare i dati del processo:

* È possibile utilizzare la console di amministrazione per eseguire una rimozione unica dei record obsoleti correlati a processi di lunga durata o per pianificare eliminazioni automatiche regolari. (Vedi [Eliminare i record dal database di Gestione processi](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* È possibile utilizzare l’API Java e l’API del servizio web di AEM Forms per eliminare a livello di programmazione i dati di processo relativi ai processi di lunga durata. (Vedi &quot;Rimozione dei dati del processo&quot; in [Programmazione con AEM forms](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Utilizzare lo strumento di rimozione del processo per eliminare i processi in base al nome del processo e ad altri parametri. Per informazioni dettagliate, vedere il file readme dello strumento di eliminazione dei processi, nella directory principale di *[aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
