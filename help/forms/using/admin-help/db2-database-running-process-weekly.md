---
title: 'DB2&reg; database: esecuzione settimanale di un processo'
description: Scopri come migliorare le prestazioni del database AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Database DB2®: esecuzione settimanale di un processo{#db-database-running-a-process-weekly}

Se il database AEM Forms DB2® inizia a funzionare lentamente, l&#39;esecuzione settimanale del seguente processo può migliorare le prestazioni:

1. Avvia Centro controllo DB2®:

   (Windows) Selezionare Start > Programmi > IBM® DB2® > Strumenti di amministrazione generali > Centro di controllo.

   (Linux® e UNIX®) Dal prompt dei comandi digitare il comando `db2jcc`.

1. Nell&#39;albero degli oggetti di DB2® Control Center fare clic su Tutti i database.
1. Fare clic sul database creato per AEM Forms e quindi sulla cartella Tabelle.
1. Selezionare tutte le tabelle di database nel riquadro dei contenuti, fare clic con il pulsante destro del mouse su di esse, quindi selezionare Esegui statistiche.
1. Vai a Statistiche > Statistiche indice.
1. Selezionare Raccogli statistiche per tutti gli indici, selezionare Raccogli statistiche per gli indici con statistiche dettagliate estese e quindi fare clic su OK.

Al termine del processo viene visualizzato un messaggio. Chiudi il messaggio.
