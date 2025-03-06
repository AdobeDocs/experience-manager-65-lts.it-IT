---
title: Impossibile aprire PDF forms basato su XFA in Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
description: Impossibile aprire PDF forms basato su XFA in Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
feature: Adaptive Forms,Document Services
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: a28b084e-ec74-4c05-a90c-d447792faa41
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Impossibile aprire PDF forms basato su XFA in Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer o Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Molte versioni recenti del browser hanno incluso il proprio supporto limitato per PDF forms basato su XFA. Anche se questi browser possono aprire PDF forms basato su XFA, le funzionalità fornite sono limitate. Se non riesci ad aprire o inviare un modulo PDF basato su XFA in un browser moderno, utilizza uno dei seguenti metodi:

* Utilizza [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) o [Adobe® Adobe® Reader®](https://get.adobe.com/reader/), versione 8 o successiva per aprire e inviare PDF forms basato su XFA.
* Acrobat e Reader, su Microsoft® Windows®, consentono di configurare per aprire i PDF in modalità Visualizzazione protetta, che impedisce l’apertura di PDF forms basato su XFA. Assicurati che la modalità Visualizzazione protetta nell’Acrobat o nel Reader sia disabilitata. Per ulteriori informazioni, vedere [Visualizzazione protetta (solo Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Per sviluppatori Forms) Adobe Experience Manager Forms fornisce anche supporto per:

   * [esegui il rendering di moduli basati su XFA in HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65-lts/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) in modo che i moduli possano essere aperti in browser con supporto HTML5, inclusi i browser in esecuzione su dispositivi mobili come iPad. La rappresentazione HTML5 dei moduli mantiene il layout della struttura del modulo e supporta la maggior parte delle logiche del modulo (come JavaScript, calcolo dei moduli e convalide dei moduli) incorporate nel modello di modulo XFA.
   * [convertire i moduli basati su XFA in Forms adattivo reattivo per dispositivi mobili](https://experienceleague.adobe.com/docs/experience-manager-65-lts/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Questi moduli forniscono un layout dinamico, funzionalità di personalizzazione e si adattano dinamicamente alle risposte degli utenti aggiungendo o rimuovendo campi o sezioni secondo necessità. Forniscono inoltre connettori predefiniti per varie origini dati, funzionalità per documenti di record e una facile connessione ad Adobe Analytics per la valutazione delle prestazioni. Per ulteriori informazioni, vedere [Funzionalità e funzionalità chiave](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)
In questo modo, gli investimenti tecnologici nei moduli XFA sono protetti e continuano a fornire un’esperienza ottimale agli utenti finali. Per ulteriori informazioni, consulta [Documentazione del prodotto Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
