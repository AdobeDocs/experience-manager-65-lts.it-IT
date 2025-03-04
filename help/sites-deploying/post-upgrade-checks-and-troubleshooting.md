---
title: Controlli post-aggiornamento e risoluzione dei problemi
description: Scopri come risolvere i problemi che potrebbero verificarsi dopo un aggiornamento.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 09b297721b08ef428f1ac8a26fec38d5a8bd34fd
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# Controlli post-aggiornamento e risoluzione dei problemi{#post-upgrade-checks-and-troubleshooting}

## Controlli post-aggiornamento {#post-upgrade-checks}

Dopo l&#39;[aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md), è necessario eseguire le seguenti attività per finalizzare l&#39;aggiornamento. Si presume che AEM sia stato avviato con il file jar AEM 6.5 LTS e che la base di codice aggiornata sia stata distribuita.

* [Verifica dei registri per il completamento dell&#39;aggiornamento](#verify-logs-for-upgrade-success)

* [Verificare i bundle OSGi](#verify-osgi-bundles)

* [Verifica versione Oak](#verify-oak-version)

* [Convalida iniziale delle pagine](#initial-validation-of-pages)

* [Verifica configurazioni di manutenzione pianificate](#verify-scheduled-maintenance-configurations)

* [Abilita agenti di replica](#enable-replication-agents)

* [Abilita processi pianificati personalizzati](#enable-custom-scheduled-jobs)

* [Esegui piano di test](#execute-test-plan)


### Verifica registri per aggiornamento completato {#verify-logs-for-upgrade-success}

**aggiorna.registro**

In passato, il controllo dello stato di post-aggiornamento dell’istanza richiedeva un’attenta ispezione di vari file di registro, parti dell’archivio e il modulo di avvio. La generazione di un rapporto post-aggiornamento può aiutare a rilevare gli aggiornamenti difettosi prima della pubblicazione.

Lo scopo principale di questa funzione è ridurre la necessità di interpretazione manuale o logica di analisi complessa su più endpoint necessari per qualificare il successo di un aggiornamento. La soluzione fornisce informazioni inequivocabili che consentono ai sistemi di automazione esterni di reagire in caso di esito positivo o negativo di un aggiornamento.

In particolare, garantisce che:

* Gli errori di aggiornamento rilevati dal framework di aggiornamento sono centralizzati in un unico rapporto di aggiornamento.
* Il rapporto sull’aggiornamento include indicatori sul necessario intervento manuale.

Per risolvere questo problema, sono state apportate modifiche alla modalità di generazione dei registri nel file `upgrade.log`.

**error.log**

Il file error.log deve essere esaminato attentamente durante e dopo l’avvio di AEM utilizzando la versione target jar. Eventuali avvertenze o errori devono essere esaminati. In generale, è consigliabile cercare i problemi all’inizio del registro. Gli errori che si verificano più avanti nel registro possono in realtà essere effetti collaterali di una causa principale che viene richiamata all’inizio del file. Se si verificano errori e avvisi ripetuti, vedere di seguito per [Analisi dei problemi relativi all&#39;aggiornamento](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificare i bundle OSGi {#verify-osgi-bundles}

Passa alla console OSGi `/system/console/bundles` e verifica se alcuni bundle non sono stati avviati. Se uno dei bundle si trova in uno stato di installazione, consultare `error.log` per determinare il problema radice.

### Verifica versione Oak {#verify-oak-version}

In seguito all&#39;aggiornamento, dovresti notare che la versione di Oak è stata aggiornata a **1.68.1-B002**. Per verificare la versione di Oak, accedi alla console OSGi e controlla la versione associata ai bundle di Oak: Oak Core, Oak Commons, Oak Segment Tar.

### Convalida iniziale delle pagine {#initial-validation-of-pages}

Esegui una convalida iniziale su più pagine in AEM. Se si aggiorna un ambiente di authoring, aprire la pagina iniziale e la pagina di benvenuto ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). In entrambi gli ambienti Author e Publish, apri alcune pagine di applicazioni e verifica che vengano riprodotte correttamente. In caso di problemi, consultare `error.log` per la risoluzione dei problemi.

### Verifica configurazioni di manutenzione pianificate {#verify-scheduled-maintenance-configurations}

#### Abilita raccolta oggetti inattivi dell’archivio dati {#enable-data-store-garbage-collection}

Se utilizzi un archivio dati file, accertati che l’attività Raccolta oggetti inattivi dell’archivio dati sia abilitata e aggiunta all’elenco Manutenzione settimanale. Le istruzioni sono descritte in [Pulizia revisioni](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>Questa operazione non è consigliata per le installazioni dell’archivio dati personalizzato S3 o quando si utilizza un archivio dati condiviso.

#### Abilita pulizia revisioni online {#enable-online-revision-cleanup}

Se utilizzi MongoMK o il nuovo formato di segmento TarMK, accertati che l’attività Pulizia revisioni sia abilitata e aggiunta all’elenco Manutenzione giornaliera. Le istruzioni sono descritte in [Pulizia revisioni](/help/sites-deploying/revision-cleanup.md).

### Abilita agenti di replica {#enable-replication-agents}

Dopo aver aggiornato e convalidato completamente l’ambiente di pubblicazione, abilita gli agenti di replica nell’ambiente di authoring. Verifica che gli agenti siano in grado di connettersi alle rispettive istanze Publish. Consulta [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md) per ulteriori dettagli sull&#39;ordine degli eventi.

### Abilita processi pianificati personalizzati {#enable-custom-scheduled-jobs}

A questo punto è possibile abilitare tutti i processi pianificati come parte della base di codice.

### Esegui piano di test {#execute-test-plan}

Eseguire il piano di test dettagliato definito in [Aggiornamento del codice e delle personalizzazioni nella sezione **Procedura di test**](/help/sites-deploying/upgrading-code-and-customizations.md#testing-procedure-testing-procedure).

## Analisi Dei Problemi Relativi All’Aggiornamento {#analyzing-issues-with-the-upgrade}

Questa sezione contiene alcuni scenari di problemi che è possibile affrontare durante la procedura di aggiornamento ad AEM 6.5 LTS.

### Impossibile aggiornare pacchetti e bundle  {#packages-and-bundles-fail-to-update}

Nel caso in cui i pacchetti non vengano installati durante l’aggiornamento, i bundle in essi contenuti non verranno aggiornati. Questa categoria di problemi è causata da una configurazione errata dell’archivio dati. Verranno inoltre visualizzati come **ERRORE** e **AVVERTENZA** messaggi nel log degli errori. Poiché nella maggior parte di questi casi l’accesso predefinito potrebbe non funzionare, puoi utilizzare CRXDE direttamente per verificare e individuare i problemi di configurazione.

### Aggiornamento Non Eseguito {#the-upgrade-did-not-run}

Prima di avviare i passaggi di preparazione, assicurarsi di eseguire prima l&#39;istanza **source** eseguendola con il comando `java -jar aem-quickstart.jar`. Questo è necessario per assicurarsi che il file quickstart.properties sia generato correttamente. Se manca, l’aggiornamento non funzionerà. In alternativa, è possibile verificare se il file è presente cercando in `crx-quickstart/conf` nella cartella di installazione dell&#39;istanza di origine. Inoltre, quando si avvia AEM per avviare l&#39;aggiornamento, è necessario eseguirlo con il comando `java -jar <aem-quickstart-6.5-LTS.jar>`. L’avvio da uno script di avvio non avvierà AEM in modalità di aggiornamento.

### Alcuni bundle di AEM non passano allo stato attivo {#some-aem-bundles-are-not-switching-to-the-active-state}

Se sono presenti bundle che non si avviano, verifica la presenza di eventuali dipendenze non soddisfatte.

Nel caso in cui il problema sia presente ma si basi su un’installazione non riuscita del pacchetto che ha portato a un mancato aggiornamento dei bundle, questi verranno considerati incompatibili per la nuova versione. Per ulteriori informazioni su come risolvere il problema, vedere **Impossibile aggiornare pacchetti e bundle**.

Si consiglia inoltre di confrontare l’elenco dei bundle di una nuova istanza AEM 6.5 LTS con quello aggiornato per rilevare i bundle che non sono stati aggiornati. Questo fornirà un ambito più vicino di ciò che si desidera cercare in `error.log`.

### Bundle personalizzati non passano allo stato attivo {#custom-bundles-not-switching-to-the-active-state}

Se i bundle personalizzati non passano allo stato attivo, è probabile che ci sia codice che non importa l’API modificata. Questo nella maggior parte dei casi porterà a dipendenze non soddisfatte.

È inoltre consigliabile verificare se la modifica che ha causato il problema era necessaria e, in caso contrario, ripristinarla. Controlla anche se l’aumento di versione dell’esportazione del pacchetto è stato aumentato più del necessario, seguendo un rigoroso controllo delle versioni semantiche.

### Analisi di error.log e upgrade.log {#analyzing-the-error.log-and-upgrade.log}

Nella maggior parte delle situazioni, i registri devono essere consultati per gli errori per individuare la causa di un problema. Tuttavia, con gli aggiornamenti, è anche necessario monitorare i problemi di dipendenza in quanto i vecchi bundle potrebbero non essere aggiornati correttamente.

Il modo migliore per farlo è quello di eliminare error.log rimuovendo tutti i messaggi che si prevede non siano correlati al problema che stai affrontando. Puoi eseguire questa operazione tramite uno strumento come grep, utilizzando:

```shell
grep -v UnrelatedErrorString
```

Alcuni messaggi di errore potrebbero non essere immediatamente esplicativi. In questo caso, anche esaminare il contesto in cui si verificano può essere utile per capire dove è stato creato l’errore. È possibile separare l’errore utilizzando:

* `grep -B` per l&#39;aggiunta di righe prima dell&#39;errore;

oppure

* `grep -A` per l&#39;aggiunta di righe dopo.

In alcuni casi è possibile trovare anche messaggi WARN in quanto possono esserci casi validi che portano a questo stato e l’applicazione non è sempre in grado di decidere se si tratta di un errore effettivo. Assicurati di consultare anche questi messaggi.

### Contattare il supporto Adobe {#contacting-adobe-support}

Se hai già esaminato i consigli su questa pagina e riscontri ancora problemi, contatta il supporto Adobe. Per fornire quante più informazioni possibili al tecnico del supporto che lavora al tuo caso, assicurati di includere i file `error.log` e `upgrade.log` dall&#39;aggiornamento.
