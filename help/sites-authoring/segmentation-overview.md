---
title: Segmentazione durante la creazione di una campagna
description: La segmentazione è un fattore chiave per la creazione di una campagna.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: 7167c672-8d24-4493-aff6-b5b453074bff
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 46%

---

# Segmentazione{#understanding-segmentation}

La segmentazione è un concetto chiave per la creazione di una campagna. Di solito, prima di avviare la campagna devi avere già definito dei segmenti.

I visitatori del sito hanno interessi e obiettivi diversi quando arrivano su un sito. Comprendere questi obiettivi e soddisfare le aspettative è un importante fattore di successo per il marketing online.

La segmentazione consente di ottenere questo risultato analizzando e caratterizzando i:

* attività sul sito web
* profilo
* attività su altri siti web

Il contenuto può quindi essere adattato alle esigenze e agli interessi del visitatore, a seconda dei segmenti di corrispondenza.

## Utilizzo della segmentazione {#using-segmentation}

I segmenti sono definiti in [Configurazione della segmentazione](/help/sites-administering/campaign-segmentation.md). Vengono utilizzati per gestire il contenuto effettivo visualizzato da un pubblico specifico.

## Terminologia di segmentazione {#segmentation-terminology}

Quando si parla di segmentazione, viene spesso utilizzata la seguente terminologia:

**Visitatore**: un visitatore è una persona che visita un sito web. La visita di quella persona in genere inizia da una pagina di riferimento, quindi passa a una o più visualizzazioni di pagina sul tuo sito web. Puoi creare un profilo comportamentale dai dettagli della visita di quella persona.

**Utente**: l’utente è un visitatore che si è registrato sul sito web e a cui è associato un profilo di account. Per generare il loro profilo, forniscono un’identificazione aggiuntiva, tra cui un indirizzo e-mail e il genere. È inoltre possibile raccogliere informazioni aggiuntive, tra cui le attività della community e i modelli di acquisto. In base alle informazioni fornite nel profilo, è possibile creare un profilo demografico.

**Caratteristica**: per caratteristica si intende una proprietà del visitatore che può essere usata per determinarne l’appartenenza a uno specifico segmento.

**Segmento**: un segmento è una raccolta di visitatori che condividono alcune caratteristiche. I segmenti devono essere distinti, con solo un minimo di sovrapposizione con altri segmenti.

**Caratteristiche comportamentali**: le caratteristiche comportamentali fanno riferimento al comportamento di un visitatore sul sito web. Comprendono:

* Interesse nel tuo sito web, incluse le pagine visitate e i prodotti acquistati.
* Interesse nel sito web di provenienza, inclusi termini di ricerca utilizzati o annunci pubblicitari su cui è stato fatto clic.
* Interesse su altri siti; determinato utilizzando strumenti come Spyjax.
* Fedeltà del visitatore; durata della visita, frequenza delle visite.

**Caratteristiche demografiche**: caratteristiche specifiche della popolazione selezionata, tra cui:

* Età
* Reddito
* Dimensioni della famiglia
* Stato civile
* Genere
* Dove si trova

**Caratteristiche derivate**: alcune caratteristiche demografiche sono difficili da determinare senza la registrazione, ma possono essere derivate dalla combinazione di caratteristiche comportamentali e demografiche.

Ad esempio, la combinazione dell&#39;URL di riferimento (come tratto comportamentale) con i dati demografici (acquisiti da strumenti come [Google Ad Planner](https://www.google.com/adplanner/)) consente ai proprietari dei siti di derivare i tratti demografici dei loro visitatori.

**Sottosegmento**: un segmento può essere diviso in diversi sottosegmenti. Questo viene effettuato mediante la definizione di caratteristiche aggiuntive.

**Pagina teaser**: una pagina teaser si rivolge a un particolare pubblico. Contiene contenuto riutilizzabile che può essere utilizzato nel paragrafo del teaser.

**Campagna**: per campagna si intende una raccolta di pagine teaser e pagine di marketing e-mail, quali newsletter o inviti. In genere una campagna ha una durata limitata e alla sua scadenza viene sostituita da un’altra campagna.

**Paragrafo teaser**: si tratta di un paragrafo che utilizza contenuto da un’altra pagina a seconda di una strategia di selezione. Tale strategia di selezione può basarsi su segmenti e campagne.

**Elenco**: un elenco viene estratto da un segmento di utenti registrati. Ad esempio, la località da cui dipende il contenuto del paragrafo teaser.

>[!NOTE]
>
>Per ulteriori informazioni sui segmenti in Adobe Experience Manager, vedi [Segmentazione](/help/sites-administering/campaign-segmentation.md).
