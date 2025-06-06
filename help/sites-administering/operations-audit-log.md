---
title: Manutenzione del registro di controllo in AEM 6
description: Scopri come gestire i registri di audit in Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
feature: Operations
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: dd0f90f7-5e92-49d3-a5b4-17d99ed927b9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---

# Manutenzione del registro di controllo in AEM 6{#audit-log-maintenance-in-aem}

Gli eventi AEM idonei per la registrazione di audit generano molti dati archiviati. Questi dati possono crescere rapidamente nel tempo a causa di repliche, caricamenti di risorse e altre attività del sistema.

La manutenzione dei registri di controllo include diverse parti di funzionalità che consentono di automatizzare la manutenzione dei registri di controllo in base a criteri specifici.

Viene implementato come attività di manutenzione settimanale configurabile ed è accessibile tramite la console di monitoraggio della dashboard operazioni.

Per ulteriori informazioni, vedere la [documentazione del dashboard operazioni](/help/sites-administering/operations-dashboard.md).

Esistono tre tipi di opzioni di eliminazione del log di controllo:

1. [Eliminazione registro di controllo pagina](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Rimozione registro di controllo DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Esecuzione del log di controllo della replica](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Ciascuno può essere configurato creando regole nella console web di AEM. Dopo averli configurati, puoi attivarli passando a **Strumenti - Operazioni - Manutenzione - Finestra manutenzione settimanale** ed eseguendo l&#39;**Attività di manutenzione del registro di controllo**.

## Configurare la rimozione del registro di controllo della pagina {#configure-page-audit-log-purging}

Per configurare la rimozione del registro di controllo, effettua le seguenti operazioni:

1. Passare all&#39;amministratore della console Web puntando il browser su `http://localhost:4502/system/console/configMgr/`

1. Cercare un elemento denominato **Regola rimozione registro di controllo pagine** e fare clic su di esso.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Quindi, configurare il modulo di pianificazione della rimozione in base alle proprie esigenze. Opzioni disponibili:

   * **Nome regola:** il nome della regola dei criteri di controllo;
   * **Percorso contenuto:** il percorso del contenuto a cui verrà applicata la regola;
   * **Età minima:** il numero di giorni in cui i registri di audit devono essere conservati;
   * **Tipo di registro di controllo:** il tipo di registro di controllo da eliminare.

   >[!NOTE]
   >
   >Il percorso del contenuto si applica solo agli elementi figlio del nodo `/var/audit/com.day.cq.wcm.core.page` nell&#39;archivio.

1. Salva la regola.
1. Per poter essere eseguita, la regola creata deve essere esposta nel dashboard operazioni. Per eseguire questa operazione, vai a **Strumenti - Operazioni - Manutenzione** dalla schermata iniziale di AEM.

1. Premere la scheda **Finestra manutenzione settimanale**.

1. L&#39;attività di manutenzione è già presente nella scheda **Attività di manutenzione del registro di controllo**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. È possibile controllare la data dell&#39;esecuzione successiva, configurarla o eseguirla manualmente premendo il pulsante di riproduzione.

In AEM 6.3, se la finestra di manutenzione programmata si chiude prima che l’attività di rimozione del registro di controllo possa essere completata, l’attività si interrompe automaticamente. L&#39;operazione riprenderà all&#39;apertura della finestra di manutenzione successiva.

**Con AEM 6.5**, puoi interrompere manualmente un&#39;attività di eliminazione del registro di controllo facendo clic sull&#39;icona **Interrompi**. Alla successiva esecuzione l’attività riprenderà in modo sicuro.

>[!NOTE]
>
>Interrompere l&#39;attività di manutenzione significa sospenderne l&#39;esecuzione senza perdere la traccia del processo già in corso.

## Configurare la rimozione del registro di controllo DAM {#configure-dam-audit-log-purging}

1. Passa alla console di sistema all&#39;indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca la regola **Rimozione registro di controllo DAM** e fai clic sul risultato.
1. Nella finestra successiva, configura la regola di conseguenza. Le opzioni sono:

   * **Nome regola:** il nome della regola dei criteri di controllo;
   * **Percorso contenuto:** il percorso del contenuto a cui verrà applicata la regola
   * **Età minima:** il numero di giorni in cui i registri di audit devono essere conservati
   * **Tipi di eventi Dam del registro di controllo:** i tipi di eventi di controllo DAM che devono essere eliminati.

1. Fai clic su **Salva** per salvare la configurazione

## Configurare la rimozione del registro di controllo della replica  {#configure-replication-audit-log-purging}

1. Passa alla console di sistema all&#39;indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca **Utilità di pianificazione eliminazione log di controllo replica** e fai clic sul risultato
1. Nella finestra successiva, configura la regola di conseguenza. Le opzioni sono:

   * **Nome regola:** il nome della regola dei criteri di controllo
   * **Percorso contenuto:** il percorso del contenuto a cui verrà applicata la regola
   * **Età minima:** il numero di giorni in cui i registri di audit devono essere conservati
   * **Tipi di eventi di replica del registro di controllo:** i tipi di eventi di controllo della replica da eliminare

1. Fai clic su **Salva** per salvare la configurazione.
