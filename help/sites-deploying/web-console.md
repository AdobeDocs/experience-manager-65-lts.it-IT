---
title: Console web in Adobe Experience Manager
description: Scopri come utilizzare la console web Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 55d4f34c-6766-48b7-86a1-689901e8871f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 1%

---

# Console Web{#web-console}

La console Web in Adobe Experience Manager (AEM) è basata sulla [console di gestione Web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix è uno sforzo della community per implementare la piattaforma di servizio OSGi R4, che include il framework OSGi e i servizi standard.

>[!NOTE]
>
>Nella console Web, tutte le descrizioni che menzionano le impostazioni predefinite si riferiscono alle impostazioni predefinite di Sling.
>
>AEM dispone di proprie impostazioni predefinite; pertanto, le impostazioni predefinite potrebbero essere diverse da quelle documentate nella console.

La console Web offre una selezione di schede per la gestione dei bundle OSGi, tra cui:

* [Configurazione](#configuration): utilizzato per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare i parametri di sistema di AEM
* [Bundle](#bundles): utilizzati per l&#39;installazione dei bundle
* [Componenti](#components): utilizzati per controllare lo stato dei componenti necessari per AEM

Tutte le modifiche apportate vengono immediatamente applicate al sistema in esecuzione. Non è richiesto alcun riavvio.

È possibile accedere alla console da `../system/console`, ad esempio:

`http://localhost:4502/system/console/components`

## Configurazione {#configuration}

La scheda **Configurazione** viene utilizzata per configurare i bundle OSGi ed è pertanto il meccanismo sottostante per configurare i parametri di sistema di AEM.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Configurazione OSGi con la console Web](/help/sites-deploying/configuring-osgi.md).

È possibile accedere alla scheda **Configurazione** da:

* Il menu a discesa:

  **OSGi >**

* L’URL; ad esempio:

  `http://localhost:4502/system/console/configMgr`

Viene visualizzato un elenco di configurazioni:

![schermata_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Esistono due tipi di configurazioni disponibili dagli elenchi a discesa in questa schermata:

* **Configurazioni**
Consente di aggiornare le configurazioni esistenti. Hanno un’identità persistente (PID) e possono essere:

   * standard e integrale per AEM; questi sono richiesti, se eliminati i valori tornano alle impostazioni predefinite.
   * istanze create da Configurazioni di fabbrica; queste istanze vengono create dall&#39;utente; l&#39;eliminazione rimuove l&#39;istanza.

* **Configurazioni factory**
Consente di creare un&#39;istanza dell&#39;oggetto funzionalità richiesto.

  Viene allocata a un’identità persistente e quindi elencata nell’elenco a discesa Configurazioni.

Selezionando una voce dall’elenco vengono visualizzati i parametri relativi a tale configurazione:

![chlimage_1-21](assets/chlimage_1-21a.png)

Puoi quindi aggiornare i parametri come richiesto e:

* **Salva**

  Salva le modifiche apportate.

  Per una configurazione di fabbrica, viene creata un&#39;istanza con un&#39;identità persistente. La nuova istanza viene quindi elencata in Configurazioni.

* **Reimposta**

  Ripristina i parametri mostrati sullo schermo agli ultimi salvati.

* **Elimina**

  Elimina la configurazione corrente. Se standard, i parametri vengono ripristinati alle impostazioni predefinite. Se viene creata da una configurazione di fabbrica, l&#39;istanza specifica viene eliminata.

* **Annulla associazione**

  Separa la configurazione corrente dal bundle.

* **Annulla**

  Annulla le modifiche correnti.

## Bundle {#bundles}

La scheda **Bundle** è il meccanismo per installare i bundle OSGi necessari per AEM. È possibile accedere alla scheda utilizzando uno dei metodi seguenti:

* Il menu a discesa:

  **OSGi >**

* L’URL; ad esempio:

  `http://localhost:4502/system/console/bundles`

Viene visualizzato un elenco di bundle:

![schermata_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

Utilizzando questa scheda è possibile:

* **Installa o aggiorna**

  Puoi **Sfogliare** per trovare il file contenente il bundle e specificare se deve **Iniziare** immediatamente e a quale **Livello Inizio**.

* **Ricarica**

  Aggiorna l&#39;elenco visualizzato.

* **Aggiorna pacchetti**

  Questa verifica i riferimenti di tutti i colli e, se necessario, li aggiorna.

  Ad esempio, dopo un aggiornamento, la vecchia e la nuova versione potrebbero essere ancora in esecuzione a causa di riferimenti precedenti. Questa opzione controlla e sposta tutti i riferimenti alla nuova versione, consentendo l’interruzione della versione precedente.

* **Avvia**

  Avvia un bundle in base al livello iniziale specificato.

* **Interrompi**

  Arresta il bundle.

* **Disinstalla**

  Disinstalla il bundle dal sistema.

* **visualizza lo stato**

  L’elenco specifica lo stato del bundle; facendo clic sul nome di un bundle specifico per visualizzare ulteriori informazioni.

>[!NOTE]
>
>Dopo **Aggiornamento**, Adobe consiglia di eseguire un **Aggiornamento pacchetti**.

## Componenti {#components}

La scheda **Componenti** consente di abilitare e/o disabilitare i vari componenti. È accessibile da:

* Il menu a discesa:

  **Principale >**

* L’URL; ad esempio:

  `http://localhost:4502/system/console/components`

Viene visualizzato un elenco di componenti. Sono disponibili varie icone che consentono di abilitare, disabilitare o (se appropriato) aprire i dettagli di configurazione di un componente specifico.

![schermata_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Facendo clic sul nome di un particolare componente vengono visualizzate ulteriori informazioni sul suo stato. Qui puoi anche abilitare, disabilitare o ricaricare il componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>L’attivazione o la disattivazione di un componente si applica solo fino al riavvio di AEM/CRX.
>
>Lo stato iniziale è definito all’interno del descrittore del componente, che viene generato durante lo sviluppo e memorizzato nel bundle al momento della creazione del bundle.
