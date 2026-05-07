---
title: Impostare i valori di timeout per l’utilizzo con le estensioni di Acrobat Reader DC
description: Impostare i valori di timeout per l’utilizzo con le estensioni di Acrobat Reader DC
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
exl-id: c2f96686-15e3-4d92-acfe-f971c5849de4
source-git-commit: 26f8a32961cf18c2f1930ab7bc910333b3ccf188
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%

---

# Impostare i valori di timeout per l’utilizzo con le estensioni di Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Quando lavori su molti file PDF nelle Estensioni di Acrobat Reader DC, assicurati che i seguenti valori di timeout siano impostati in modo appropriato per evitare il timeout e l’errore dei processi:

**Timeout eliminazione documento**

Questo valore può essere impostato nella console di amministrazione. Fai clic su Impostazioni > Impostazioni sistema core > Configurazioni e specifica un valore per Timeout eliminazione documento predefinito.

**Timeout AEM Forms della gestione utenti:** questo valore può essere impostato modificando il file config.xml. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione, quindi fai clic su Esporta. Apri il file config.xml esportato e modifica le righe seguenti:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salva e importa nuovamente il file config.xml nella console di amministrazione.

**Timeout sessione server applicazioni:** questo valore può essere impostato sul server applicazioni. Per ulteriori informazioni, consulta la documentazione fornita con il server applicazioni.
