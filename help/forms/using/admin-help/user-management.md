---
title: User Management
description: Gestione utenti consente di abilitare l'SSO tra i moduli di AEM Forms e le applicazioni protette da Netegrity SiteMinder utilizzando SAML. Questo documento fornisce ulteriori informazioni sulla gestione degli utenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5a87e340-053b-4b72-99a0-df14d7bf304c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# User Management {#user-management}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Gestione utenti consente di abilitare il Single Sign-On (SSO) tra i moduli di AEM Forms e le applicazioni protette da Netegrity SiteMinder utilizzando il linguaggio SAML (Security Assertion Markup Language). Quando si implementa l’SSO, le pagine di accesso dell’utente di AEM Forms non sono obbligatorie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

Per informazioni sul miglioramento delle prestazioni di sincronizzazione di database e directory per DB2, vedere [Database IBM DB2: esecuzione di comandi per la manutenzione regolare](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configurazione della gestione degli utenti per un server LDAP abilitato per SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se si dispone di un server LDAP abilitato per SSL, configurare User Management per utilizzarlo. (Vedere [Configurare la gestione degli utenti per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Impostazione dei privilegi utente per l’utilizzo con Document Security {#setting-user-privileges-for-use-with-document-security}

Creare un utente amministratore con i privilegi appropriati per la creazione di utenti e gruppi. Se l’ambiente AEM Forms include Document Security, concedi il privilegio di gestire gli utenti invitati e locali a un utente che fungerà da amministratore per questi utenti. Assegna inoltre il ruolo Utente alla console di amministrazione per fornire all’utente l’accesso alla console di amministrazione. (Vedi [Creazione e configurazione dei ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti dei criteri, un amministratore privilegiato o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all&#39;elenco visibile di utenti e gruppi per ogni set di criteri creato.

L’elenco visibile di utenti e gruppi è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l’utente finale può sfogliare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà alcun utente o gruppo da aggiungere al criterio. Per ogni set di criteri può essere presente più di un coordinatore.

>[!NOTE]
>
>La creazione di domini deve essere eseguita prima di poter creare qualsiasi criterio.

### Impostare utenti e gruppi visibili {#set-visible-users-and-groups}

Dopo aver installato e configurato l’ambiente AEM Forms con Document Security, imposta tutti i domini appropriati in Gestione utente.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Criteri, quindi fai clic sulla scheda Set di criteri.
1. Selezionare Set di criteri globale, quindi fare clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.
1. Passa a Servizi > Document Security > Configurazione > I miei criteri e fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.

## Limitazioni per gli utenti amministratori {#administrator-user-restrictions}

Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine Web degli utenti finali di Workspace per motivi di sicurezza. Poiché queste pagine Web possono esistere all&#39;esterno di un firewall, consentire attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore di Workspace o di utente di Workspace possono accedere alle pagine Web degli utenti finali.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.
