---
title: Preparazione del contenuto per la traduzione
description: Scopri come preparare i contenuti per la traduzione in Adobe Experience Manager.
contentOwner: Guillaume Carlino
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 3db57dbc-757d-44be-8d32-ea5bc1f02fc8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 42%

---

# Preparazione del contenuto per la traduzione{#preparing-content-for-translation}

I siti web multilingue forniscono generalmente una certa quantità di contenuto in più lingue. Il sito viene creato in una lingua e poi tradotto in altre lingue. In genere, i siti multilingue sono composti da rami di pagine, in cui ogni ramo contiene le pagine del sito in una lingua diversa.

Il sito demo di Geometrixx di esempio include diversi rami di lingua e utilizza la seguente struttura:

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

Ogni ramo linguistico di un sito è denominato copia per lingua. La lingua principale di una copia per lingua, nota come directory principale della lingua, identifica la lingua del contenuto nella copia per lingua. Ad esempio, `/content/geometrixx/fr` è la directory principale della lingua della copia in lingua francese. Le copie per lingua devono utilizzare una [directory principale lingua configurata correttamente](/help/sites-administering/tc-prep.md#creating-a-language-root) in modo che la lingua corretta venga utilizzata quando vengono eseguite le traduzioni di un sito di origine.

La copia per lingua per la quale originariamente si è creato il contenuto del sito è la lingua master. Il lingua master è quella di partenza che viene tradotta in altre lingue.

Utilizza i seguenti passaggi per preparare il sito alla traduzione:

1. Crea la lingua principale della lingua master. Ad esempio, la directory principale della lingua del sito di dimostrazione Geometrixx in inglese è /content/geometrixx/en. Assicurati che la directory principale della lingua sia configurata correttamente in base alle informazioni in [Creazione di una directory principale della lingua](/help/sites-administering/tc-prep.md#creating-a-language-root).
1. Creare il contenuto della lingua master.
1. Crea la directory principale della lingua di ogni copia per la lingua del sito. Ad esempio, la copia in lingua francese del sito di esempio Geometrixx è /content/geometrixx/fr.

Dopo aver preparato il contenuto per la traduzione, puoi creare automaticamente le pagine mancanti nelle copie della lingua e nei relativi progetti di traduzione. (Vedi [Creazione di un progetto di traduzione](/help/sites-administering/tc-manage.md).) Per una panoramica del processo di traduzione dei contenuti in AEM, vedi [Traduzione di contenuti per siti Web multilingue](/help/sites-administering/translation.md).

## Creazione di una directory principale della lingua {#creating-a-language-root}

Crea una directory principale della lingua come pagina principale di una copia per lingua che identifica la lingua del contenuto. Dopo aver creato la directory principale lingua, puoi creare progetti di traduzione che includono la copia per lingua.

Per creare la directory principale della lingua è necessario creare una pagina e utilizzare un codice della lingua ISO come valore per la proprietà Name. Il codice della lingua deve essere in uno dei seguenti formati:

* `<language-code>`Il codice della lingua supportato è un codice a due lettere come definito dallo standard ISO-639-1, ad esempio `en`.

* `<language-code>_<country-code>` o `<language-code>-<country-code>`Il codice paese supportato è un codice a due lettere minuscole o maiuscole come definito dallo standard ISO 3166, ad esempio `en_US`, `en_us`, `en_GB`, `en-gb`.

Puoi utilizzare entrambi i formati, in base alla struttura scelta per il sito globale.  La pagina principale della copia in lingua francese del sito Geometrixx, ad esempio, ha `fr` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della pagina nell’archivio e quindi determina il percorso della pagina. (http://localhost:4502/content/geometrixx/fr.html)

La procedura seguente utilizza l’interfaccia utente ottimizzata per il tocco per creare una copia in lingua di un sito web. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia classica, vedere [Creazione di una directory principale della lingua tramite l&#39;interfaccia classica](/help/sites-administering/tc-lroot-classic.md).

1. Passa a Sites.
1. Fare clic sul sito per il quale si desidera creare una copia per lingua.

   Ad esempio, per creare una copia per lingua del sito Geometrixx Outdoors, fare clic su Sito Geometrixx Outdoors.

1. Fare clic su Crea e quindi su Crea pagina.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Selezionare il modello della pagina e quindi fare clic su Avanti.
1. Nel campo Nome digitare il codice del paese nel formato `<language-code>` o `<language-code>_<country-code>`, ad esempio `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Digita un titolo per la pagina.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Fai clic su Crea. Nella finestra di dialogo di conferma, fai clic su **Fine** per tornare alla console Sites oppure su **Apri** per aprire la copia per lingua.

## Visualizzazione dello stato delle directory principali della lingua {#seeing-the-status-of-language-roots}

L’interfaccia utente ottimizzata per il tocco fornisce un pannello Riferimenti che mostra un elenco di directory principali della lingua create.

![chlimage_1-23](assets/chlimage_1-23a.png)

La procedura seguente utilizza l’interfaccia utente ottimizzata per il tocco per aprire il pannello Riferimenti di una pagina.

1. Nella console Sites, seleziona una pagina del sito e fai clic su **Riferimenti**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. Nel pannello dei riferimenti, fai clic su **Copie per lingua**. Il pannello Copie per lingua mostra le copie per lingua del sito web.
