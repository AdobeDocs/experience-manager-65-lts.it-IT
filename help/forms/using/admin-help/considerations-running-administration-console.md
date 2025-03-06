---
title: Considerazioni durante l’esecuzione di Administration Console
description: In questo documento sono elencati alcuni punti da considerare durante l'esecuzione di Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: bdd884c4-ae12-4827-8251-01033cbc0185
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Considerazioni durante l’esecuzione di Administration Console {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Di seguito sono riportati alcuni aspetti da considerare durante l’esecuzione di Administration Console:

* Se si accede alla console di amministrazione utilizzando l&#39;URL `https://[hostname]:'port'/adminui`, il nome host specificato non può contenere caratteri di sottolineatura. In caso contrario, i collegamenti ad alcune aree della console di amministrazione potrebbero non funzionare correttamente.
* Se si esegue una console di amministrazione in Esplora risorse su un sistema operativo giapponese, è possibile che si verifichino i seguenti problemi:

   * Facendo clic su un collegamento si ritorna alla pagina di accesso anziché al collegamento previsto.
   * Quando si fa clic su un collegamento, viene visualizzato un errore di autorizzazione.

  La best practice prevede di eseguire la console di amministrazione da un altro browser, come Mozilla Firefox, per garantire che nessun collegamento non riesca.

* Non utilizzare i caratteri barra rovesciata () durante l’esecuzione di ricerche nella console di amministrazione.
