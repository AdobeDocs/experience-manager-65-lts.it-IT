---
title: Riconoscimento di certificati validi e scaduti nei documenti di PDF
description: Scopri come riconoscere i certificati validi e scaduti nei documenti di PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Riconoscimento di certificati validi e scaduti nei documenti di PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando un documento PDF con diritti di utilizzo applicati dalle estensioni Reader viene aperto in Adobe Reader, viene visualizzata una barra di stato che descrive i diritti di utilizzo specifici abilitati nel documento PDF.

Quando il certificato digitale che specifica i diritti di utilizzo per un documento PDF scade e il documento PDF viene aperto in Adobe Reader, una finestra di dialogo informa l&#39;utente che il documento PDF dispone di diritti di utilizzo, ma tali diritti sono disabilitati. Sebbene il messaggio indichi che il documento PDF è stato alterato o manomesso, ciò non avviene necessariamente. Adobe Reader visualizza questo messaggio quando un certificato scade o un documento viene modificato. In Adobe Reader 7.0.x o versione successiva, non è possibile determinare quale caso sia attualmente il problema.

Dopo aver chiuso la finestra di dialogo, Adobe Reader apre il documento PDF. I diritti di utilizzo applicati mediante le estensioni di Acrobat Reader DC non sono disponibili, come previsto. Se il documento di PDF è un modulo interattivo, i campi del modulo sono bloccati e l’utente non può modificare i dati del modulo.
