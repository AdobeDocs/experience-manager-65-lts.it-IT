---
title: Procedura dettagliata sul sito di riferimento We.Gov FOIA
description: Consulta la procedura dettagliata sul sito di riferimento We.Gov per capire in che modo AEM Forms aiuta i governi a ricevere e comunicare le informazioni richieste da singoli individui in base al Freedom of Information Act.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
exl-id: a2f79634-6eca-479a-89d7-e1ef2e4a6e6d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# Procedura dettagliata sul sito di riferimento We.Gov FOIA {#we-gov-reference-site-foia-walkthrough}

## Scenario del Freedom of Information Act per il sito di riferimento {#reference-site-freedom-of-information-act-scenario}

We.Gov è un&#39;organizzazione gestita dallo stato che consente ai genitori adottivi di iscriversi per il sostegno al bambino se hanno adottato un bambino. We.Gov consente inoltre ai genitori di richiedere informazioni ai seguenti dipartimenti governativi in base al Freedom of Information Act:

* Agenzia logistica della difesa
* Dipartimento della Difesa Ufficio dell&#39;Ispettore Generale
* Dipartimento della Giustizia - Ufficio delle politiche dell&#39;informazione
* Dipartimento della Marina
* Agenzia per la protezione dell&#39;ambiente

Per ulteriori informazioni sul Freedom Of Information Act, vedere [https://www.foia.gov/](https://www.foia.gov).

Lo scenario coinvolge i seguenti utenti tipo:

* Sarah Rose, la persona che ha richiesto le informazioni
* John Jacobs, la persona che gestisce la richiesta la inoltra al reparto appropriato
* Gloria Rios, l&#39;impiegato governativo che fornisce le informazioni come da richiesta

## Sarah avvia una richiesta di informazioni in base alla FOIA {#sarah-initiates-request-for-information-under-foia}

Ai sensi del Freedom of Information Act, Sarah richiede una copia dei registri dell&#39;Administration for Children and Families dal 2013 al 2016. Sarah presenta tale richiesta al Dipartimento di giustizia - Ufficio delle politiche dell&#39;informazione e si dichiara altresì disposta a pagare fino a 100 USD per le spese di stampa e di spedizione.

### Come funziona {#how-it-works}

### Vedi tu stesso {#see-it-yourself}

Nel browser aprire `https://<hostname>:<PublishPort>/wegov`. Nel sito We.Gov, selezionare Applicazioni > Tutte le applicazioni. Nella pagina Tutte le applicazioni, selezionare Applica in Applicazione per richiesta FOIA.

## Sarah inizia la sua richiesta di informazioni sotto FOIA {#sarah-starts-her-application-for-information-under-foia}

Sarah fa clic su **Applica** e nella pagina del modulo di richiesta Freedom of Information Act immette le seguenti informazioni:

* **Agenzia:** Sarah specifica l&#39;agenzia a cui è stata indirizzata la richiesta come Department of Justice - Office of Information Policy.

* **Pagherà fino a**: Sarah specifica di essere disposta a pagare fino a 100 USD per le spese di stampa e di spedizione.
* **Descrivere la richiesta in dettaglio**: Sarah specifica &quot;Richiesta di copia dei registri dei casi relativi all&#39;amministrazione per figli e famiglie per gli anni fiscali dal 2013 al 2016&quot;.

![Richiesta della copia dei registri dei casi relativi all&#39;amministrazione per figli e famiglie per gli anni fiscali dal 2013 al 2016](assets/sarahfiosform.png)

Richiesta di copia dei registri dei casi relativi all’amministrazione per bambini e famiglie per gli anni fiscali dal 2013 al 2016

In qualsiasi momento, Sarah può selezionare **Salva** per salvare una bozza del modulo e tornare in seguito per compilare il modulo e inviarlo. Sarah invia il modulo.

>[!NOTE]
>
>Il flusso di lavoro Riprendi da e-mail funziona solo con gli utenti connessi. Nello scenario del sito di riferimento, accertati che sia aggiunto l’utente Sarah Rose. Le credenziali di accesso di Sarah sono `srose/password`.

## John Jacobs riceve e approva la richiesta {#john-jacobs-receives-and-approves-the-application}

John Jacobs riceve la richiesta e la indirizza alla persona giusta. Casella in entrata AEM consente a John di visualizzare tutte le applicazioni inviate in un’unica posizione.

### Come funziona {#how-it-works-1}

Quando Sarah compila e invia l&#39;applicazione FOIA, un record dell&#39;applicazione viene inviato alla casella in entrata di John Jacobs. John Jacobs può visualizzare la domanda presentata e accettarla o rifiutarla.

### Vedi tu stesso {#see-it-yourself-1}

Puoi accedere alla casella in entrata di AEM all&#39;indirizzo https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Accedi alla casella in entrata di AEM utilizzando jjacobs/password come nome utente/password per John Jacobs e controlla l’applicazione FOIA. Per informazioni sull&#39;utilizzo della Posta in arrivo di AEM per le attività del flusso di lavoro incentrate sui moduli, vedere [Gestione delle applicazioni e delle attività di Forms nella Posta in arrivo di AEM](/help/forms/using/manage-applications-inbox.md).

![johnjacobs](assets/johnjacobs.png)

John Jacobs può visualizzare, approvare o rifiutare l’applicazione dal dashboard dell’applicazione. John Jacobs seleziona e apre i dettagli della richiesta e, dopo aver esaminato la richiesta, la approva.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah riceve un&#39;e-mail di conferma</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

Dopo che John Jacobs ha approvato l&#39;applicazione, Sarah riceve un&#39;e-mail di conferma dal sito We.Gov. Sarah viene informata delle tariffe e del tempo necessario per elaborare la sua domanda. L’e-mail include anche i dettagli dell’e-mail e del telefono che Sarah può contattare per ottenere aggiornamenti sulla sua applicazione.

![sarahroseemail](assets/sarahroseemail.png)

## Gloria riceve la richiesta FOIA per l&#39;approvazione di secondo livello {#gloria-receives-the-foia-request-for-second-level-approval}

Dopo che John Jacobs compila le informazioni richieste e approva la richiesta di Sarah, passa a Gloria Rios per l&#39;approvazione finale. Gloria esamina il documento di record allegato e approva la richiesta.

![gloriariosinbox](assets/gloriariosinbox.png)

### Come funziona {#how-it-works-2}

Quando John Jacobs approva la richiesta FOIA, viene creato un PDF o un documento di record dell’applicazione e inviato alla casella in entrata di Gloria Rios. Gloria può visualizzare la richiesta inviata e approvarla o rifiutarla.

### Vedi tu stesso {#see-for-yourself}

Puoi accedere alla casella in entrata di AEM all&#39;indirizzo https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html. Accedi alla casella in entrata di AEM utilizzando grios/password come nome utente/password per Gloria Rios e controlla la richiesta FOIS.

Gloria apre la richiesta ed esamina i dettagli della richiesta FOIA. Dopo aver esaminato i dettagli della richiesta e verificato la fattibilità di fornire i documenti richiesti, Gloria approva la richiesta.

![gloriariosapproves](assets/gloriariosapproves.png)

## Sarah riceve una notifica di approvazione della sua richiesta {#sarah-receives-notification-that-her-request-is-approved}

Dopo che Gloria approva la richiesta FOIA, Sarah riceve un&#39;e-mail che le notifica che la sua richiesta è approvata. L’e-mail include anche le informazioni sulla tempistica provvisoria per la presentazione del documento e i recapiti per il follow-up della richiesta.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
