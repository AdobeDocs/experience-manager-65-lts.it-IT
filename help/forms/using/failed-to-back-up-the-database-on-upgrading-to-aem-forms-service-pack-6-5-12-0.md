---
title: Impossibile eseguire il backup del database durante l'aggiornamento a 6.5.12.0 per MySQL.
description: Quando un utente esegue l'aggiornamento ad Experience Manager 6.5.12.0 e fa clic su "Aggiorna MySQL", il gestore della configurazione non riesce a eseguire il backup del database Experience Manager Forms precedente.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Impossibile eseguire il backup del database durante l&#39;aggiornamento a 6.5.12.0 per MySQL {#issue}

Quando un utente esegue l&#39;aggiornamento ad Experience Manager 6.5.12.0 e fa clic su &quot;Aggiorna MySQL&quot;, il gestore della configurazione non riesce a eseguire il backup del database Experience Manager Forms precedente e viene visualizzato il messaggio di errore:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Si applica a {#applies-to}

* Experience Manager 6.5 Forms

## Soluzione {#solution}

Per risolvere il problema, aumentare il valore di max_packet_size del database a 100 M o come richiesto nel file my.ini che si trova in {AEM_HOME}/mysql.
