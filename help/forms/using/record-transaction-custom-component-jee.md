---
title: Registra una transazione per l’API del componente personalizzato per AEM Forms su JEE.
description: Scopri come utilizzare l’API TransactionRecorder per registrare le transazioni per il componente personalizzato.
feature: Transaction Reports
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: e2d1b548-ce30-471b-b01c-ce37b737aeb5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Registrare una transazione per le API dei componenti personalizzati per AEM Forms su JEE {#record-a-transaction-for-custom-components}

Quando utilizzi le API fatturabili nel componente personalizzato, puoi abilitare la generazione rapporti sulle transazioni per il componente. Per abilitare il reporting delle transazioni, modificare il file `component.xml` del componente e aggiungere il tag specificato di seguito nell&#39;operazione per la quale deve essere abilitato il reporting delle transazioni.

**Tag**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Tag precedente dell’operazione | Nuovo tag operazione |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Se devi acquisire più di una transazione per un’API, ad esempio un’API batch in cui il conteggio delle transazioni varia in base al numero di conteggi di input, gestisci il conteggio delle transazioni a livello di API.

**Per registrare il conteggio delle transazioni variabili:**

1. Importa la classe `"com.adobe.idp.dsc.InvocationContextStack"` nel codice. La classe fa parte del file sdk `adobe-livecycle-client.jar`. Il file sdk è disponibile in `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Aggiorna il file client condiviso in precedenza nel progetto client con il nuovo file, nel caso in cui sia già incluso nel bundle.

1. Nell’API per la quale devono essere registrate le transazioni varie:
   1. Aggiungere la logica per memorizzare il conteggio delle transazioni in alcune variabili intere, ad esempio `transaction_count`.
   1. Al termine dell&#39;operazione, aggiungere `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Articoli correlati

* [Abilitazione e visualizzazione dei rapporti sulle transazioni per AEM Forms su JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Elenco delle API fatturabili per AEM Forms su JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)
