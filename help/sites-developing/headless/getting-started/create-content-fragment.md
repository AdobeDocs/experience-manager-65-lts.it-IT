---
title: Guida rapida alla creazione di frammenti di contenuto headless
description: Scopri come utilizzare i Frammenti di contenuto AEM per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la consegna headless.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: 7b26e5cb-3aab-4f69-a0f1-42268c39bba8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 73%

---

# Guida rapida alla creazione di frammenti di contenuto headless {#creating-content-fragments}

Scopri come utilizzare i Frammenti di contenuto AEM per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la consegna headless.

## Cosa sono i Frammenti di contenuto? {#what-are-content-fragments}

[Ora che hai creato una cartella risorse](create-assets-folder.md) nella quale puoi archiviare i Frammenti di contenuto, puoi cominciare a crearli.

I frammenti di contenuto ti consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalle pagine. Consentono di preparare contenuti pronti per l&#39;uso in più posizioni e su più canali.

I Frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

## Come creare un Frammento di contenuto {#how-to-create-a-content-fragment}

Gli autori dei contenuti creano un certo numero di Frammenti di contenuto per rappresentare il contenuto creato. Questa sarà l’attività principale dei Frammenti di contenuto in AEM. Ai fini di questa guida introduttiva, ne creeremo uno.

1. Accedi ad AEM e dal menu principale seleziona **Navigazione > Assets**.
1. Passa alla cartella [ creata in precedenza.](create-assets-folder.md)
1. Fare clic su **Crea > Frammento di contenuto**.
1. La creazione di un Frammento di contenuto viene presentata come una procedura guidata in due passaggi. Seleziona innanzitutto il modello da utilizzare per creare il frammento di contenuto e fai clic su **Avanti**.
   * I modelli disponibili dipendono dalla [**configurazione cloud** definita per la cartella risorse](create-assets-folder.md) in cui stai creando il frammento di contenuto.
   * Se ricevi il messaggio `We could not find any models`, controlla la configurazione della cartella delle risorse.

   ![Seleziona modello di Frammento di contenuto](assets/content-fragment-model-select.png)
1. Fornisci **Titolo**, **Descrizione** e **Tag** secondo necessità e fai clic su **Crea**.

   ![Creare Frammento di contenuto](assets/content-fragment-create.png)
1. Fai clic su **Apri** nella finestra di conferma.

   ![Conferma di creazione del Frammento di contenuto](assets/content-fragment-confirmation.png)
1. Fornisci i dettagli del Frammento di contenuto nell’Editor frammento di contenuto.

   ![Editor frammento di contenuto](assets/content-fragment-edit.png)
1. Fai clic su **Salva** o **Salva e chiudi**.

I Frammenti di contenuto possono fare riferimento ad altri Frammenti di contenuto, consentendo se necessario una struttura di contenuto nidificata.

I Frammenti di contenuto possono fare riferimento ad altre risorse in AEM. [Queste risorse devono essere memorizzate in AEM](/help/assets/manage-assets.md) prima di creare un riferimento in un Frammento di contenuto.

## Passaggi successivi {#next-steps}

Dopo aver creato un Frammento di contenuto, puoi passare alla parte finale della guida introduttiva e [creare richieste API per accedere e distribuire frammenti di contenuto.](create-api-request.md)

>[!TIP]
>
>Per informazioni complete sulla gestione dei Frammenti di contenuto, consulta la sezione [Documentazione sui Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).
