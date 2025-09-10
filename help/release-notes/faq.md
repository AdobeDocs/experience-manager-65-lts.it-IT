---
title: Domande frequenti (FAQ)
description: Domande frequenti su AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 9f9da819550b93d7a06b151962bf41751ecbc8b3
workflow-type: ht
source-wordcount: '513'
ht-degree: 100%

---

# Domande frequenti (FAQ) su AEM 6.5 LTS {#faq}

Questa pagina risponde ad alcune domande frequenti su AEM 6.5 LTS.

## Perché Adobe ha rilasciato 6.5 LTS per AEM?

Adobe si impegna a fondo per la sicurezza e la stabilità delle applicazioni che fornisce. Il supporto a lungo termine per AEM 6.5 getta le basi per gli aggiornamenti futuri di AEM 6.5. In particolare, AEM 6.5 LTS include il supporto per Oracle Java 17 e Java 21 e sarà il ramo AEM che riceverà nuove funzioni e innovazioni di AEM.

## Sono un cliente on-premise, cosa succede se non eseguo l’aggiornamento a AEM 6.5 LTS?

AEM 6.5 LTS include importanti aggiornamenti su sicurezza e stabilità, tra cui il supporto per Oracle Java 17 e Java 21. Anche se Adobe continuerà a supportare AEM 6.5 per almeno i prossimi 2 anni, si consiglia alle organizzazioni di iniziare a pianificare un aggiornamento a 6.5 LTS.

## Se eseguo l’aggiornamento a AEM 6.5 LTS, le personalizzazioni e le integrazioni esistenti ne saranno interessate?

Mentre AEM 6.5 LTS mira a mantenere la compatibilità con le versioni precedenti, alcune funzioni e artefatti precedenti sono stati rimossi.
È essenziale rivedere le [note sulla versione](/help/release-notes/release-notes.md#deprecated-and-removed-features) e utilizzare lo strumento [AEM Analyzer](/help/sites-deploying/aem-analyzer.md) per valutare l’impatto sulle personalizzazioni e sulle integrazioni.

## Come posso garantire una transizione fluida a AEM 6.5 LTS?

Per garantire una transizione senza intoppi, si consiglia di:

* rivedere le [note sulla versione](/help/release-notes/release-notes.md) e la documentazione accuratamente.
* Utilizzare lo strumento [AEM Analyzer](/help/sites-deploying/aem-analyzer.md) per valutare la complessità dell’aggiornamento.
* Pianificare e assegnare tempo e risorse sufficienti per il processo di aggiornamento.
* Partecipare alle sessioni di supporto e abilitazione di Adobe per ottenere assistenza e guida.

## Cosa sono i Service Pack di AEM 6.5 LTS?

I Service Pack di AEM 6.5 LTS sono un aggiornamento cumulativo che include tutte le correzioni e i miglioramenti apportati a AEM 6.5 LTS dalla sua versione iniziale. Si consiglia di applicare il service pack più recente per garantire che l’istanza di AEM sia aggiornata con le funzioni e le patch di sicurezza più recenti.

## Al momento sono in AEM 6.5, posso effettuare direttamente l’aggiornamento ai Service Pack di AEM 6.5 LTS senza effettuare l’aggiornamento a AEM 6.5 LTS in disponibilità generale?

Sì, puoi eseguire direttamente l’aggiornamento da AEM 6.5 a qualsiasi Service Pack di AEM 6.5 LTS. È consigliabile rivedere le [note sulla versione](/help/release-notes/release-notes.md) e la sezione [Aggiornamento a AEM 6.5 LTS](/help/sites-deploying/upgrade.md).

## Al momento sono in AEM 6.5 LTS GA, devo apportare modifiche al codice per eseguire l’aggiornamento ai Service Pack di AEM 6.5 LTS?

No, non è necessario apportare alcuna modifica al codice per eseguire l’aggiornamento da AEM 6.5 LTS ai Service Pack di AEM 6.5 LTS. Tuttavia, è sempre consigliabile rivedere le [note sulla versione](/help/release-notes/release-notes.md) e testare le personalizzazioni e le integrazioni in un ambiente di staging prima di applicare il Service Pack all’istanza di produzione.

## Desidero cominciare da zero con una nuova configurazione di AEM 6.5 LTS, posso iniziare direttamente dal Service Pack di AEM 6.5 LTS?

Sì, è possibile configurare direttamente un nuovo Service Pack AEM 6.5 LTS senza configurare la build AEM 6.5 LTS in disponibilità generale. Per ulteriori informazioni, è consigliabile rivedere le [note sulla versione](/help/release-notes/release-notes.md) e la sezione [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md).
