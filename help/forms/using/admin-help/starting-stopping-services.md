---
title: Avvio e arresto dei servizi
description: Scopri come avviare e arrestare i servizi associati ai moduli AEM Forms, al server applicazioni e al database.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a4ff69d2-a429-49b9-ba48-9dd56ccdf23e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Avvio e arresto dei servizi {#starting-and-stopping-services}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Esistono due tipi di servizi che fanno parte di AEM Forms:

* Servizi che controllano il server applicazioni e il database di AEM Form.
* Servizi che controllano i moduli di AEM Forms

## Avviare o arrestare i servizi associati ai moduli di AEM Forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

I moduli di AEM Forms (ad esempio, Forms, Rights Management, Output) funzionano come servizi. A volte può essere necessario arrestare o avviare i servizi per questi moduli di AEM Forms. È ad esempio necessario arrestare e riavviare un servizio AEM Forms dopo aver modificato un&#39;impostazione per il servizio.

>[!NOTE]
>
> Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Nella console di amministrazione, fare clic su **Servizi** > **Applicazioni e servizi** > **Gestione servizi**.
1. Nella pagina Gestione servizio selezionare la casella di controllo accanto al servizio da arrestare o avviare e fare clic su Arresta o Avvia.

## Avviare o arrestare i servizi per il server applicazioni e il database {#start-or-stop-services-for-the-application-server-and-database}

Un&#39;implementazione completa di AEM Forms include un server applicazioni e servizi di database:

* *`[application server]`* per AEM Forms
* *`[database]`* per AEM Forms

In Windows, questi servizi sono accessibili tramite **Strumenti di amministrazione** > **Pannello servizi**. Ad esempio, se AEM Forms è stato installato su JBoss utilizzando il metodo chiavi in mano, nel sistema sono disponibili i seguenti servizi:

* JBoss per Adobe Experience Manager forms
* MySQL per Adobe Experience Manager forms

Avviare o arrestare questi servizi selezionandoli dall&#39;elenco nel pannello Servizi e quindi facendo clic sul pulsante di azione appropriato nel pannello.

In UNIX® o Linux, immettere il testo seguente da una riga di comando, dove *`[service name]`* è il nome del servizio che si sta verificando:

```java
     ps -A | grep [service name]
```
