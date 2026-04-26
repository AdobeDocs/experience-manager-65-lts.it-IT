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
hidefromtoc: true
exl-id: d19b7265-42cc-41d9-9897-e7b044c4529c
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 100%

---

# Configurazione degli endpoint di comunicazione remota {#configuring-remoting-endpoints}

Un endpoint di comunicazione remota consente a un’applicazione creata con Flex di richiamare il servizio utilizzando (obsoleto per AEM Forms) moduli AEM di comunicazione remota. Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell’endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

## Impostazioni endpoint di comunicazione remota {#remoting-endpoint-settings}

**Metodo di autenticazione client Flex:** determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la sicurezza, l’operazione richiamata non supporta chiamate anonime e il client non trasmette credenziali o le trasmette non valide.
