---
title: Configurazione per le app AEM
description: Scopri come utilizzare le app Adobe Experience Manager per aggiornare il contenuto dell’OTA dell’applicazione (over the air).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
exl-id: 4f36487c-45a2-4c18-b3cc-bb9284d68f49
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# Configurazione per le app AEM{#configuring-for-aem-apps}

Le app Adobe Experience Manager ti consentono di aggiornare il contenuto dell’OTA dell’applicazione (via etere). Il contenuto aggiornato viene archiviato nell’istanza di pubblicazione. Per consentire all’app sul dispositivo di connettersi all’istanza Publish e di verificare la disponibilità di aggiornamenti, l’istanza Publish deve essere configurata in modo da consentire l’utilizzo di un’intestazione referente vuota.

## Configurazione di un’intestazione di riferimento vuota {#configuring-empty-referrer-header}

Per configurare il servizio filtro referenti:

* Apri la console Apache Felix (**Configurazioni**) in:
* https://&lt;server>:&lt;numero_porta>/system/console/configMgr
* Accedi come amministratore.
* Nel menu **Configurazioni**, seleziona: *Filtro referrer Apache Sling*
* Seleziona il campo Consenti vuoto per consentire intestazioni referente vuote/mancanti.
* Fai clic su **Salva** per salvare le modifiche.

![chlimage_1-58](assets/chlimage_1-58a.png)

Per ulteriori dettagli, vedi [Impostazioni configurazione OSGI](/help/sites-deploying/osgi-configuration-settings.md) e [Elenco di controllo sicurezza - Problemi relativi a false richieste tra siti](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).
