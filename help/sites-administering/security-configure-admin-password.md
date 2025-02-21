---
title: Configurare la password amministratore durante l’installazione
description: Scopri come modificare la password amministratore nell’installazione di Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Configurare la password amministratore durante l’installazione{#configure-the-admin-password-on-installation}

## Panoramica {#overview}

A partire dalla versione 6.3, Adobe Experience Manager (AEM) consente di impostare la password amministratore tramite la riga di comando durante l’installazione di una nuova istanza.

Con le versioni precedenti di AEM, la password dell’account amministratore, insieme alla password per varie altre console, doveva essere modificata dopo l’installazione.

Questa funzione consente inoltre di impostare una nuova password amministratore per l’archivio e il Servlet Engine durante l’installazione di un’istanza di AEM, eliminando in tal modo la necessità di eseguire manualmente l’operazione successivamente.

>[!CAUTION]
>
>La funzione non copre la console Felix, per la quale la password deve essere modificata manualmente. Per ulteriori informazioni, vedere la [sezione Elenco di controllo protezione](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts) pertinente.

## Come Si Utilizza? {#how-do-i-use-it}

Questa funzione si attiva automaticamente se si sceglie di installare AEM tramite la riga di comando, anziché fare doppio clic sul file JAR da una finestra di esplorazione del file system.

La sintassi generale per l’esecuzione di un’istanza AEM dalla riga di comando è:

```shell
java -jar aem6.3.jar
```

Dopo aver eseguito l’istanza dalla riga di comando, viene visualizzata l’opzione per modificare la password amministratore durante il processo di installazione:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>La richiesta di modifica della password amministratore viene visualizzata solo durante l’installazione di una nuova istanza di AEM.

## Utilizzo del flag -nointeractive {#using-the-nointeractive-flag}

Puoi anche scegliere di specificare la password da un file di proprietà. Questa operazione viene eseguita utilizzando il flag `-nointeractive` combinato con la proprietà di sistema `-Dadmin.password.file`.

Di seguito è riportato un esempio:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

La password all&#39;interno del file `passwordfile.properties` deve avere il seguente formato:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Se si utilizza semplicemente il parametro `-nointeractive` senza la proprietà di sistema `-Dadmin.password.file`, AEM utilizza la password amministratore predefinita senza chiedere di modificarla, essenzialmente replicando il comportamento delle versioni precedenti. Questa modalità non interattiva può essere utilizzata per le installazioni automatizzate tramite la riga di comando in uno script di installazione.
