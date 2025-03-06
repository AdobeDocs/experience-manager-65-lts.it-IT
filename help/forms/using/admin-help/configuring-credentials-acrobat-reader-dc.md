---
title: Configurazione delle credenziali per l'utilizzo con le estensioni di Acrobat Reader DC
description: Scopri come configurare le credenziali per l’utilizzo con le estensioni Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 040a4db1-45e1-4501-8117-d2d41d4a73ea
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Configurazione delle credenziali per l&#39;utilizzo con le estensioni di Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Per applicare i diritti di utilizzo ai documenti di PDF, configura AEM Forms con una credenziale valida per le estensioni Acrobat Reader DC. È possibile che durante l&#39;installazione di AEM Forms sia stata configurata una credenziale. Se non sono state configurate le credenziali delle estensioni di Acrobat Reader DC durante l&#39;esecuzione di Configuration Manager o se è necessario importare una credenziale nuova o sostitutiva, è possibile utilizzare le pagine Gestione archivio fonti attendibili.

Se utilizzi una credenziale di valutazione, sostituiscila con una credenziale di produzione durante il passaggio all’ambiente di produzione. Per aggiornare una credenziale scaduta o di valutazione, eliminare innanzitutto la credenziale precedente delle estensioni DC di Acrobat Reader.

Per informazioni su come ottenere le credenziali, vedere [Preparazione all&#39;installazione di AEM Forms (server singolo)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

L&#39;archivio fonti attendibili può contenere più di una credenziale delle estensioni di Acrobat Reader DC. Imposta una di queste credenziali come credenziale predefinita delle estensioni di Reader. Le credenziali predefinite vengono utilizzate quando un utente di Workbench non è in grado di determinare quali credenziali utilizzare durante la creazione del processo. Queste regole si applicano alle credenziali predefinite:

* Se si importa una credenziale Acrobat Reader DC Extensions e l&#39;archivio fonti attendibili non contiene altre credenziali Acrobat Reader DC Extensions, questa verrà impostata come predefinita.
* Se si importa una credenziale Acrobat Reader DC Extensions con l&#39;opzione Default selezionata, il tipo predefinito viene rimosso da una credenziale predefinita esistente. Le credenziali importate diventano predefinite.
* Non è possibile eliminare una credenziale predefinita di Acrobat Reader DC Extensions. Per eliminare le credenziali predefinite, impostare innanzitutto un&#39;altra credenziale come predefinita. Un&#39;eccezione a questa regola è che se è presente una sola credenziale, è possibile eliminarla anche se è l&#39;impostazione predefinita.
* Non è possibile aggiornare una credenziale predefinita di Acrobat Reader DC Extensions.

>[!NOTE]
>
>È inoltre possibile importare ed eliminare le credenziali a livello di programmazione. (Vedi [Programmazione con AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).)

## Importare una credenziale Estensioni DC Acrobat Reader {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fare clic su Importa e in Tipo archivio fonti attendibili selezionare Credenziali estensioni DC Acrobat Reader.
1. (Facoltativo) Per indicare che questa credenziale è quella predefinita da utilizzare con le estensioni di Acrobat Reader DC, selezionare Predefinita.
1. Nella casella Alias digitare un identificatore per le credenziali. Questo identificatore viene utilizzato come nome visualizzato per le credenziali nelle estensioni Acrobat Reader DC. Questo alias viene utilizzato anche per accedere alle credenziali a livello di programmazione tramite AEM Form SDK.

   >[!NOTE]
   >
   >Il nome dell’alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome dell&#39;alias non fa distinzione tra maiuscole e minuscole quando vi si fa riferimento in un processo.

1. Fare clic su Scegli file per individuare le credenziali, digitare la password delle credenziali e quindi fare clic su OK.

   Se viene visualizzato il messaggio di errore &quot;Impossibile importare le credenziali a causa di un formato di file errato o di una password errata&quot;, verificare che la password sia valida.

## Rimuovere le credenziali di un&#39;estensione DC Acrobat Reader {#remove-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Selezionare le credenziali e fare clic su Elimina.

## Sostituire una credenziale delle estensioni DC di Acrobat Reader {#replace-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Prendere nota dell&#39;alias della credenziale esistente, quindi selezionarlo e fare clic su Elimina.
1. Importa la nuova credenziale utilizzando lo stesso alias.
