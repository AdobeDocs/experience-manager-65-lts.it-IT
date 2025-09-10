---
title: Domande frequenti (FAQ) tecniche
description: Domande frequenti tecniche su AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: f983fc1edc613feaa070c4e82a92aabab9d50cbb
workflow-type: ht
source-wordcount: '247'
ht-degree: 100%

---

# FAQ tecniche su AEM 6.5 LTS {#technical-faq}

Questa pagina consente di rispondere ad alcune domande frequenti tecniche su AEM 6.5 LTS.

## FAQ tecniche

### L’endpoint `/systemalive` non è più disponibile in AEM 6.5 LTS.

Il bundle Felix System Ready configurato per fornire l’endpoint `/systemalive` è stato dichiarato obsoleto e sostituito dalle verifiche stato di Apache Felix. Questo bundle non è più incluso in AEM 6.5 LTS.

Il nuovo endpoint di verifica stato è disponibile all’indirizzo `/system/health` e viene implementato tramite i le verifiche stato di Apache Felix.

Per la documentazione dettagliata sul framework di verifica stato Felix, consulta la [documentazione Felix](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md).

### Supporto della console AEM Groovy

La versione della console AEM Groovy in uso in AEM 6.5 potrebbe non funzionare in AEM 6.5 LTS a causa di dipendenze guava mancanti. La nuova versione supportata della console AEM Groovy è [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip).

### AEM 6.5 LTS supporta la sincronizzazione utente?

Sì, AEM 6.5 LTS supporta la sincronizzazione utente. Non vi è alcuna modifica nella funzionalità di sincronizzazione utente tra AEM 6.5 e 6.5 LTS.

### Il file JAR Uber su Maven Central sembra essere danneggiato: qual è il problema?

Verifica di utilizzare il file JAR Uber con il classificatore `apis`. La struttura del pacchetto del file JAR Uber è cambiata in AEM 6.5 LTS. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

## Ottenere ulteriore assistenza.

Se riscontri problemi non trattati qui:
* rivedi le [note sulla versione](/help/release-notes/release-notes.md) per informazioni sui problemi noti.
* Per ricevere assistenza, contatta il supporto Adobe.
