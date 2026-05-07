---
title: Impostazione delle opzioni di internazionalizzazione
description: Scopri come specificare le impostazioni della lingua utilizzate per il rendering dei moduli e come specificare il set di caratteri utilizzato per codificare il flusso di output.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: 47a49147-2921-4d28-8d04-2281c0b9a190
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%

---

# Impostazione delle opzioni di internazionalizzazione{#setting-internationalization-options}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

## Specificare la lingua utilizzata per il rendering dei moduli {#specify-the-locale-used-to-render-forms}

Puoi specificare la lingua utilizzata per il rendering di un modulo di PDF. I campi di un modulo di PDF utilizzano la lingua specificata per la visualizzazione dei dati. Se, ad esempio, la lingua è confugurata sul tedesco, per i valori numerici verranno utilizzati i separatori decimali tedeschi. La lingua viene utilizzata anche per inviare messaggi di convalida ai dispositivi client, ad esempio i browser web, come parte delle trasformazioni HTML.

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. Nell’elenco Lingua in Internazionalizzazione seleziona la lingua utilizzata per il rendering di un modulo. Il valore predefinito è Inglese (Stati Uniti).
1. Fai clic su Salva.

## Specificare il set di caratteri utilizzato per codificare il flusso di output {#specify-the-character-set-used-to-encode-the-output-stream}

1. Seleziona un set di caratteri sell’elenco Set di caratteri in Internazionalizzazione. Questa impostazione dipende dall’API utilizzata, renderHTMLForm o renderPDFForm. Per specificare un set di caratteri diverso da quelli elencati, seleziona Personalizzato e specifica un valore di codifica nella casella visualizzata.

   Per le trasformazioni HTML, AEM Forms supporta i valori di codifica dei caratteri definiti dal pacchetto `java.nio.charset`. Se sFormPreference è PDFForm, sono supportati solo set di caratteri specifici. Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su Salva.
