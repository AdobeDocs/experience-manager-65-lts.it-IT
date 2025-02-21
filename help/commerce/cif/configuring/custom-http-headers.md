---
title: Intestazioni HTTP personalizzate
description: Scopri come configurare le intestazioni HTTP personalizzate in Adobe Experience Manager Commerce.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---

# Intestazioni HTTP personalizzate {#custom-http-headers}

## Panoramica {#overview}

Per ottenere un maggiore controllo sul back-end, gli autori possono configurare intestazioni HTTP personalizzate da inviare al motore di e-commerce, insieme a quelle già inviate da CIF. I casi d’uso comuni includono impostazioni multi-store in cui puoi utilizzare le intestazioni HTTP per controllare la risposta del back-end di Commerce.

>[!NOTE]
>
>Gli sviluppatori possono sempre configurare intestazioni HTTP personalizzate utilizzando la configurazione client di GraphQL.
>

## Configurazione {#configuration}

Per configurare le intestazioni HTTP personalizzate, devi prima definirle. Le intestazioni HTTP personalizzate devono prima essere definite aggiungendole alla configurazione del servizio `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` tramite una configurazione OSGi.

Puoi configurare i valori delle intestazioni HTTP nella pagina Configurazione Cloud Service per il progetto:

1. Vai alla pagina di configurazione di Cloud Service in Strumenti > Servizi cloud > Configurazione CIF.
1. Apri una configurazione esistente o creane una.
1. Vai alla scheda &quot;Avanzate&quot; e trova il multicampo &quot;Intestazioni HTTP personalizzate&quot;. Puoi selezionare le intestazioni definite in precedenza e assegnarvi dei valori.

I componenti che utilizzano la configurazione del servizio cloud precedente inviano queste intestazioni HTTP a ogni richiesta di GraphQL.

## Restrizioni {#restrictions}

Anche se il servizio consente di definire qualsiasi nome di intestazione, inclusi quelli standard, non sono disponibili per la configurazione. In altre parole, non puoi sovrascrivere le intestazioni HTTP standard con questa funzione. Un elenco di nomi di intestazione con restrizioni si trova in [documenti Web MDN - intestazioni HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Oltre a queste, ci sono altre due intestazioni che non possono essere utilizzate:

* &quot;Store&quot;: utilizzato da CIF per identificare lo store di Adobe Commerce
* &quot;Preview-Version&quot;: utilizzato da CIF per recuperare i prodotti in staging
