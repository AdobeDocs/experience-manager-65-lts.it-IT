---
title: Flusso di lavoro di installazione e aggiornamento per AEM Forms su JEE
description: Flusso di lavoro di installazione e aggiornamento per AEM Forms 6.5 LTS su JEE (JBoss), con un elenco consolidato dei PDF pertinenti e il loro scopo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 6d8c0e24-7f08-4e66-bb12-2cf1cfe1d5d3
source-git-commit: fb9f6ef794da7f3b242e9e81a6c2505692c16cd8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---


# Flusso di lavoro di installazione e aggiornamento per AEM Forms su JEE {#aem-forms-jee-installation-upgrade-documentation}

## Applicabile a {#applies-to}

Questa documentazione si applica a **AEM 6.5 LTS Forms**.

Utilizza il flusso di lavoro e le tabelle seguenti per scegliere le guide corrette per lo scenario. Alcuni documenti vengono pubblicati in formato PDF. È possibile aggiungere altri documenti nel tempo non appena diventano disponibili.

## Installazione e aggiornamento del flusso di lavoro {#installation-upgrade-workflow}

1. Rivedi [Piattaforme supportate per AEM Forms su JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) e assicurati che il tuo sistema soddisfi le combinazioni software/hardware richieste.
2. Decidi se stai eseguendo una **nuova installazione** o un **aggiornamento**.
3. Per il percorso scelto, segui la sequenza descritta di seguito (alcuni scenari richiedono più di una guida).

## Passaggi di preinstallazione e pre-aggiornamento {#start-here}

| Guida | Descrizione |
| --- | --- |
| [Piattaforme supportate per AEM Forms su JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) | Elenca le combinazioni software e hardware supportate per AEM Forms su JEE. Utilizzare questa opzione per convalidare i prerequisiti prima di iniziare un&#39;installazione o un aggiornamento. |
| [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md) | Vengono illustrate le architetture e le topologie di distribuzione consigliate per consentire di scegliere un approccio che corrisponda all&#39;ambiente (ad esempio, server singolo e cluster). |
| [Scelta di un tipo di persistenza per un&#39;installazione di AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | Consente di selezionare un tipo di persistenza appropriato per la topologia di installazione prima di iniziare. |

## Come si installa Adobe Experience Manager Forms (AEM Forms) su JEE su JBoss? {#installing-aem-forms-jee-jboss}

### Tasto {#install-jee-jboss-turnkey}

| Guida | Descrizione |
| --- | --- |
| [Installazione e distribuzione di AEM Forms 6.5 LTS su JEE tramite JBoss Turnkey (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | Utilizza per **un&#39;installazione chiavi in mano** su JBoss. Questo documento fornisce istruzioni per l’installazione e la distribuzione di AEM Forms su JEE utilizzando la distribuzione JBoss chiavi in mano. |

### Server singolo (non chiavi in mano) {#install-jee-jboss-single-server}

| Guida | Descrizione |
| --- | --- |
| [Preparazione all&#39;installazione di AEM Forms (server singolo) (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | Utilizza **prima** di un&#39;installazione **nuova a server singolo (non chiavi in mano)**. In questo documento sono elencati i prerequisiti e i passaggi di preparazione dell’ambiente per installare AEM Forms su JEE in una topologia a server singolo. |
| [Installazione e distribuzione di AEM Forms in JEE per JBoss (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | Utilizza per **installazione e distribuzione dettagliate** di AEM Forms su JEE in JBoss (**non chiavi in mano**). Per le installazioni con un solo server, seguire questa guida **dopo** il completamento di *Preparazione all&#39;installazione di AEM Forms (server singolo)*. |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## Come posso aggiornare Adobe Experience Manager Forms (AEM Forms) su JEE su JBoss? {#upgrading-aem-forms-jee-jboss}

### Tasto {#upgrade-jee-jboss-turnkey}

| Guida | Descrizione |
| --- | --- |
| [Aggiornamento a AEM Forms 6.5 LTS su JEE per JBoss Turnkey (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | Utilizza per un **aggiornamento chiavi in mano**. Questo documento fornisce istruzioni per l’aggiornamento di un’installazione AEM Forms esistente su JEE JBoss chiavi in mano. |

### Server singolo {#upgrade-jee-jboss-single-server}

| Guida | Descrizione |
| --- | --- |
| [Preparazione all&#39;aggiornamento di AEM Forms (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | Utilizza **prima** di un **aggiornamento a server singolo**. Descrive come preparare l’ambiente prima dell’aggiornamento a AEM 6.5 LTS Forms. Si applica agli ambienti che eseguono AEM Forms su JEE in modalità di installazione a server singolo. |
| [Aggiornamento ad AEM Forms su JEE per JBoss (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | Utilizzare per la **procedura di aggiornamento dettagliata** su JBoss in modalità di installazione **server singolo**. Segui questa guida **dopo** aver completato *la preparazione all&#39;aggiornamento di AEM Forms*. |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* | -->

