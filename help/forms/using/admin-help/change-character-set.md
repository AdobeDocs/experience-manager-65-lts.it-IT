---
title: Modificare il set di caratteri
description: Puoi specificare il set di caratteri utilizzato per codificare il flusso di output. Scopri come modificare il set di caratteri.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 1d614736-5897-4fd3-9ca4-94b115139ba3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# Modificare il set di caratteri {#change-the-character-set}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi specificare il set di caratteri utilizzato per codificare il flusso di output.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > output]**.
1. In Internazionalizzazione selezionare un set di caratteri nell&#39;elenco Set di caratteri. Questa impostazione dipende da `TransformationFormat` e `PrintFormat` specificati tramite l&#39;API. Per specificare un set di caratteri diverso da quelli elencati, selezionare Personalizzato e specificare un valore di codifica nella casella visualizzata.

   Se `TransformationFormat` è PDF e PDF/A o `PrintFormat` è PCL, PostScript, etichetta Zebra, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, sono supportati solo set di caratteri specifici.

   Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su **[!UICONTROL Salva]**.
