---
title: Impostazione dei valori di timeout per l'utilizzo con le estensioni di Acrobat Reader DC
description: Scopri come impostare i valori di timeout per l’utilizzo con le estensioni Acrobat Reader DC.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c2f96686-15e3-4d92-acfe-f971c5849de4
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Impostazione dei valori di timeout per l&#39;utilizzo con le estensioni di Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Quando si lavora su molti file PDF nelle estensioni Acrobat Reader DC, assicurarsi che i seguenti valori di timeout siano impostati in modo appropriato per evitare il timeout e l&#39;errore dei processi:

**Timeout eliminazione documento**

Questo valore può essere impostato nella console di amministrazione. Fai clic su Impostazioni > Impostazioni sistema core > Configurazioni e specifica un valore per Timeout eliminazione documento predefinito.

**Timeout AEM Form di User Manager:** Questo valore può essere impostato modificando il file config.xml. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione, quindi fai clic su Esporta. Apri il file config.xml esportato e modifica le righe seguenti:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salva e importa nuovamente il file config.xml nella console di amministrazione.

**Timeout sessione server applicazioni:** Questo valore può essere impostato sul server applicazioni. Per ulteriori informazioni, vedere la documentazione fornita con il server applicazioni.
