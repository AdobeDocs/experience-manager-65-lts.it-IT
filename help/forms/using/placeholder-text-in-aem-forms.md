---
title: Testo segnaposto in AEM Forms
description: Il testo segnaposto ha lo scopo di aiutare l'utente a immettere dati quando il controllo non contiene alcun valore. Potrebbe essere un valore di esempio o una breve descrizione del formato previsto.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 85ea442a-6e92-4fa8-aa0a-3076aac6f134
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 1%

---

# Testo segnaposto in AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Il testo segnaposto rappresenta una parola o una breve frase. Lo scopo è quello di aiutare l&#39;utente a inserire dati quando il controllo non ha valore. Un testo segnaposto può essere un valore di esempio o una breve descrizione del formato previsto. Il testo segnaposto viene visualizzato prima che l’utente immetta un valore, viene rimosso quando l’utente immette o seleziona un valore.

>[!NOTE]
>
>Il testo segnaposto, se specificato, deve avere un valore che non contenga caratteri di riga nuovi.

![Componente data con e senza testo segnaposto](assets/dat-picker-place-holder-text.png)

**A.** Componente data con testo segnaposto **B.** Componente data senza testo segnaposto

AEM Forms supporta il testo segnaposto per i campi casella Password, selettore data, casella Numerica e casella di testo.\
I testi segnaposto non sono supportati per il widget data HTML5 nativo. Per specificare un testo segnaposto:

1. Fare clic con il pulsante destro del mouse su un componente che supporta il testo segnaposto e scegliere **Modifica**. Viene visualizzata la finestra di dialogo Modifica componente.

1. Apri la scheda **Titolo e testo**.
1. Specificare una parola o una breve frase nella **casella di testo Segnaposto**. Fai clic su **OK**.

>[!NOTE]
>
>Testo segnaposto non supportato in Microsoft Internet Explorer 9.
