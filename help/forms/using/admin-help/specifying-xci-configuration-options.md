---
title: Specificare le opzioni di configurazione XCI
description: Scopri come specificare le opzioni di configurazione XCI. Puoi specificare i valori di un file XCI personalizzato per il modulo adattivo, che verrà utilizzato per il rendering del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 198016d7-0fb5-47e6-91ed-f2f0c98b2224
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
source-wordcount: '161'
ht-degree: 90%
---
# Specificare le opzioni di configurazione XCI {#specifying-xci-configuration-options}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I moduli ti consentono di specificare un file XCI personalizzato da utilizzare per il rendering. (Consulta [Configurare le posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Per impostazione predefinita, Forms ignora alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puoi selezionare opzioni che annullano la sostituzione delle opzioni elencate qui sopra, nel qual caso i moduli utilizzano i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fai clic su **Servizi** > **Moduli**.
1. Seleziona o deseleziona la casella di controllo Usa le opzioni XCI predefinite di sistema. Quando questa opzione è selezionata, i moduli utilizzano valori predefiniti per le impostazioni packets, creator, producer e compressObjectStream. Quando questa opzione è deselezionata, i moduli utilizzano i valori specificati nel file XCI personalizzato.
1. Fai clic su **Salva**.
