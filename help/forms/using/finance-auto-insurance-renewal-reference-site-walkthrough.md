---
title: Procedura dettagliata sul sito di riferimento per il rinnovo dell'assicurazione automatica We.Finance
description: Scopri il sito di riferimento "We.Finance" per il rinnovo dell’assicurazione automatica seguendo una procedura dettagliata.
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
exl-id: 3f9f1a20-9029-4e30-9c9d-ef452512f7e9
source-git-commit: c0bf6864bb344e582c4f88371c892d401ce2827c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Procedura dettagliata sul sito di riferimento per il rinnovo dell&#39;assicurazione automatica `We.Finance`{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## `We.Finance` scenario del sito di riferimento  {#we-finance-reference-site-scenario}

Il sito Web `We.Finance` è un sito di servizi finanziari progettato per consentire l&#39;apprendimento delle funzionalità di comunicazione interattiva di AEM Forms.

Leggi una procedura dettagliata per un caso di utilizzo di Assicurazione automatica `We.Finance` che illustra come AEM Forms e la sua integrazione con Microsoft® Dynamics consentono di personalizzare l&#39;esperienza del cliente in una società di servizi finanziari. La procedura dettagliata interattiva è progettata per facilitare l’implementazione di transazioni digitali complesse e la comunicazione con i clienti in una società finanziaria.

**Il percorso inizia con il caso d&#39;uso:**

Sarah Rose è un cliente `We.Finance` esistente e ha acquistato una polizza di assicurazione automatica. È quel periodo dell&#39;anno in cui Sarah rinnova la sua polizza assicurativa. Gloria Rios è la sua agente assicurativo. Il sito Web `We.Finance` invia un promemoria a Sarah in merito al rinnovo dei criteri. Sarah segue le istruzioni contenute nell’e-mail e completa correttamente il processo.

## Procedura dettagliata per l&#39;applicazione di assicurazione automatica {#auto-insurance-application-walkthrough}

Lo scenario dell&#39;applicazione di Assicurazione automatica `We.Finance` è una narrazione visiva per l&#39;utente e si basa su due utenti tipo:

* Sarah Rose, cliente di `We.Finance`
* Gloria Rios, agente assicurativo, `We.Finance`

### Gloria invia una comunicazione di rinnovo della polizza assicurativa da `We.Finance` {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria accede all&#39;istanza di AEM, fa clic su **Rinnovo assicurazione automatica,**, quindi fa clic su **Apri interfaccia utente agente**. Il clic precompila il documento di assicurazione con i dettagli della polizza di Sarah Rose. Gloria fa clic su **Invia** e viene visualizzato un messaggio nella schermata &quot;Invio avviato&quot; e quindi tra pochi secondi &quot;Invio completato&quot;.

Sarah riceve un’e-mail con l’oggetto &quot;Rinnovo dell’assicurazione automatica&quot;.

![Interfaccia utente agente](assets/agent_ui_email_new.png)

#### Vedi tu stesso {#see-it-yourself}

Vai a **Adobe Experience Manager** > **Forms** > **Forms e documenti** > **`We.Finance`** > **Assicurazione automatica**. Seleziona Rinnovo assicurazione automatica **comunicazione interattiva** e fai clic su **Apri interfaccia utente agente**. La comunicazione interattiva si apre nell’interfaccia utente dell’agente. Inserisci un indirizzo e-mail valido in modo che possano ricevere l’e-mail con il documento della policy allegato e fai clic su Invia.

Puoi accedere alla comunicazione interattiva Rinnovo assicurazione automatica e rivederla direttamente da `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah riceve una comunicazione di rinnovo della polizza assicurativa da `We.Finance` e decide di rinnovare {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah riceve un&#39;e-mail con un allegato da `We.Finance`, che ricorda a Sarah che la sua polizza di assicurazione automatica sta per scadere. L&#39;allegato è la versione stampata della lettera di Assicurazione automatica di Sarah.

Sarah fa clic sull&#39;opzione **Rinnova ora** e viene indirizzata alla versione Web della lettera di assicurazione automatica. In cima a questa lettera, Sarah trova il tempo rimanente nella polizza prima della scadenza. La pagina fornisce una panoramica della polizza assicurativa. Descrive il numero della polizza, l’importo dovuto, le offerte di sconto e i premi fedeltà. **Rinnova ora** è stato selezionato in fondo al criterio.

![rif1](assets/ref1.png)

#### Come funziona {#how-it-works}

L’output web e cartaceo della lettera di Assicurazione automatica viene creato utilizzando le funzionalità multicanale delle comunicazioni interattive.

Il pulsante Rinnova ora nell’e-mail è collegato all’applicazione Rinnova assicurazione automatica, che è una comunicazione interattiva su un’istanza pubblicata.

#### Vedi tu stesso {#see-it-yourself-1}

È necessario aver ricevuto un&#39;e-mail con un PDF allegato. Il PDF è una versione stampata della lettera di assicurazione automatica. Fare clic su **Rinnova ora** per accedere alla versione Web del criterio. Controlla le tue informazioni personali e i dettagli dei criteri e fai clic su **Rinnova ora** per passare a un&#39;altra comunicazione interattiva.

Il pulsante **Rinnova ora** nell&#39;e-mail indirizza Sarah al criterio sul Web. Puoi visitare il seguente URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Controlla il riepilogo dettagliato del rinnovo dell&#39;assicurazione automatica e fai clic su **Rinnova ora** nella parte inferiore della pagina.

### Sarah raggiunge la pagina dei pagamenti {#sarah-reaches-the-payment-page}

Il sito Web `We.Finance` porta Sarah alla pagina Pagamento. Sarah controlla nuovamente i suoi documenti dal numero della polizza e dalla data di scadenza. Sul lato destro della pagina, Sarah controlla il Riepilogo pagamenti del rinnovo con uno sconto del 10% sull’importo totale.

#### Come funziona {#how-it-works-1}

Il pulsante Rinnova ora indirizza Sarah alla pagina di pagamento. La pagina di pagamento è un modulo adattivo.

#### Vedi tu stesso {#see-it-yourself-2}

Fai clic su **Rinnova ora** per accedere alla pagina Pagamento. Inserisci le informazioni sulla tua carta di credito e fai clic su **Paga**.

Puoi accedere alla pagina dei pagamenti nell’istanza di authoring all’indirizzo

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah effettua il pagamento e completa la procedura {#sarah-makes-the-payment-and-completes-the-process}

Sarah compila i dettagli della sua carta di credito e fa clic su **Effettua pagamento**.

#### Come funziona {#how-it-works-2}

Quando Sarah compila i dettagli della carta di credito e fa clic su Invia, il pagamento con la carta di credito viene elaborato e sullo schermo viene visualizzato un messaggio di ringraziamento configurato nel modulo adattivo.

#### Vedi tu stesso {#see-it-yourself-3}

Puoi visualizzare il messaggio di conferma dopo aver fatto clic su Effettua pagamento all’indirizzo

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
