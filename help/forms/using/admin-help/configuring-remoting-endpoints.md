---
title: Configurazione degli endpoint di comunicazione remota
description: Scopri come configurare gli endpoint remoti. Questo documento spiega come abilitare l’applicazione creata con Flex per richiamare il servizio utilizzando AEM Forms Remoting.
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
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# Configurazione degli endpoint di comunicazione remota {#configuring-remoting-endpoints}

Un endpoint remoto consente a un’applicazione creata con Flex di richiamare il servizio utilizzando (obsoleto per AEM Forms) AEM Forms Remoting. Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

## Impostazioni endpoint remoto {#remoting-endpoint-settings}

**Metodo di autenticazione client Flex:** Determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la sicurezza, l&#39;operazione richiamata non supporta chiamate anonime e il client trasmette credenziali non valide o non valide.
