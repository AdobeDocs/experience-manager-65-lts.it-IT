---
title: Strategia di backup per il connettore per gli utenti di EMC Documentum&reg;
description: Verificare come creare una strategia di backup per Connector per gli utenti di EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 019e1a9b-c26c-429f-8153-fceeb85f7096
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 85%
---
# Strategia di backup del connettore per gli utenti di EMC Documentum® {#backup-strategy-for-connector-for-emc-documentum-users}

Se hai installato il connettore per EMC Documentum®, oltre alle istruzioni riportate in questo capitolo, la strategia di backup e ripristino deve includere il backup (o il ripristino) del computer su cui è installato il sistema ECM. (Consulta la documentazione di ECM Documentum®).

Esegui il backup dell’ambiente AEM Forms utilizzando l’archivio ECM e procedendo con le attività seguenti:

* Eseguire il backup di AEM Forms seguendo le istruzioni presenti in questo documento.
* Eseguire il backup del sistema ECM Documentum® seguendo le istruzioni riportate in [Backup del server di gestione dei contenuti EMC Documentum®](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Ripristina l’ambiente AEM Forms utilizzando l’archivio ECM e procedendo con le seguenti attività:

* Ripristinare il proprio sistema ECM seguendo le istruzioni in [Ripristino del server di gestione dei contenuti EMC Documentum®](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Ripristinare AEM Forms seguendo le istruzioni presenti in questo documento.
