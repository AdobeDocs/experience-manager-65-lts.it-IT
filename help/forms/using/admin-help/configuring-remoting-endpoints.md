---
title: Configurazione degli endpoint di comunicazione remota
description: Scopri come configurare gli endpoint di comunicazione remota Questo documento spiega come abilitare l’applicazione creata con Flex per richiamare il servizio utilizzando moduli AEM di comunicazione remota.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: d19b7265-42cc-41d9-9897-e7b044c4529c
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 100%
---
# Configurazione degli endpoint di comunicazione remota {#configuring-remoting-endpoints}

Un endpoint di comunicazione remota consente a un’applicazione creata con Flex di richiamare il servizio utilizzando (obsoleto per AEM Forms) moduli AEM di comunicazione remota. Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell’endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

## Impostazioni endpoint di comunicazione remota {#remoting-endpoint-settings}

**Metodo di autenticazione client Flex:** determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la sicurezza, l’operazione richiamata non supporta chiamate anonime e il client non trasmette credenziali o le trasmette non valide.
