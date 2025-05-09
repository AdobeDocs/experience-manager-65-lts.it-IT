---
title: Consegna sicura delle informazioni a volumi elevati
description: Document Security supporta l’associazione delle licenze agli utenti, anziché ai documenti negli ambienti di produzione di massa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5df8c609-8007-4422-9bf8-5bae6d53b9b7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Consegna sicura delle informazioni a volumi elevati {#high-volume-secure-information-delivery}

In un ambiente di produzione di massa, ad esempio quello che genera fatture mensili protette per una società di telecomunicazioni, la creazione di licenze specifiche per ciascun documento può diventare un processo che richiede molte risorse. In questi casi, la protezione dei documenti supporta l&#39;associazione delle licenze agli utenti anziché ai documenti. La licenza generata per un utente viene utilizzata per tutti i documenti protetti per tale utente.

Un vantaggio di questo approccio è che le dimensioni del database di protezione dei documenti non crescono in modo lineare con i documenti, ma con il numero di utenti. Inoltre, poiché è necessario creare la licenza una sola volta per un utente, la successiva protezione dei documenti tramite queste policy diventa più veloce. Funzionalità quali l&#39;accesso offline, la scadenza e la revoca dei documenti sono supportate per tutti questi documenti.

La protezione dei documenti supporta anche Criteri astratti. I criteri astratti sono modelli di criteri che contengono tutti gli attributi dei criteri, ad esempio le impostazioni di protezione dei documenti e i diritti di utilizzo, ma non contengono un elenco di entità principali. Gli amministratori possono creare un numero qualsiasi di criteri dalla policy astratta con entità diverse che devono avere accesso ai documenti. Le modifiche apportate al criterio astratto non influiscono sui criteri effettivi generati dai criteri astratti.

Se viene generata una fattura mensile per una società di telecomunicazioni, è possibile creare una policy astratta, creare utenti e quindi generare licenze univoche per ogni utente. Le licenze vengono successivamente applicate ai documenti per ogni utente.

La creazione di un criterio astratto è supportata solo tramite Document Security Java SDK. È tuttavia possibile amministrare i criteri creati dai criteri astratti dalle pagine Web di Document Security. I criteri creati con questo metodo hanno lo stesso comportamento di quelli creati dalle pagine Web di Document Security.

Per ulteriori informazioni, vedere [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).
