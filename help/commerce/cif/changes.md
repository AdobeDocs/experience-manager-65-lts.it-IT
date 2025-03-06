---
title: Modifiche di rilievo del componente aggiuntivo Commerce integration framework (CIF)
description: Modifiche di rilievo del componente aggiuntivo Commerce integration framework (CIF) rispetto alle versioni precedenti di CIF.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: aced89a0-dec1-49fe-afbc-3ddf1318b900
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce integration framework (CIF){#notable-changes}

Questo documento evidenzia le differenze importanti tra il componente aggiuntivo Commerce integration framework (CIF) e le versioni precedenti di CIF, principalmente note come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il pacchetto del componente aggiuntivo AEM CIF viene installato e aggiornato con AEM Package Manager.

**Versioni precedenti di CIF**

* CIF Classic: non è necessaria alcuna installazione, CIF faceva parte di Quickstart. Gli aggiornamenti di CIF facevano parte dei normali aggiornamenti di AEM o service pack
* CIF Open-source: installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato tramite la console OSGi.

**Versioni precedenti di CIF**

* CIF Classic: tramite la configurazione OSGi in AEM
* CIF Open-source: tramite browser configurazioni CIF

## Implementazione del progetto CIF Venia

Progetto disponibile su [AEM Guides GitHub - Progetto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e distribuzione eseguita tramite Gestione pacchetti AEM.

**Versioni precedenti di CIF**

* CIF Classic: tramite l’installazione del pacchetto AEM

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni precedenti di CIF**

* CIF Classic: i dati di prodotto live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione di prodotti completa o delta. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze nel catalogo dei prodotti con rendering AEM

AEM esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni precedenti di CIF**

* CIF Classic: AEM Author crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare CIF con AEM Managed Service o AEM On-Premise, vedi [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
