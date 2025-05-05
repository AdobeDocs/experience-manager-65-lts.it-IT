---
title: Attivazione della protezione hotlinking in Dynamic Media
description: Informazioni su come attivare la protezione hotlink in Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
feature: Configuration
solution: Experience Manager, Experience Manager Assets
exl-id: 56eb956e-c6a8-464b-980a-28e0dab0da7c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Attivare la protezione hotlinking in Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Il collegamento rapido si verifica quando un sito web di terze parti utilizza il codice HTML per visualizzare un’immagine dal sito web. Utilizzano la larghezza di banda ogni volta che l&#39;immagine viene richiesta, perché il browser del visitatore vi accede direttamente dal server. Hotlink *protezione* è un metodo per impedire ad altri siti Web di collegarsi direttamente a immagini, CSS o JavaScript nelle pagine Web. Questo tipo di schermatura consente di ridurre l’utilizzo di larghezza di banda non necessaria nell’account Dynamic Media.

[L&#39;Assistenza clienti Experience Manager](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&amp;lang=it#support) può configurare un filtro referente a livello CDN (Content Delivery Network) in modo che il contenuto di Dynamic Media venga distribuito solo ai siti Web inclusi nell&#39;elenco dei siti Web consentiti per il dominio.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione. Per attivare la protezione hotlink, un amministratore deve creare un ticket all’Assistenza clienti di Adobe per richiedere la modifica della configurazione dell’account Dynamic Media. L&#39;attivazione della protezione hotlink non comporta costi aggiuntivi.
