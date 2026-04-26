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
hidefromtoc: true
exl-id: 198016d7-0fb5-47e6-91ed-f2f0c98b2224
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
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
