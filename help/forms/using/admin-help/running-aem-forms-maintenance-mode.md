---
title: Esecuzione di AEM Forms in modalità manutenzione
description: La modalità di manutenzione è utile quando si eseguono attività quali l’applicazione di patch a un DSC, l’aggiornamento di AEM Forms o l’applicazione di un service pack. Ulteriori informazioni sull’esecuzione di AEM Forms in modalità manutenzione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: d4cfe1c1-8b44-4bd5-b6ec-29e5f70f0674
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Esecuzione di AEM Forms in modalità manutenzione {#running-aem-forms-in-maintenance-mode}

La modalità di manutenzione è utile quando si eseguono attività quali l’applicazione di patch a un DSC, l’aggiornamento di AEM Forms o l’applicazione di un service pack.

Evita di richiamare i processi mentre il server è in modalità di manutenzione. Questo è ciò che accade se un processo viene richiamato mentre il server è in modalità di manutenzione:

* Se il processo è di lunga durata, viene aggiunto al database dei processi, ma non viene avviato. Quando si esce dalla modalità di manutenzione, AEM Forms elabora i processi di lunga durata presenti nella coda, anche se il server è stato riavviato in modalità di manutenzione.
* Se il processo è di breve durata, viene elaborato immediatamente.

**Metti AEM Forms in modalità manutenzione**

1. In un browser web, immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato il messaggio &quot;ora in pausa&quot;.

   >[!NOTE]
   >
   >Se si arresta il server mentre è in modalità di manutenzione, al riavvio il server è ancora in modalità di manutenzione. Disattivare la modalità di manutenzione al termine delle attività di manutenzione.

**Verificare se AEM Forms è in esecuzione in modalità di manutenzione**

1. In un browser web, immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   Lo stato viene visualizzato nella finestra del browser. Lo stato &quot;true&quot; indica che il server è in esecuzione in modalità di manutenzione, mentre &quot;false&quot; indica che il server non è in modalità di manutenzione.

**Disattiva modalità di manutenzione**

1. In un browser web, immetti:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Nella finestra del browser viene visualizzato il messaggio &quot;in esecuzione&quot;.
