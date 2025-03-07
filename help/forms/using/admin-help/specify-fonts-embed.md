---
title: Specificare i font da incorporare
description: Scopri come specificare i font da incorporare in un modulo adattivo. È possibile specificare i tipi di carattere incorporati o mai incorporati con i moduli generati dal servizio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 374f9425-b596-4481-8fd0-6df07c521a19
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Specificare i font da incorporare{#specify-fonts-to-embed}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

È possibile specificare quali tipi di carattere devono essere sempre incorporati o non incorporati con i moduli utilizzati dall&#39;output. L&#39;incorporamento di caratteri aumenta le dimensioni dei file dei moduli. Incorpora font insoliti che gli utenti non avranno probabilmente sui loro sistemi e non incorpora font comuni che avranno installato.

>[!NOTE]
>
>Se è stato specificato un file XCI personalizzato per l&#39;output, l&#39;opzione incorpora font nel file XCI ignora queste impostazioni. (Vedi [Specificare i percorsi dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Nella console di amministrazione, fai clic su Servizi > output.
1. Nella casella Incorpora sempre caratteri della casella Impostazioni incorporamento caratteri digitare i nomi dei caratteri da incorporare con i moduli, separati da virgole. I tipi di carattere specificati vengono incorporati nel modulo generato solo se vengono utilizzati nel modulo. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata attivata nel file XCI passato al servizio. In tal caso, tutti i font utilizzati in PDF sono sempre incorporati.
1. Nella casella Non incorporare mai i tipi di carattere digitare i nomi dei tipi di carattere da non incorporare con i moduli, separati da virgole. I tipi di carattere specificati non vengono incorporati in PDF, anche se vengono utilizzati nel PDF generato. Questa impostazione viene ignorata se l&#39;opzione incorpora font è stata disattivata nel file XCI passato al servizio. In tal caso, nessuno dei tipi di carattere utilizzati in PDF è incorporato.
1. Fai clic su Salva.
