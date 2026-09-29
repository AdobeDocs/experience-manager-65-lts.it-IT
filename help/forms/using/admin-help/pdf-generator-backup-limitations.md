---
title: Limitazioni del backup di PDF Generator
description: Scopri le limitazioni del backup di PDF Generator. Non puoi eseguire il backup della directory temporanea utilizzata da PDF Generator poiché questo cancella il contenuto a intervalli impostati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: f76ce3be-6d50-4531-a982-2e902f866208
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
source-wordcount: '73'
ht-degree: 100%
---
# Limitazioni del backup di PDF Generator {#pdf-generator-backup-limitations}

Non puoi eseguire il backup della directory temporanea utilizzata da PDF Generator per convertire i file. Anche se il servizio viene ripristinato correttamente, i dati possono andare persi perché PDF Generator rivede e cancella il contenuto della directory temporanea a intervalli impostati.
