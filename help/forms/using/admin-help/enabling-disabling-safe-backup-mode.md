---
title: Attivazione e disattivazione della modalità di backup sicuro
description: Nella pagina Impostazioni di backup è possibile utilizzare AEM Forms in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage). Scopri come abilitare e disabilitare la modalità di backup sicuro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 34381caa-154e-479c-b475-7b3549909e9a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Attivazione e disattivazione della modalità di backup sicuro {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Nella pagina Impostazioni di backup è possibile utilizzare AEM Forms in modalità di backup sicura in modo da poter eseguire il backup affidabile del database e della directory GDS (Global Document Storage).

AEM Forms è in modalità di backup sicura ma funziona normalmente, tranne per il fatto che non rimuove attivamente i file dalla directory GDS.

>[!NOTE]
>
>L&#39;impostazione di questa opzione non esegue il backup del sistema, ma prepara il sistema per il backup.

## Abilita modalità di backup sicura {#enable-safe-backup-mode}

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistemi core > Impostazioni di backup.
1. Nella pagina Impostazioni di backup, selezionare Esegui in modalità di backup sicuro e fare clic su OK.

>[!NOTE]
>
>Se il sistema è già in esecuzione in modalità di backup sicuro, non verrà creata una nuova prenotazione quando si fa clic su OK.

## Disattiva modalità di backup sicuro {#disable-safe-backup-mode}

1. Nella console di amministrazione, fai clic su Impostazioni > Impostazioni sistemi core > Impostazioni di backup.
1. Nella pagina Impostazioni di backup deselezionare Esegui in modalità di backup sicuro e fare clic su OK.
