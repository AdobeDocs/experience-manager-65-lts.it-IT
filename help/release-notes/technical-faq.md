---
title: Domande frequenti di carattere tecnico
description: Domande tecniche frequenti su AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 2352420843c613884ad3cae487ed048bd775e294
workflow-type: tm+mt
source-wordcount: '171'
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

## Ottenimento di ulteriore assistenza

Se riscontri problemi non trattati qui:
* Consulta le [note sulla versione](/help/release-notes/release-notes.md) per informazioni sui problemi noti.
* Per assistenza, contatta il supporto Adobe.
