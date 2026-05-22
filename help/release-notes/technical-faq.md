---
title: Domande frequenti (FAQ) tecniche
description: Domande frequenti tecniche su AEM 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: f994a8712a403083de1edc62579846ba99bd3afd
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 59%

---

# FAQ tecniche su AEM 6.5 LTS {#technical-faq}

Questa pagina consente di rispondere ad alcune domande frequenti tecniche su AEM 6.5 LTS.

## FAQ tecniche

### L’endpoint `/systemalive` non è più disponibile in AEM 6.5 LTS.

Il bundle Felix System Ready configurato per fornire l’endpoint `/systemalive` è stato dichiarato obsoleto e sostituito dalle verifiche stato di Apache Felix. Questo bundle non è più incluso in AEM 6.5 LTS.

Il nuovo endpoint di verifica stato è disponibile all’indirizzo `/system/health` e viene implementato tramite i le verifiche stato di Apache Felix.

Per la documentazione dettagliata sul framework di verifica stato Felix, consulta la [documentazione Felix](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md).

### Supporto di AEM Groovy Console

La versione di AEM Groovy Console in uso in AEM 6.5 potrebbe non funzionare in AEM 6.5 LTS a causa di dipendenze guava mancanti. La nuova versione supportata di AEM Groovy Console è [19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip).

#### Configurazione aggiuntiva richiesta per AEM Groovy Console

Se utilizzi AEM Groovy Console, devi aggiungere esplicitamente la seguente configurazione OSGi per `com.adobe.granite.apicontroller.FilterResolverHookFactory`. Aggiungi `aem-groovy-console-bundle` all&#39;elenco di bundle consentiti per la chiave `org.apache.sling.distribution.api`, estendendo le impostazioni predefinite della piattaforma:

```
"org.apache.sling.distribution.api": "com.adobe.*,com.day.*,org.apache.sling.*,aem-groovy-console-bundle"
```

### AEM 6.5 LTS supporta la sincronizzazione utente?

Sì, AEM 6.5 LTS supporta la sincronizzazione utente. Non vi è alcuna modifica nella funzionalità di sincronizzazione utente tra AEM 6.5 e 6.5 LTS.

### Il file JAR Uber su Maven Central sembra essere danneggiato: qual è il problema?

Verifica di utilizzare il file JAR Uber con il classificatore `apis`. La struttura del pacchetto del file JAR Uber è cambiata in AEM 6.5 LTS. Per ulteriori informazioni, consulta [Aggiornare la versione del file JAR Uber di AEM](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

### AEM 6.5 LTS supporta gli spazi dei nomi del pacchetto `jakarta.*` (ad esempio, `jakarta.annotation`)?

No. AEM 6.5 LTS non supporta gli artefatti Sling migrati negli spazi dei nomi del pacchetto `jakarta.*`. Utilizza gli equivalenti `javax.*` nel codice e nelle dipendenze, ad esempio `javax.annotation.PostConstruct` anziché `jakarta.annotation.PostConstruct` nei modelli Sling. L’implementazione dei modelli Sling in AEM 6.5 LTS riconosce solo le annotazioni `javax.*`, pertanto `jakarta.*` annotazioni vengono ignorate automaticamente durante l’inizializzazione.

Per ulteriori informazioni, vedere l&#39;articolo della Knowledge Base [Errore dei modelli Sling con `jakarta.annotation.PostConstruct` in AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-30339).

## Ottenere ulteriore assistenza.

Se riscontri problemi non trattati qui:
* rivedi le [note sulla versione](/help/release-notes/release-notes.md) per informazioni sui problemi noti.
* Per ricevere assistenza, contatta il supporto Adobe.
