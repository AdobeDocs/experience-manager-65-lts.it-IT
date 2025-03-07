---
title: Configurazione delle estensioni del controller di dominio Acrobat Reader per l'acquisizione dei dati
description: Scopri come configurare le estensioni DC di Acrobat Reader per l’acquisizione dei dati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
hide: true
hidefromtoc: true
exl-id: f9b01de7-1de5-43aa-bcc3-b15719bfa5c0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Configurazione delle estensioni del controller di dominio Acrobat Reader per l&#39;acquisizione dei dati {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Se gli utenti dell&#39;installazione di AEM Forms utilizzano la funzionalità di acquisizione dati di Content Services (obsoleto), è consigliabile creare un ruolo con accesso in sola lettura per tali utenti.

***Nota **: Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 12/31/2014. Consulta il documento sul ciclo di vita del prodotto [Adobe](https://helpx.adobe.com/it/support/programs/eol-matrix.html).*

Per l&#39;acquisizione dei dati è necessario assegnare un ruolo utente per accedere a SampleReaderExtensionsCredential. È possibile assegnare il ruolo standard Amministratore trust. Tuttavia, si consideri che questo ruolo conferisce agli utenti generali e non amministratori privilegi di amministratore che controllano le impostazioni di attendibilità PKI e gestiscono le credenziali PKI, il che potrebbe compromettere la sicurezza dell&#39;installazione di AEM Forms in un ambiente di produzione. È consigliabile che l&#39;amministratore di sistema di AEM Forms crei un ruolo che consenta solo l&#39;accesso in sola lettura all&#39;archivio fonti attendibili e assegni questo nuovo ruolo agli utenti non amministratori che utilizzano l&#39;acquisizione dei dati.

## Creare un ruolo per gli utenti di acquisizione dati {#create-a-role-for-data-capture-users}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Nuovo ruolo.
1. Immettere il nome del ruolo (ad esempio, Utente di acquisizione dati) e la descrizione nei campi appropriati, quindi fare clic su Avanti.
1. Nella schermata Autorizzazioni ruolo, fai clic su Trova autorizzazioni, quindi seleziona Lettura credenziali dall’elenco delle autorizzazioni disponibili.
1. Fare clic su OK, quindi su Fine.

## Assegnare il ruolo di acquisizione dati {#assign-the-data-capture-role}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione ruolo, quindi fai clic su Trova.
1. Fai clic sul ruolo utente di acquisizione dati creato.
1. Nella scheda Utenti/gruppi ruolo fare clic su Trova utenti/gruppi.
1. Nella schermata Trova utenti e gruppi fare clic su Trova, selezionare gli utenti che richiedono il ruolo utente di acquisizione dati, quindi fare clic su OK.
1. Nella schermata Modifica ruolo, fai clic su Salva.
