---
title: Domande frequenti di carattere tecnico
description: Domande tecniche frequenti su AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: ec722773ce3acff1d0de861523db8ff7df552c4b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# Domande frequenti tecniche su AEM 6.5 LTS {#technical-faq}

Questa pagina consente di rispondere ad alcune domande tecniche frequenti su AEM 6.5 LTS.

## Domande frequenti tecniche

### L&#39;endpoint `/systemalive` non è più disponibile in AEM 6.5 LTS.

Il bundle Felix System Ready configurato per fornire l&#39;endpoint `/systemalive` è stato dichiarato obsoleto e sostituito da Apache Felix Health Checks. Questo bundle non è più incluso in AEM 6.5 LTS.

Il nuovo endpoint di verifica stato è disponibile all&#39;indirizzo `/system/health` e viene implementato tramite i controlli di integrità di Apache Felix.

Per la documentazione dettagliata sul framework di verifica stato Felix, consulta la [documentazione Felix](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md).

### Supporto della console AEM Groovy

La versione della console AEM Groovy in uso in AEM 6.5 potrebbe non funzionare in AEM 6.5 LTS a causa di dipendenze guava mancanti. La nuova versione supportata della console AEM Groovy è [19.0.8](https://mvnrepository.com/artifact/be.orbinson.aem/aem-groovy-console/19.0.8).

### AEM 6.5 LTS supporta la sincronizzazione degli utenti?

Sì, AEM 6.5 LTS supporta la sincronizzazione degli utenti. Non vi è alcuna modifica nella funzionalità di sincronizzazione utente tra AEM 6.5 e 6.5 LTS.

### Il file JAR di Uber su Maven Central sembra essere danneggiato — qual è il problema?

Verificare di utilizzare il file JAR Uber con il classificatore `apis`. La struttura di imballaggio del file JAR Uber è cambiata in AEM 6.5 LTS. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR AEM Uber](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

## Ottenimento di ulteriore assistenza

Se riscontri problemi non trattati qui:
* Consulta le [note sulla versione](/help/release-notes/release-notes.md) per informazioni sui problemi noti.
* Per assistenza, contatta il supporto Adobe.
