---
title: Problemi di connessione con i servizi DoR di output, Forms e (documento di record)
description: Risolvere gli errori di connessione di AEM Forms dopo SP19. Arrestare, installare Microsoft Visual C++, riavviare il server per una soluzione ottimale. Risolvere i problemi relativi ai servizi Output, Forms e DoR.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
hide: true
removedfrom6.5.2025: 'yes'
exl-id: c84ba536-a78d-4cf9-a480-59cb18e41076
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
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 26%
---
# Impossibile utilizzare il servizio di output, il servizio Forms o il servizio Document of Record (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problema

Dopo aver installato AEM Forms 6.5 Service Pack 19, il tentativo di utilizzare il servizio di output, il servizio Forms o il servizio Document of Record (DoR) potrebbe causare un errore `Connection to failed service`.

## Soluzione

Per risolvere il problema:

1. Arresta l’istanza Forms di AEM 6.5.
1. Scaricare e installare la versione a [64 bit dei pacchetti ridistribuibili di Microsoft Visual C++ per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) nel computer in cui è installato AEM 6.5 Forms.
1. Riavvia il server AEM Forms.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.


>[!NOTE]
>
>
> Assicurati di installare Redistributable anche se è installata una versione precedente.
