---
title: Normative sulla protezione dei dati e la privacy dei dati - Preparazione di Adobe Experience Manager
description: Scopri come Adobe Experience Manager supporta le varie normative su privacy e protezione dei dati. Include il Regolamento generale sulla protezione dei dati (RGPD) dell’UE, il California Consumer Privacy Act e le modalità per conformarsi quando si implementa un nuovo progetto AEM.
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer,Leader,Architect,Data Architect,User
exl-id: 6faf8e4f-ca2a-4d68-a354-fb0aa6c2644b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 44%

---

# Preparazione di Adobe Experience Manager per le normative su privacy e protezione dei dati {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Il contenuto di questo documento non costituisce una consulenza legale e non intende sostituirsi a una consulenza legale.
>
>Consulta l’ufficio legale della tua azienda per ricevere consigli in merito alle normative su privacy e protezione dei dati.

>[!NOTE]
>
>Per ulteriori informazioni sulla risposta di Adobe ai problemi di privacy e sulle conseguenze per i clienti di Adobe, consulta [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html).

Adobe fornisce documentazione e procedure (con API se disponibili) per l’amministratore della privacy del cliente o AEM per gestire le richieste di protezione dei dati e privacy dei dati. Può aiutarti a conformarti a queste normative. Le procedure documentate consentono ai clienti di eseguire le richieste normative manualmente o chiamando nelle API, se disponibili, da un portale o servizio esterno.

>[!CAUTION]
>
>I dettagli qui documentati sono limitati a Adobe Experience Manager.
>
>I dati provenienti da un altro servizio Adobe on-demand, insieme a eventuali richieste di accesso a dati personali correlate, richiederanno azioni su tale servizio.
>
>Per ulteriori informazioni, consulta [Centro per la privacy di Adobe](https://www.adobe.com/it/privacy.html).

## Introduzione {#introduction}

Le istanze di Adobe Experience Manager e le applicazioni che vengono eseguite su di esse sono di proprietà e gestite dai clienti Adobe.

Di conseguenza, le normative sulla protezione dei dati, come GDPR, CCPA e altri, sono in gran parte responsabilità dei clienti.

Come breve introduzione, le norme sulla privacy e la protezione dei dati includono nuove regole che devono essere seguite dai ruoli di:

* Business Entities (CCPA) e/o Data Controllers (GDPR)

* Service Providers (CCPA) e/o Data Processors (GDPR)

Le principali disposizioni di tali regolamenti sono le seguenti:

1. Definizione ampliata dei dati personali per includere tutti gli ID univoci; come nei dati direttamente e indirettamente identificabili.

2. Requisiti più severi in materia di consenso.

3. Maggiore attenzione ai diritti di eliminazione (Cancellazione dati).

4. Rinuncia alla vendita di dati.

Per Adobe Experience Manager:

* Le istanze, e le applicazioni che le eseguono, sono di proprietà e gestite dal cliente.

   * Il cliente gestisce i ruoli normativi, tra cui Business Entities e Service Provider, Data Controller e Data Processor, tra gli altri.

   * Adobe Experience Platform Privacy Service non farà parte del flusso di lavoro per AEM, come illustrato nel diagramma seguente.

* AEM include la documentazione e le procedure per l’amministratore della privacy del cliente e/o l’amministratore AEM per eseguire le richieste relative alla normativa sulla privacy, manualmente o tramite API, se disponibili.

* Nessun nuovo servizio o interfaccia utente aggiunto.

   * Le procedure e le API sono invece documentate per l’utilizzo da parte dell’interfaccia utente/dei portali dei clienti che gestiscono le richieste di normativa sulla privacy.

* AEM non includerà alcuno strumento predefinito per supportare il flusso di lavoro delle richieste di privacy.

   * Adobe fornisce documentazione e procedure per l’amministratore della privacy del cliente e per l’amministratore AEM, consentendo loro di eseguire manualmente le richieste relative alle normative sulla privacy.

Adobe fornisce procedure per la gestione delle richieste di accesso, cancellazione e rinuncia alla privacy relative a Adobe Experience Manager. A volte sono disponibili API che possono essere richiamate da un portale sviluppato dal cliente o da script per facilitare l’automazione.

Il diagramma seguente illustra l’aspetto di un flusso di lavoro per la richiesta di accesso a dati personali (illustrato con Adobe Experience Manager 6.5):

![Protezione dei dati e privacy](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager e preparazione alle normative {#aem-and-regulatory-readiness}

Consulta le sezioni seguenti per la documentazione normativa per le aree di prodotto di AEM.

## AEM Foundation {#aem-foundation}

Consulta [Gestione delle richieste di protezione dei dati e privacy per AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM: consenso alla raccolta di statistiche di utilizzo aggregate {#aem-opting-into-aggregate-usage-statistics-collection}

Vedi [Raccolta di statistiche di utilizzo aggregate](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

Consulta [AEM Sites - Preparazione per la protezione dei dati e la privacy.](/help/sites-administering/gdpr-compliance-sites.md)

## Integrazione di AEM con Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Queste integrazioni Adobe Experience Manager si riferiscono ai servizi di protezione dei dati e privacy pronti (ad esempio, GDPR o CCPA). In AEM non vengono memorizzati dati personali da Adobe Target o Adobe Analytics in relazione alle integrazioni.

Per ulteriori informazioni, consulta:

* [Adobe Target - Panoramica sulla privacy](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Flusso di lavoro sulla privacy dei dati di Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=it)

## AEM Forms {#aem-forms}

AEM Forms include componenti e flussi di lavoro che acquisiscono, elaborano e memorizzano dati per orchestrare i processi aziendali e completare le transazioni digitali. Componenti diversi utilizzano archivi di dati diversi e consentono l’integrazione anche con archivi di dati personalizzati. Nella documentazione seguente sono illustrate le procedure e le linee guida per l’accesso e la gestione dei dati utente per supportare i flussi di lavoro relativi alla privacy e alla protezione dei dati (ad esempio, GDPR o CCPA) per un componente.

* [Portale moduli](/help/forms/using/forms-portal-handling-user-data.md)
* [Gestione della corrispondenza](/help/forms/using/correspondence-management-handling-user-data.md)
* [Integrazione con Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Flussi di lavoro incentrati su Forms su OSGi](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Flussi di lavoro di Forms JEE](/help/forms/using/forms-workflow-jee-handling-user-data.md) (solo AEM Forms JEE)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (solo AEM Forms JEE)
* [Gestione utente](/help/forms/using/user-management-handling-user-data.md) (solo AEM Forms JEE)
