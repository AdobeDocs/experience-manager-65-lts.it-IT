---
title: Creare nuove cartelle per categorizzare i moduli
description: Utilizza le cartelle per organizzare modelli di modulo, PDF, risorse e moduli adattivi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: cc84c92b-d1a3-4314-a079-7dcbf013712a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Creare nuove cartelle per categorizzare i moduli {#create-new-folders-to-categorize-forms}

Puoi organizzare meglio le risorse utilizzando le cartelle. Poiché AEM Forms supporta diversi tipi di risorse (modelli di modulo, PDF, documenti, risorse e moduli adattivi con vari metadati), è possibile utilizzare le cartelle per categorizzare i moduli in base ai criteri desiderati.

AEM Forms consente di modificare il titolo di una cartella. Il titolo non corrisponde al nome del nodo in cui è memorizzata la cartella nell&#39;archivio. Il titolo viene invece mantenuto come metadati per la cartella. Se modifichi il titolo di una cartella, il percorso di qualsiasi risorsa presente all’interno della cartella non viene modificato.

## Crea una cartella {#create-a-folder}

Puoi creare una cartella in AEM Forms in uno dei seguenti modi:

* Caricare un file ZIP contenente risorse nella struttura di cartelle desiderata (vedere [Recupero di documenti XDP e PDF in AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Crea una cartella vuota

1. Accedere all&#39;interfaccia utente di AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.
1. Passare alla posizione in cui si desidera creare una cartella.
1. Fai clic sull&#39;icona ![aem6forms_add](assets/aem6forms_add.png) nella barra degli strumenti, quindi seleziona **[!UICONTROL Crea cartella]**.

1. Immetti i seguenti dettagli:

   * **Titolo:** Nome visualizzato per la cartella
   * **Nome:** *(obbligatorio)* Nome del nodo in cui si desidera archiviare la cartella nel repository

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici o trattini (-) e trattini bassi (_) caratteri speciali. Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti da un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

1. Fai clic su **[!UICONTROL Invia].**

   Nell’elenco delle risorse, nella posizione corrente viene visualizzata una nuova cartella con il titolo definito.

   Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Puoi visualizzare il messaggio di errore passando il cursore sull&#39;icona di errore ![aem6forms_error_alert](assets/aem6forms_error_alert.png) visualizzata accanto al campo del nome.

### Modifica il titolo della cartella {#edit-the-folder-title-br}

1. Seleziona la cartella di cui desideri modificare il titolo.
1. Fai clic sull&#39;icona Modifica ![aem6forms_edit](assets/aem6forms_edit.png) nella barra degli strumenti.
1. Inserisci il nuovo titolo. Nel campo di testo viene inserito automaticamente il valore corrente del titolo della cartella. È possibile modificarlo in un nuovo valore.
1. Fai clic su **[!UICONTROL Invia].**
