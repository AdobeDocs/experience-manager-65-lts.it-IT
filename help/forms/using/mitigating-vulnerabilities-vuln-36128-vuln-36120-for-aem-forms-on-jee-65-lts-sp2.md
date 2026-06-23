---
title: Mitigazione delle vulnerabilità VULN-36128 e VULN-36120 per AEM Forms su JEE 6.5 LTS SP2
description: Passaggi di mitigazione per le implementazioni VULN-36128 e VULN-36120 su AEM Forms su JEE 6.5 LTS Service Pack 2 in esecuzione su JBoss.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1b876f20cbc3a00a02a4449f0d353fb858695235
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---

# Mitigazione delle vulnerabilità VULN-36128 e VULN-36120 per AEM Forms su JEE 6.5 LTS SP2

## Riferimento rapido {#quick-reference}

| Livello di impatto | Versioni interessate | Azione consigliata |
| --- | --- | --- |
| Critico | AEM Forms su JEE 6.5 LTS Service Pack 2 (6.5 LTS SP2) | Installa manualmente [hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear) |
| Non interessato | AEM Forms su OSGi, Workbench, Cloud Service | Nessuna azione richiesta |

**Vulnerabilità risolte:**

* **VULN-36128**: vulnerabilità di esecuzione del codice remoto che consente a utenti non autorizzati che eseguono attacchi remoti di eseguire codice arbitrario.
* **VULN-36120**: vulnerabilità di convalida dell&#39;input non corretta che potrebbe consentire l&#39;accesso non autorizzato a informazioni riservate.

## Passaggi di mitigazione {#mitigation-steps}

### Prima di iniziare {#before-you-start}

Prima di apportare qualsiasi modifica, eseguire il backup del file EAR che si sta per sostituire:

* Individuare `adobe-edcserver-jboss.ear` nella directory di distribuzione:

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* Copiare il file in un percorso di backup protetto all&#39;esterno della directory di distribuzione.
* Prima di procedere con gli aggiornamenti, verificare che il backup sia completo e accessibile.

Questa precauzione ti consente di ripristinare lo stato originale se riscontri problemi durante il processo di aggiornamento.

### Installazione manuale di hotfix per AEM Forms su JEE 6.5 LTS SP2 (JBoss) {#manual-hotfix-installation-aem-forms-jee-65-lts-sp2-jboss}

1. Scarica `adobe-edcserver-jboss.ear` dal [portale di distribuzione software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear).

1. Individuare `adobe-edcserver-jboss.ear` nella directory di distribuzione e sostituirlo con il file scaricato:

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. Avvia AEM Forms Configuration Manager per ridistribuire l’EAR aggiornato e applicare completamente la patch.

1. Riavviare il server applicazioni e confermare la corretta distribuzione dai registri del server.

## Riferimenti {#references}

* [Best practice per la sicurezza Adobe Experience Manager Forms](/help/forms/using/hardening-securing-aem-forms-environment.md)
