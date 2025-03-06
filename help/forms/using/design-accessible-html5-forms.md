---
title: Progettazione di moduli HTML5 accessibili
description: I moduli HTML5 utilizzano lo standard di accessibilità ARIA HTML5. Questi moduli supportano la navigazione a schede e sono certificati per la compatibilità con le utilità per la lettura dello schermo più comuni.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 9a23dc13-48e4-44dc-b601-10fa0d56cbc8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Progettazione di moduli HTML5 accessibili {#designing-accessible-html-forms}

I moduli HTML5 utilizzano lo standard di accessibilità ARIA HTML5 per generare moduli HTML accessibili. Questi moduli supportano la navigazione a schede (ad eccezione di Mozilla FireFox) e sono certificati per essere compatibili con gli assistenti vocali comuni. Per generare un modulo HTML5 con buone funzioni di accessibilità, progettare il modello di modulo XFA in base ad alcune linee guida di progettazione di base. Le linee guida per la progettazione includono la configurazione dell&#39;ordine di tabulazione corretto e la fornitura del contenuto Testo parlato per ogni controllo modulo. AEM Forms Designer supporta l’impostazione di questi attributi di controllo modulo per generare un modulo PDF e HTML5 accessibile.

*Nota: la navigazione a schede non copre i campi protetti, ad esempio i campi di calcolo che visualizzano la somma dei valori. Affinché l’assistente vocale possa leggere il valore di un campo protetto, inserisci un campo di sola lettura vuoto sopra o accanto al campo protetto. Assegnare il valore del campo protetto al nuovo campo di sola lettura. L&#39;utilità di lettura dello schermo o la navigazione a schede può scegliere questo campo di sola lettura e indicarlo come valore del campo protetto.*

AEM Forms Designer include diverse opzioni Speak Text che possono essere trasmesse agli assistenti vocali. Per ogni oggetto di un modulo, l’utente può specificare una delle diverse impostazioni per il testo dell’assistente vocale:

* Testo personalizzato dell&#39;utilità di lettura dello schermo, che può essere impostato utilizzando la tavolozza Accessibilità. Gli autori possono annotare i nomi di pulsanti e campi e il relativo scopo.
* Descrizioni comandi che possono essere impostate nella tavolozza Accessibilità.
* Sottotitoli per i campi del modulo.
* Nomi di oggetti, come specificato nell&#39;opzione Nome della scheda Associazione.

![accessibilità](assets/accessibility.png)

Quando in un controllo Modulo sono disponibili più opzioni quali descrizione comando, Testo Reader schermo e Didascalia, il Reader schermo utilizza solo una di queste proprietà. L&#39;ordine predefinito è Testo Reader schermo personalizzato, descrizione comando, Didascalia e Nome. È possibile modificare l&#39;ordine predefinito utilizzando l&#39;opzione Screen Reader **Precedence** nella tavolozza Accessibilità.
