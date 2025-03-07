---
title: Aggiornare il tipo di licenza per la distribuzione
description: Aggiorna il tipo di licenza per la distribuzione utilizzando la pagina Modifica licenza nella console di amministrazione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 21f062c6-bb9a-4e18-9fb2-2bb7f0050c9c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Aggiornare il tipo di licenza per la distribuzione {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Come parte del processo di installazione di AEM Forms, è stato utilizzato Configuration Manager per configurare e distribuire i moduli di AEM Forms richiesti. Per impostazione predefinita, tali moduli sono configurati con una licenza di valutazione di 60 giorni. Utilizzare la pagina Modifica licenza nella console di amministrazione per modificare il tipo di licenza per la distribuzione. I moduli attualmente distribuiti vengono visualizzati nella pagina Modifica licenza.

Nella pagina Modifica licenza vengono visualizzate le informazioni sulla licenza:

* Tipo di licenza corrente
* Data e ora dell&#39;ultimo aggiornamento della licenza
* Chi ha eseguito l’ultimo aggiornamento
* Stato corrente della licenza
* Data di installazione di AEM Forms
* Data di scadenza della licenza corrente

>[!NOTE]
>
>La modifica della licenza si applica a tutti i moduli distribuiti. Prima di modificare il tipo di licenza, annullare la distribuzione dei moduli non concessi in licenza. Non selezionare il tipo di licenza Produzione se l’elenco dei moduli distribuiti contiene moduli diversi da quelli acquistati da Adobe.

## Aggiornare il tipo di licenza {#update-the-license-type}

1. Nella console di amministrazione, fare clic su Gestione licenze.
1. Leggere il contratto di licenza con l&#39;utente finale di AEM Forms, selezionare Accetto se si accettano i termini del contratto e quindi fare clic su Avanti.
1. Nella pagina Modifica licenza selezionare un tipo di licenza:

   * **EVAL:** licenza di valutazione di 60 giorni
   * **DEV:** Licenza di sviluppo permanente
   * **NFR:** licenza di valutazione biennale
   * **IDEV:** abbonamento di 1 anno al programma Adobe Developer
   * **Produzione:** licenza perpetua

1. Seleziona Sì, La Modifica Della Licenza È Valida Per Tutti I Moduli Distribuiti.
1. Fare clic su Conferma modifica licenza. Viene visualizzato un messaggio che informa che la licenza è stata aggiornata correttamente.
