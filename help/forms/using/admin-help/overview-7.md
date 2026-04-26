---
title: Nozioni di base sulla configurazione dei moduli
description: Scopri i vari servizi di moduli che ti consentono di creare applicazioni di acquisizione dati interattive.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 68e43842-cba9-47b8-b7a3-6f625dbfca08
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---

# Nozioni di base sulla configurazione dei moduli {#basics-of-configuring-forms}

Il servizio Forms consente di creare applicazioni client di acquisizione dati interattive per la convalida, il processo, la trasformazione e la distribuzione di moduli generalmente creati in Designer. Gli autori dei moduli sviluppano una singola progettazione di moduli che il servizio Forms esegue in vari formati:

* come PDF in Adobe Reader o in un browser
* come HTML in vari ambienti di browser, tra cui un rendering XHTML 1.0 conforme
* come guide per moduli in vari ambienti del browser che supportano Adobe Flash Player.

Per ulteriori informazioni sul servizio Forms, consulta [Riferimento ai servizi](https://www.adobe.com/go/learn_aemforms_services_63).

Utilizzando la pagina Forms nella console di amministrazione, puoi configurare il comportamento del servizio Forms. Queste impostazioni si applicano a tutte le chiamate del servizio. Tutti i parametri inviati tramite l’SDK di AEM Forms sostituiscono le impostazioni configurate nella console di amministrazione; tuttavia, influiscono solo su tale chiamata particolare.

Dopo aver modificato le impostazioni di Forms nella console di amministrazione, fai clic su Salva. Non è necessario riavviare il server per rendere effettive le modifiche. Tuttavia, potrebbe essere necessario interrompere e riavviare il servizio Forms durante la configurazione delle impostazioni della modalità cache (consulta [Avvio e interruzione dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
