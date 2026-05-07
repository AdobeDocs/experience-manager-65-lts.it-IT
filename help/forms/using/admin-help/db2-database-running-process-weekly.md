---
title: 'Database DB2&reg;: esecuzione settimanale di un processo'
description: Scopri come migliorare le prestazioni del tuo database AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: e8cf9e73-345c-4dea-8361-b678c1a3cd1b
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 85%

---

# Database DB2®: esecuzione settimanale di un processo{#db-database-running-a-process-weekly}

Se il database DB2® di AEM Forms inizia a funzionare lentamente, l’esecuzione settimanale del seguente processo può migliorare le prestazioni:

1. Avviare il Centro controllo DB2®:

   (Windows) Seleziona Start > Programmi > IBM® DB2® > Strumenti di amministrazione generale > Centro di controllo.

   (Linux® e UNIX®) Dal prompt dei comandi digita il comando `db2jcc`.

1. Nella struttura degli oggetti del Centro di controllo DB2®, fai clic su Tutti i database.
1. Fai clic sul database creato per AEM Forms e quindi sulla cartella Tabelle.
1. Seleziona tutte le tabelle di database nel riquadro dei contenuti, fai clic con il pulsante destro del mouse su di esse, quindi seleziona Esegui statistiche.
1. Passa a Statistiche > Statistiche indice.
1. Seleziona Raccogli statistiche per tutti gli indici, seleziona Raccogli statistiche per gli indici con statistiche dettagliate estese e quindi fai clic su OK.

Al termine del processo viene visualizzato un messaggio. Chiudi il messaggio.
