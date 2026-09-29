---
title: Pacchetto di compatibilità
description: L’installazione del pacchetto di compatibilità in AEM Forms 6.5 LTS consente di utilizzare le risorse di Gestione della corrispondenza di AEM Forms 6.5 e versioni precedenti e i modelli e le pagine obsoleti dei moduli adattivi
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3a529a82-e2fd-423c-96c1-a5accc87775e
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 19%
---
# Pacchetto di compatibilità{#compatibility-package}

## Panoramica {#overview}

La comunicazione interattiva è l’approccio predefinito e consigliato per la creazione di comunicazioni con i clienti in AEM Forms 6.5 LTS. Per continuare a utilizzare lettere in AEM Forms 6.5 LTS, è necessario installare il [pacchetto di compatibilità AEMFD](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) più recente.

Il pacchetto di compatibilità AEMFD consente inoltre di [utilizzare le seguenti risorse da AEM Forms 6.5.22.0, 6.4, 6.3 e 6.2 in AEM Forms 6.5 LTS](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Frammenti del documento
* Lettere
* Dizionari dati
* Moduli adattivi: modelli e pagine obsoleti

Per ulteriori informazioni, vedere [Assets reso compatibile con AEM Forms 6.5 installando il pacchetto di compatibilità](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Aggiunta del supporto per risorse AEM Forms 6.5, 6.4, 6.3 e 6.2 in AEM Forms 6.5 LTS {#add-support-for-aem-forms-and-assets-in-aem-forms-6.5.lts}

Dopo aver eseguito un aggiornamento, effettua le seguenti operazioni per installare il pacchetto di compatibilità AEMFD e rendere le risorse compatibili con la versione 6.5:

Verifica che il [pacchetto di compatibilità di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) sia preinstallato.

1. Installa il pacchetto di compatibilità [AEM 6.5 LTS più recente](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

   Per ulteriori informazioni sul caricamento e l&#39;installazione del pacchetto, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md).

1. Una volta stabilizzati i registri, riavviare il server.
1. Utilizza l’utility di migrazione per rendere le risorse compatibili con 6.5 LTS.

   >[!NOTE]
   >
   > È consigliabile utilizzare il comando `Ctrl + C` per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

   Per ulteriori informazioni, vedere [utilità di migrazione](../../forms/using/migration-utility.md).

## Assets reso compatibile con AEM Forms 6.5 LTS installando il pacchetto di compatibilità {#assetsmadecompatible}

Installando il pacchetto di compatibilità, puoi rendere compatibili con AEM Forms 6.5 LTS le risorse e i modelli seguenti:

* Gestione della corrispondenza Assets da AEM 6.4 e versioni precedenti:

  * [Lettere](../../forms/using/create-letter.md)
  * [Dizionari dati](/help/forms/using/data-dictionary.md)
  * Frammenti del documento

* Modelli obsoleti per moduli adattivi:

  * /libs/fd/af/templates/blankTemplate2
  * /libs/fd/af/templates/simpleEnrollmentTemplate
  * /libs/fd/af/templates/simpleEnrollmentTemplate2
  * /libs/fd/af/templates/surveyTemplate
  * /libs/fd/af/templates/surveyTemplate2
  * /libs/fd/af/templates/tabbedEnrollmentTemplate
  * /libs/fd/af/templates/tabbedEnrollmentTemplate2
  * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
  * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Pagine obsolete dei moduli adattivi:

  * /libs/fd/af/components/page/survey
  * /libs/fd/af/components/page/tabbedenrollment
  * /libs/fd/afaddon/components/page/advancedenrollment
