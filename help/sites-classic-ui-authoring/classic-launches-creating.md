---
title: Creazione dei lanci
description: Crea un lancio per abilitare l’aggiornamento di una nuova versione delle pagine web esistenti per l’attivazione futura. Quando crei un lancio, specifichi un titolo e la pagina sorgente.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 02fd32c8-7def-45d4-ba3b-d4cb346f5103
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 55%

---

# Creazione dei lanci{#creating-launches}

Crea un lancio per abilitare l’aggiornamento di una nuova versione delle pagine web esistenti per l’attivazione futura. Per creare un lancio, è necessario specificare un titolo e la pagina di origine:

* Il titolo viene visualizzato in **Sidekick**, da cui gli autori possono accedere per lavorarci.
* Per impostazione predefinita, le pagine secondarie della pagina sorgente sono incluse nel lancio. Se necessario, puoi utilizzare solo la pagina sorgente.
* Per impostazione predefinita, [Live Copy](/help/sites-administering/msm.md) aggiorna automaticamente le pagine del lancio durante il cambio delle pagine sorgente. È possibile specificare di creare una copia statica per impedire modifiche automatiche.

Facoltativamente, puoi specificare la **Data lancio** (e l’ora) per definire quando promuovere e attivare le pagine del lancio. Tuttavia, la **Data lancio** funziona solo in combinazione con il flag **Production Ready** (vedi la sezione [Modifica di una configurazione di lancio](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)). Affinché le azioni vengano effettivamente eseguite in automatico, è necessario impostare entrambe.

## Creazione di un lancio {#creating-a-launch}

La procedura seguente crea un lancio.

1. Aprire la pagina Amministrazione sito Web ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Fai clic su **Nuovo...** e quindi su **Nuovo lancio...**.
1. Nella finestra di dialogo **Crea lancio**, specifica i valori per le seguenti proprietà:

   * **Titolo lancio**: il nome del lancio. Il nome deve essere significativo per gli autori.
   * **Pagina Source**: il percorso della pagina per cui creare il lancio. Per impostazione predefinita, sono incluse tutte le pagine figlie.
   * **Escludi sottopagine**: selezionare questa opzione per creare il lancio solo per la pagina di origine e non per le pagine figlie. Per impostazione predefinita, questa opzione non è selezionata.
   * **Mantieni in sincronia**: selezionare questa opzione per aggiornare automaticamente il contenuto delle pagine di lancio quando cambiano le pagine di origine. Ciò si ottiene rendendo il lancio una [Live Copy](/help/sites-administering/msm.md).
   * **Data lancio**: la data e l&#39;ora in cui la copia del lancio deve essere attivata (in base alla segnalazione **Produzione pronta**; consulta [Lanci: l&#39;ordine degli eventi](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Fai clic su **Crea**.

## Eliminazione di un lancio {#deleting-a-launch}

Puoi anche eliminare un lancio.

1. Nella console [Launches](/help/sites-classic-ui-authoring/classic-launches.md), seleziona il lancio richiesto.
1. Fai clic su **Elimina**. È necessaria la conferma:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Quando elimini i lanci nidificati, devi prima eliminare i livelli inferiori.
