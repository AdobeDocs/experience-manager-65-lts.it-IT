---
title: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5 LTS SP1
description: Trova informazioni sulla versione, novità, procedure di installazione e un elenco dettagliato delle modifiche per  [!DNL Adobe Experience Manager] 6.5 LTS SP1
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 27ec3c516b0746fd7e0d82f86750fbb4ef410711
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 3%

---


# Note sulla versione di Adobe Experience Manager (AEM) Forms 6.5 LTS SP1 su JEE

## Informazioni sulla versione

| **Prodotto** | Adobe Experience Manager Forms |
| -------------------- | ------------------------------------ |
| **Versione** | 6,5 LTS SP1 |
| **Tipo** | JEE (Long-Term Support Service Pack) |
| **Categoria rilascio** | Versione di aggiornamento |
| **URL di download** | Distribuzione del software |

## Cosa è incluso in [!DNL Experience Manager] 6.5 LTS SP1 {#what-is-included-in-aem-65ltssp1}

Adobe Experience Manager (AEM) Forms **6.5 LTS SP1 su JEE** offre nuove funzionalità, aggiornamenti chiave della piattaforma richiesti dai clienti e correzioni di bug generali, con particolare attenzione alla stabilità del prodotto e al supporto a lungo termine.

## Cosa è incluso in AEM Forms 6.5 LTS SP1

### &#x200B;1. Aggiornamenti del supporto Java

È stato introdotto il supporto per le versioni Java più recenti:

* **Java™ 17**
* **Java™ 21**

### &#x200B;2. Aggiornamenti al supporto di Application Server

#### Supporto per JBoss EAP 8

* È stato aggiunto il supporto per **JBoss EAP 8**.
* Il framework di sicurezza **PicketBox** legacy è stato rimosso.
* **Gli archivi delle credenziali basati su Elytron** sono ora supportati per la gestione sicura delle credenziali.

##### Configurazione: archivio credenziali (basato su Elytron)

AEM Forms su JBoss EAP 8 utilizza Elytron per la gestione delle credenziali sicure. I clienti devono configurare un archivio credenziali basato su Elytron per garantire l&#39;avvio corretto del server e l&#39;autenticazione sicura del database.

Per informazioni dettagliate sulla configurazione, consulta la guida all’installazione e alla configurazione.

### &#x200B;3. Modifiche alla piattaforma e alla compatibilità

#### Supporto delle specifiche dei servlet

* Supporto per **Specifica servlet 5+**
* In base alla conformità di **Jakarta EE 9**

#### Requisito di migrazione dello spazio dei nomi

* Jakarta EE 9 introduce una modifica dello spazio dei nomi da `javax.*` a `jakarta.*`
* Tutti i **DSC personalizzati** devono essere migrati allo spazio dei nomi `jakarta.*`
* AEM Forms 6.5 LTS SP1 supporta **solo i server applicazioni basati su Jakarta EE 9+**

Per ulteriori informazioni, consulta **Migrazione da javax a jakarta Namespace**.

## Aggiornamento

Per istruzioni di aggiornamento dettagliate, consulta la [Guida all&#39;aggiornamento per AEM Forms 6.5 LTS SP1 su JEE](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## Installazione

Per i passaggi e i prerequisiti dell&#39;installazione, fare riferimento alla **Guida all&#39;installazione per AEM Forms 6.5 LTS SP1 (JEE)**.

## Piattaforme supportate

Per un elenco completo delle piattaforme supportate, dei sistemi operativi, dei database e dei server applicazioni, vedere:

**Matrice di piattaforme supportate - AEM Forms 6.5 LTS SP1 (JEE)**

## Funzioni obsolete e rimosse

* Il supporto per **RDBMK** per la persistenza dell&#39;archivio CRX è stato rimosso.
* Per gli ambienti cluster, **solo MongoMK** è supportato per la persistenza dell&#39;archivio.

## Migrazione da javax a jakarta Namespace

### Migrazione da `javax` a `jakarta` spazio dei nomi

A partire da **AEM Forms 6.5 LTS SP1**, sono supportati solo i server applicazioni che implementano **Jakarta Servlet API 5/6**. Con **Jakarta EE 9 e versioni successive**, tutte le API sono passate dallo spazio dei nomi `javax.{}` a `jakarta.`.

Di conseguenza, **tutte le DSC personalizzate devono utilizzare lo spazio dei nomi `jakarta`**. I componenti personalizzati generati con le API `javax.{}` sono **non compatibili** con i server applicazioni supportati.

### Opzioni di migrazione per DSC personalizzate

È possibile eseguire la migrazione di DSC personalizzate esistenti utilizzando uno dei seguenti approcci:

#### Opzione 1: migrazione del codice Source (scelta consigliata)

* Aggiorna tutte le istruzioni di importazione da `javax.{}` a `jakarta.`
* Ricompilare e ricompilare i progetti DSC personalizzati
* Ridistribuisci i componenti aggiornati nel server applicazioni

**Vantaggi:**

* Garantisce la compatibilità a lungo termine con Jakarta EE 9+
* Ideale per progetti con manutenzione attiva

#### Opzione 2: migrazione binaria con il trasformatore Eclipse

* Usa lo strumento **Trasformatore Eclipse** per convertire i file binari compilati (`.jar`, `.war`) da `javax` in `jakarta`
* Non è richiesta alcuna modifica o ricompilazione del codice sorgente
* Ridistribuisci i file binari trasformati nel server applicazioni

>[!NOTE]
>
> La trasformazione binaria viene eseguita al **livello di bytecode**.

Mappature di importazione di esempio

Di seguito sono riportati alcuni esempi comuni di modifiche allo spazio dei nomi necessarie durante la migrazione:

Prima (javax)    Dopo (jakarta)
javax.servlet.*    jakarta.servlet.*
javax.servlet.http.*    jakarta.servlet.http.*

### Mappature di importazione di esempio

La tabella seguente mostra le modifiche comuni allo spazio dei nomi richieste durante la migrazione da `javax` a `jakarta`:

| Prima di (`javax`) | Dopo (`jakarta`) |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

Utilizza queste mappature come riferimento per aggiornare il codice sorgente DSC personalizzato o convalidare i file binari trasformati.

