---
title: Mitigazione delle vulnerabilità SSRF (Server-Side Request Forgery) per AEM Forms in JEE 6.5 LTS SP2
description: Passaggi di mitigazione per le vulnerabilità SSRF (Server-Side Request Forgery) nelle implementazioni di AEM Forms su JEE 6.5 LTS Service Pack 2 in esecuzione su JBoss.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1d825cd821609504c5e2cff7f7002bf3afe30434
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%

---

# Mitigazione delle vulnerabilità SSRF (Server-Side Request Forgery) per AEM Forms in JEE 6.5 LTS SP2

## Riferimento rapido {#quick-reference}

| Livello di impatto | Versioni interessate | Azione consigliata |
| --- | --- | --- |
| Critico | AEM Forms su JEE 6.5 LTS Service Pack 2 (6.5 LTS SP2) | Installa manualmente [hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| Non interessato | AEM Forms su OSGi, Workbench, Cloud Service | Nessuna azione richiesta |

**Vulnerabilità risolte:**

* SSRF (Server-Side Request Forgery) (CWE-918)

## Panoramica {#overview}

### Che cosa è interessato {#whats-affected}

| Vulnerabilità | Impatto | Componenti interessati |
| --- | --- | --- |
| SSRF (Server-Side Request Forgery) (CWE-918) | Gli aggressori possono indurre il server a effettuare richieste non intenzionali a risorse interne o esterne | AEM Forms su JEE 6.5 LTS SP2 |

### Cosa non viene interessato {#whats-not-affected}

* Experience Manager Forms Workbench (tutte le versioni)
* Experience Manager Forms su OSGi (tutte le versioni)
* Experience Manager Forms as a Cloud Service

## Opzioni di risoluzione {#resolution-options}

### Prima di iniziare {#before-you-start}

Prima di apportare qualsiasi modifica, eseguire una copia di backup del file EAR che si sta per sostituire:

* Individuare `adobe-edcserver-jboss.ear` nella directory di distribuzione:

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* Copiare il file in un percorso di backup protetto all&#39;esterno della directory di distribuzione.
* Prima di procedere con gli aggiornamenti, verificare che il backup sia completo e accessibile.

Questa precauzione ti consente di ripristinare lo stato originale nel caso in cui si verifichino problemi durante il processo di aggiornamento.

### Installazione manuale di hotfix per AEM Forms su JEE 6.5 LTS SP2 (JBoss)

1. Scarica `adobe-edcserver-jboss.ear` dal [portale di distribuzione software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear).

1. Individuare `adobe-edcserver-jboss.ear` nella directory di distribuzione e sostituirlo con il file scaricato:

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. Avvia AEM Forms Configuration Manager per ridistribuire l’EAR aggiornato e applicare l’hotfix.

1. Riavviare il server applicazioni e confermare la corretta distribuzione dai registri del server.

## Riferimento {#references}

* [Best practice per la sicurezza di Adobe Experience Manager Forms](/help/forms/using/hardening-securing-aem-forms-environment.md)
