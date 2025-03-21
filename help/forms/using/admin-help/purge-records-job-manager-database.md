---
title: Eliminare i record dal database di Gestione processi
description: I dati di processo di grandi dimensioni possono comportare prestazioni inferiori per i moduli AEM. È buona prassi eliminare i dati del processo quando i record non sono più necessari.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a5e6b09a-c4c7-41c0-8221-d563cb74b3b7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Eliminare i record dal database di Gestione processi {#purge-records-from-the-job-manager-database}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona prassi eliminare i dati del processo quando i record non sono più necessari.

È possibile utilizzare la console di amministrazione per eseguire una rimozione una tantum di record obsoleti o per pianificare eliminazioni automatiche regolari. Altri metodi per eliminare i record obsoleti sono descritti in [Rimozione dei dati del processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accedere alla pagina Utilità di pianificazione rimozione processi**

1. In Administration Console, fare clic su Health Monitor nell&#39;angolo superiore destro della pagina.
1. Fare clic sulla scheda Pianificazione rimozione job.

Le informazioni sulle rimozioni attualmente pianificate vengono visualizzate nella casella Informazioni modulo di pianificazione rimozione OdL.

>[!NOTE]
>
>Facendo clic su Interrompi modulo di pianificazione vengono interrotte le rimozioni pianificate in futuro, ma non viene interrotto un processo di rimozione già in corso.

**Pianifica un&#39;eliminazione una tantum**

1. Selezionare Solo una volta.
1. Nell&#39;area Filtro record completati rimozione specificare il numero di giorni o settimane dopo le quali un record viene considerato obsoleto e pronto per la rimozione.

   >[!NOTE]
   >
   >I record relativi a processi non completati non vengono eliminati, anche se sono più vecchi della data specificata.

1. Specifica quando avverrà l’eliminazione. Selezionare la casella di controllo Usa data e ora corrente oppure deselezionarla e fare clic sulle icone del calendario e dell&#39;orologio per specificare la data e l&#39;ora in cui verrà eseguita la rimozione.

   >[!NOTE]
   >
   >Se si specifica una data e un&#39;ora di inizio nel passato, la rimozione viene eseguita immediatamente quando si fa clic su Avvia modulo di pianificazione.

1. Fare clic su Avvia modulo di pianificazione. Tutte le impostazioni pianificate in precedenza vengono sostituite con le nuove impostazioni.

**Configurare una pianificazione di eliminazione automatica**

1. Selezionare Ripeti ogni e specificare il numero di giorni o settimane tra le eliminazioni.
1. Nell&#39;area Filtro record completati rimozione specificare il numero di giorni o settimane dopo le quali un record viene considerato obsoleto e pronto per la rimozione. Impossibile impostare il valore su `0`.

   >[!NOTE]
   >
   >I record relativi a processi non completati non vengono eliminati, anche se sono più vecchi della data specificata.

1. Specifica quando inizieranno le eliminazioni. Selezionare la casella di controllo Usa data e ora corrente oppure deselezionarla e fare clic sulle icone del calendario e dell&#39;orologio per specificare la data e l&#39;ora in cui verrà eseguita la rimozione.

   >[!NOTE]
   >
   >Se si specificano una data e un&#39;ora di inizio nel passato, AEM Form calcola la data di inizio successiva logica in base alla data specificata. Ad esempio, se si pianifica che le eliminazioni del processo avvengano settimanalmente a partire dal 7 aprile e ora è il 9 aprile, la prima eliminazione avviene il 14 aprile.

1. Fare clic su Avvia modulo di pianificazione. Tutte le impostazioni pianificate in precedenza vengono sostituite con le nuove impostazioni.
