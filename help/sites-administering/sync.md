---
title: Sincronizzazione utente
description: Scopri le funzioni interne della sincronizzazione degli utenti in AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b7b1bce6-9cea-4f13-955f-f9e361f298bf
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 1%

---

# Sincronizzazione utente{#user-synchronization}

## Introduzione {#introduction}

Quando la distribuzione è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), i membri devono essere in grado di accedere e visualizzare i propri dati in qualsiasi nodo di pubblicazione.

Gli utenti e i gruppi di utenti (dati utente) creati nell’ambiente di pubblicazione non sono necessari nell’ambiente di authoring.

La maggior parte dei dati utente creati nell’ambiente di authoring devono rimanere nell’ambiente di authoring e non devono essere copiati nelle istanze di pubblicazione.

Per poter accedere agli stessi dati utente, la registrazione e le modifiche effettuate su un’istanza Publish devono essere sincronizzate con altre istanze Publish.

A partire da AEM 6.1, quando la sincronizzazione utente è abilitata, i dati utente vengono sincronizzati automaticamente tra le istanze Publish nella farm e non vengono creati nell’ambiente di authoring.

## Distribuzione Sling {#sling-distribution}

I dati utente, insieme ai relativi [ACL](/help/sites-administering/security.md), sono archiviati nel [Oak Core](/help/sites-deploying/platform.md), il livello inferiore a Oak JCR, e sono accessibili utilizzando l&#39;[API Oak](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Con aggiornamenti non frequenti, è ragionevole sincronizzare i dati utente con altre istanze Publish utilizzando [Distribuzione contenuto Sling](https://github.com/apache/sling-old-svn-mirror/blob/trunk/contrib/extensions/distribution/README.md) (distribuzione Sling).

Rispetto alla replica tradizionale, la sincronizzazione degli utenti con la distribuzione Sling offre i seguenti vantaggi:

* *utenti*, *profili utente* e *gruppi di utenti* creati al momento della pubblicazione non creati nell&#39;istanza di authoring

* La distribuzione Sling imposta le proprietà negli eventi JCR, consentendo di agire all’interno dei listener di eventi lato pubblicazione senza preoccuparsi di cicli di replica infiniti
* La distribuzione Sling invia solo i dati utente alle istanze Publish non originarie, eliminando il traffico non necessario
* [Gli ACL](/help/sites-administering/security.md) impostati nel nodo utente sono inclusi nella sincronizzazione

>[!NOTE]
>
>Se sono necessarie sessioni, si consiglia di utilizzare una soluzione SSO o una sessione permanente e chiedere ai clienti di effettuare l’accesso se passano a un’altra istanza Publish.

>[!CAUTION]
>
>La sincronizzazione del gruppo **amministratori** non è supportata, anche se la sincronizzazione degli utenti è abilitata. Al contrario, nel registro degli errori viene registrato un errore di &quot;importazione delle differenze&quot;.
>
>Pertanto, quando la distribuzione è una farm di pubblicazione, se un utente viene aggiunto o rimosso dal gruppo **amministratori**, la modifica deve essere eseguita manualmente in ogni istanza di pubblicazione.

## Abilita sincronizzazione utenti {#enable-user-sync}

>[!NOTE]
>
>Per impostazione predefinita, la sincronizzazione utente è `disabled`.
>
>L&#39;abilitazione della sincronizzazione degli utenti comporta la modifica di *configurazioni OSGi esistenti*.
>
>Non è possibile aggiungere nuove configurazioni abilitando la sincronizzazione degli utenti.

La sincronizzazione degli utenti si basa sull’ambiente di authoring per gestire le distribuzioni dei dati utente, anche se i dati utente non vengono creati nell’ambiente di authoring. Gran parte della configurazione, ma non tutte, si svolge nell’ambiente di authoring e ogni passaggio identifica chiaramente se deve essere eseguita su Author o Publish.

Di seguito sono riportati i passaggi necessari per abilitare la sincronizzazione utente, seguiti da una sezione [Risoluzione dei problemi](#troubleshooting):

### Prerequisiti {#prerequisites}

1. Se utenti e gruppi di utenti sono già stati creati in un&#39;istanza Publish, si consiglia di [sincronizzare manualmente](#manually-syncing-users-and-user-groups) i dati utente in tutte le istanze Publish prima di configurare e abilitare la sincronizzazione utente.

Una volta abilitata la sincronizzazione degli utenti, vengono sincronizzati solo gli utenti e i gruppi appena creati.

1. Verifica che sia installato il codice più recente:

* [Aggiornamenti alla piattaforma AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it)

### 1. Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione {#apache-sling-distribution-agent-sync-agents-factory}

**Abilita sincronizzazione utenti**

* **su autore**

   * accedi con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individua `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleziona la configurazione esistente per aprirla per la modifica (icona a forma di matita)
Verifica `name`: **`socialpubsync`**

      * selezionare la casella di controllo `Enabled`
      * seleziona `Save`

![Agente di distribuzione Apache Sling](assets/chlimage_1-20.png)

### 2. Crea utente autorizzato {#createauthuser}

**Configurare le autorizzazioni**

L’utente autorizzato viene utilizzato nel passaggio 3 per configurare la distribuzione Sling in Author.

* **su ogni istanza Publish**

   * accedi con privilegi di amministratore
   * accedere a [Console sicurezza](/help/sites-administering/security.md)

      * ad esempio, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * creare un utente

      * ad esempio, `usersync-admin`

   * aggiungi questo utente al gruppo di utenti **`administrators`**
   * [aggiungi ACL per questo utente a /home](#howtoaddacl)

      * `Allow jcr:all` con restrizione `rep:glob=*/activities/*`

>[!CAUTION]
>
>Creare un nuovo utente.
>
>* Utente predefinito assegnato: **`admin`**.
>

#### Come aggiungere ACL {#addacls}

* accedere a CRXDE Lite

   * ad esempio, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* seleziona `/home` nodo
* nel riquadro destro selezionare la scheda `Access Control`
* per aggiungere una voce ACL, selezionare il pulsante `+`

   * **Entità**: *ricerca utente creato per sincronizzazione utenti*
   * **Tipo**: `Allow`
   * **Privilegi**: `jcr:all`
   * **Limitazioni** `rep:glob`: `*/activities/*`
   * seleziona **OK**

* seleziona **Salva tutto**

![Aggiungi finestra ACL](assets/chlimage_1-21.png)

Consulta anche

* [Gestione diritti di accesso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Risoluzione dei problemi nella sezione [Modifica eccezione operazione durante l&#39;elaborazione della risposta](#modify-operation-exception-during-response-processing).

### 3. Distribuzione Adobe Granite - Provider segreto di trasporto per password crittografata {#adobegraniteencpasswrd}

**Configurare le autorizzazioni**

Dopo aver creato un utente autorizzato membro del gruppo di utenti **`administrators`** in tutte le istanze Publish, è necessario identificare l&#39;utente autorizzato in Autore come autorizzato a sincronizzare i dati utente da Autore a Pubblicazione.

* **su autore**

   * accedi con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individua `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * per aprire per la modifica, seleziona la configurazione esistente (icona matita)
Verifica `property name`: **`socialpubsync-publishUser`**

   * imposta il nome utente e la password per l&#39;[utente autorizzato](#createauthuser) creato al momento della pubblicazione nel passaggio 2

      * ad esempio, `usersync-admin`

![Provider segreto di trasporto per password crittografata](assets/chlimage_1-22.png)

### 4. Agente di distribuzione Apache Sling - Factory agenti coda {#apache-sling-distribution-agent-queue-agents-factory}

**Abilita sincronizzazione utenti**

* **su ogni istanza Publish**:

   * accedi con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * individua `Apache Sling Distribution Agent - Queue Agents Factory`

      * per aprire per la modifica, seleziona la configurazione esistente (icona matita)
Verifica `Name`: `socialpubsync-reverse`

      * selezionare la casella di controllo `Enabled`
      * seleziona `Save`

   * **repeat** per ogni istanza Publish

![Factory agenti coda](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Factory {#diffobserver}

**Abilita sincronizzazione gruppo**

* **su ogni istanza Publish**:

   * accedi con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * individua **`Adobe Social Sync - Diff Observer Factory`**

      * per aprire per la modifica, seleziona la configurazione esistente (icona matita)

        Verifica `agent name`: `socialpubsync-reverse`

      * selezionare la casella di controllo `Enabled`
      * seleziona `Save`

![Diff Observer Factory](assets/screen-shot_2019-05-24at090809.png)

### 6. Trigger di distribuzione Apache Sling - Fabbrica dei trigger pianificati {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Facoltativo) modifica intervallo di polling**

Per impostazione predefinita, l’autore esegue il polling delle modifiche ogni 30 secondi. Per modificare questo intervallo:

* **su autore**

   * accedi con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individua `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * per aprire per la modifica, seleziona la configurazione esistente (icona matita)

         * Verifica `Name`: `socialpubsync-scheduled-trigger`

      * imposta `Interval in Seconds` sull&#39;intervallo desiderato
      * seleziona `Save`

![Fabbrica attivatori pianificati](assets/chlimage_1-24.png)

## Configurazione per più istanze di pubblicazione {#configure-for-multiple-publish-instances}

La configurazione predefinita è per una singola istanza Publish. Poiché il motivo per abilitare la sincronizzazione degli utenti è quello di sincronizzare più istanze di pubblicazione, ad esempio per una farm di pubblicazione, è necessario aggiungere le istanze di pubblicazione aggiuntive alla factory degli agenti di sincronizzazione.

### 7. Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione {#apache-sling-distribution-agent-sync-agents-factory-1}

**Aggiungi istanze di pubblicazione:**

* **su autore**

   * accedi con privilegi di amministratore
   * accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

      * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * individua `Apache Sling Distribution Agent - Sync Agents Factory`

      * per aprire per la modifica, seleziona la configurazione esistente (icona matita)
Verifica `Name`: `socialpubsync`

![Factory agenti di sincronizzazione](assets/chlimage_1-25.png)

* **Endpoint esportazione**
Deve essere presente un endpoint di esportazione per ogni istanza Publish. Ad esempio, se sono presenti 2 istanze Publish, localhost:4503 e 4504, devono essere presenti due voci:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Endpoint importazione**
Deve essere presente un endpoint di importazione per ogni istanza Publish. Ad esempio, se sono presenti 2 istanze Publish, localhost:4503 e 4504, devono essere presenti due voci:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* seleziona `Save`

### 8. ID Sling univoco {#unique-sling-id}

>[!CAUTION]
>
>Se l’ID Sling corrisponde tra due o più istanze Publish, la sincronizzazione dei gruppi di utenti non riesce.

Se l’ID Sling è lo stesso per più istanze Publish in una farm di pubblicazione, i gruppi di utenti non vengono sincronizzati.

Per verificare che tutti i valori degli ID Sling siano diversi, per ogni istanza Publish:

1. passa a `http://<host>:<port>/system/console/status-slingsettings`
1. verifica il valore di **Sling ID**

![Controllo del valore dell&#39;ID Sling](assets/chlimage_1-27.png)

Se l’ID Sling di un’istanza Publish corrisponde all’ID Sling di qualsiasi altra istanza Publish:

1. arresta una delle istanze Publish con un ID Sling corrispondente
1. nella directory crx-quickstart/launchpad/felix

   * cerca ed elimina il file denominato *sling.id.file*

      * ad esempio, su un sistema Linux®:
        `rm -i $(find . -type f -name sling.id.file)`

      * ad esempio, in un sistema Windows:
        `use windows explorer and search for *sling.id.file*`

1. avviare l’istanza Publish

   * all’avvio viene assegnato un nuovo ID Sling

1. verifica che **Sling ID** sia univoco

Ripeti questi passaggi fino a quando tutte le istanze Publish non hanno un ID Sling univoco.

## Generatore pacchetti Vault - Fabbrica {#vault-package-builder-factory}

Per sincronizzare correttamente gli aggiornamenti, è necessario modificare il generatore di pacchetti di Vault per la sincronizzazione utente:

* su ogni istanza di AEM Publish
* accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

   * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* individuare `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* seleziona l’icona modifica
* aggiungi due `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* gestione delle policy:

   * per sovrascrivere i nodi rep:policy esistenti con quelli nuovi, aggiungete un terzo filtro pacchetto:

      * `/home/users|+.*/rep:policy`

   * per impedire la distribuzione dei criteri, impostare

      * `Acl Handling:` `IGNORE`

![Generatore di pacchetti Vault](assets/vault-package-builder-factory.png)

## Cosa Succede Quando... {#what-happens-when}

### Autoregistrazione utente o modifica profilo durante la pubblicazione {#user-self-registers-or-edits-profile-on-publish}

Per progettazione, gli utenti e i profili creati nell’ambiente di pubblicazione (registrazione autonoma) non vengono visualizzati nell’ambiente di authoring.

Se la topologia è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm) e la sincronizzazione utente è stata configurata correttamente, il profilo utente *utente* e *utente* viene sincronizzato nella farm di pubblicazione utilizzando la distribuzione Sling.

### Gli utenti o i gruppi di utenti vengono creati utilizzando la console Sicurezza {#users-or-user-groups-are-created-using-security-console}

Per progettazione, i dati utente creati nell’ambiente di pubblicazione non vengono visualizzati nell’ambiente di authoring e viceversa.

Se necessario, quando si utilizza la console [Amministrazione utenti e sicurezza](/help/sites-administering/security.md) per aggiungere nuovi utenti nell&#39;ambiente di pubblicazione, la sincronizzazione utente sincronizza i nuovi utenti e l&#39;appartenenza al gruppo con altre istanze di pubblicazione. La sincronizzazione degli utenti sincronizza anche i gruppi di utenti creati tramite la console di sicurezza.

## Risoluzione dei problemi {#troubleshooting}

### Come portare offline User Sync {#how-to-take-user-sync-offline}

Per portare la sincronizzazione utente offline, per [rimuovere un&#39;istanza Publish](#how-to-remove-a-publish-instance) o [sincronizzare manualmente i dati](#manually-syncing-users-and-user-groups), la coda di distribuzione deve essere vuota e silenziosa.

Per verificare lo stato della coda di distribuzione:

* su Autore:

   * utilizzo di [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * cerca voci in `/var/sling/distribution/packages`

         * nodi cartella denominati con il pattern `distrpackage_*`

   * utilizzo di [Gestione pacchetti](/help/sites-administering/package-manager.md)

      * cerca pacchetti in sospeso (non ancora installati)

         * denominato con il pattern `socialpubsync-vlt*`

Quando la coda di distribuzione è vuota, disabilita la sincronizzazione utente:

* all’autore

   * *deselezionare *la casella di controllo `Enabled` per [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

Al termine delle attività, per riattivare la sincronizzazione utente:

* all’autore

   * selezionare la casella di controllo `Enabled` per [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnostica sincronizzazione utenti {#user-sync-diagnostics}

Diagnostica sincronizzazione utenti è uno strumento che controlla la configurazione e tenta di identificare eventuali problemi.

In fase di creazione, è sufficiente passare dalla console principale tramite **Strumenti, Operazioni, Diagnosi, Diagnostica sincronizzazione utenti.**

I risultati vengono visualizzati semplicemente inserendo la console Diagnostica sincronizzazione utenti.

Questo viene visualizzato quando Sincronizzazione utente non è stata abilitata:

![Avviso relativo al fatto che Diagnostica sincronizzazione utenti non è abilitata](assets/chlimage_1-28.png)

#### Eseguire la diagnostica per le istanze di pubblicazione {#how-to-run-diagnostics-for-publish-instances}

Quando la diagnostica viene eseguita dall&#39;ambiente di authoring, i risultati superati/non riusciti includono una sezione [INFO] che mostra l&#39;elenco delle istanze di pubblicazione configurate per la conferma.

Nell’elenco è incluso un URL per ogni istanza Publish che esegue la diagnostica per tale istanza. Il parametro URL `syncUser` viene aggiunto all&#39;URL di diagnostica con il relativo valore impostato sull&#39;*utente di sincronizzazione autorizzato* creato nel [passaggio 2](#createauthuser).

**Nota**: prima di avviare l&#39;URL, l&#39;utente di sincronizzazione *autorizzato* deve avere già effettuato l&#39;accesso all&#39;istanza Publish.

![Diagnostica per istanze di pubblicazione](assets/chlimage_1-29.png)

### Configurazione aggiunta in modo errato {#configuration-improperly-added}

Quando la sincronizzazione utente non funziona, il problema più comune è che sono state aggiunte *configurazioni aggiuntive*. La configurazione *predefinita esistente deve essere stata *modificata*.

Di seguito sono riportate le visualizzazioni delle configurazioni predefinite modificate da visualizzare nella console Web. Se compaiono più istanze, la configurazione aggiunta deve essere rimossa.

#### (Autore) Un agente di distribuzione Apache Sling - Sync Agents Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![Visualizzazione configurazioni predefinite modificate nella console Web](assets/chlimage_1-30.png)

#### (Autore) Una credenziale trasporto distribuzione Apache Sling - Credenziali utente basate su DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![Visualizzazione configurazioni predefinite modificate nella console Web](assets/chlimage_1-31.png)

#### (Pubblicazione) Un agente di distribuzione Apache Sling - Queue Agents Factory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![Visualizzazione configurazioni predefinite modificate nella console Web](assets/chlimage_1-32.png)

#### (Pubblicazione) One Adobe Social Sync - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![Visualizzazione configurazioni predefinite modificate nella console Web](assets/chlimage_1-33.png)

#### (Autore) Un trigger di distribuzione Apache Sling - Factory di trigger pianificati {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![Visualizzazione configurazioni predefinite modificate nella console Web](assets/chlimage_1-34.png)

### Modifica eccezione operazione durante l&#39;elaborazione della risposta {#modify-operation-exception-during-response-processing}

Se nel registro è visibile quanto segue:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

Verificare quindi che la sezione [2. La creazione dell&#39;utente autorizzato](#createauthuser) è stata seguita correttamente.

Questa sezione descrive come creare un utente autorizzato, presente in tutte le istanze Publish, e come identificarlo nella configurazione OSGi &quot;Provider segreto&quot; nell’ambiente di authoring. Per impostazione predefinita, l&#39;utente è `admin`.

L&#39;utente autorizzato deve essere incluso nel gruppo di utenti **`administrators`** e le autorizzazioni per tale gruppo non devono essere modificate.

L’utente autorizzato deve disporre esplicitamente dei seguenti privilegi e restrizioni su tutte le istanze Publish:

| **percorso** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | &#42;/attività/&#42; |
| /home/users | X | &#42;/attività/&#42; |
| /home/groups | X | &#42;/attività/&#42; |

Come membro del gruppo `administrators`, l&#39;utente autorizzato deve disporre dei seguenti privilegi su tutte le istanze Publish:

| **percorso** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Sincronizzazione gruppo utenti non riuscita {#user-group-sync-failed}

Se l’ID Sling corrisponde tra due o più istanze Publish, la sincronizzazione del gruppo di utenti non riesce.

Vedere la sezione [9. ID Sling univoco](#unique-sling-id)

### Sincronizzazione manuale di utenti e gruppi di utenti {#manually-syncing-users-and-user-groups}

* nelle istanze Publish in cui esistono utenti e gruppi di utenti:

   * [se abilitata, disabilita la sincronizzazione utenti](#how-to-take-user-sync-offline)
   * [crea un pacchetto](/help/sites-administering/package-manager.md#creating-a-new-package) di `/home`

      * durante la modifica del pacchetto

         * Scheda Filtri: Aggiungi filtro: Percorso principale: `/home`
         * Scheda Avanzate: Gestione AC: `Overwrite`

   * [esportare il pacchetto](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* su altre istanze Publish:

   * [importare il pacchetto](/help/sites-administering/package-manager.md#installing-packages)

Per configurare o abilitare la sincronizzazione utente, andare al passaggio 1: [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)

### Quando un’istanza Publish non è più disponibile {#when-a-publish-instance-becomes-unavailable}

Quando un’istanza Publish non è più disponibile, non deve essere rimossa se ritorna online in futuro. Le modifiche vengono inserite in coda per l&#39;istanza Publish e, quando questa è di nuovo online, vengono elaborate.

Se l’istanza Publish non torna mai online o se è offline in modo permanente, deve essere rimossa perché l’accumulo della coda determina un notevole utilizzo di spazio su disco nell’ambiente di authoring.

Quando un’istanza Publish è inattiva, il registro di authoring presenta eccezioni simili alle seguenti:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Come rimuovere un’istanza di pubblicazione {#how-to-remove-a-publish-instance}

Per rimuovere un&#39;istanza Publish dall&#39;[Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory), la coda di distribuzione deve essere vuota e invisibile all&#39;utente.

* su Autore:

   * [Disconnetti sincronizzazione utenti](#how-to-take-user-sync-offline)
   * segui il [passaggio 7](#apache-sling-distribution-agent-sync-agents-factory) per rimuovere l&#39;istanza Publish da entrambi gli elenchi di server:

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * riabilita sincronizzazione utenti

      * selezionare la casella di controllo `Enabled` per [Agente di distribuzione Apache Sling - Factory agenti di sincronizzazione](#apache-sling-distribution-agent-sync-agents-factory)
