---
title: Aggiornamento ad AEM 6.5 Forms LTS su OSGi
description: È possibile eseguire un aggiornamento diretto da AEM 6.5.22.0 Forms a AEM 6.5 Forms LTS.
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: dd45dfe953a111ccbbc71e8e25a8a2577037587a
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# Aggiornamento ad AEM 6.5 Forms LTS su OSGi {#upgrade-to-aem-forms-osgi}

Per [eseguire l&#39;aggiornamento da AEM 6.5 a AEM 6.5 LTS](/help/sites-deploying/upgrade.md), eseguire l&#39;aggiornamento a AEM 6.5.22.0 Forms o versione successiva. È supportato un aggiornamento diretto da AEM 6.5.22.0 a AEM 6.5 Forms LTS.

Se utilizzi AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms, AEM 6.3 Forms, AEM 6.4 Forms o AEM 6.5 Forms, non è disponibile un aggiornamento diretto a AEM 6.5 Forms LTS. Per i percorsi di aggiornamento dettagliati, consulta la documentazione sui [percorsi di aggiornamento](/help/forms/using/upgrade.md).

Dopo l&#39;aggiornamento al service pack AEM Forms 6.5.22.0, eseguire la procedura seguente per eseguire l&#39;aggiornamento ad AEM 6.5 LTS Forms:

1. Installa il pacchetto del componente aggiuntivo AEM Forms. I passaggi sono elencati di seguito:

   1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
   1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
   1. Nella sezione **[!UICONTROL Filtri]**:
      1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
      1. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
   1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
   1. Apri [Gestione pacchetti](/help/sites-administering/package-manager.md) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
   1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

      Puoi scaricare il pacchetto anche utilizzando il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

      Dopo l’installazione del pacchetto, viene richiesto di riavviare l’istanza di AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel file &lt;crx-repository>/error.log e che il registro sia stabile. Inoltre, alcuni pacchetti possono rimanere nello stato di installazione. Puoi ignorare lo stato di questi pacchetti.


      **Riavviare l&#39;istanza di AEM con i seguenti parametri della riga di comando JVM aggiuntivi**:
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      Se il server viene avviato tramite uno script o un servizio, aggiornarlo di conseguenza in modo da includere quanto riportato sopra, in modo che siano effettivi anche dopo i riavvii successivi.

      >[!NOTE]
      >
      > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Eseguire attività successive all&#39;installazione.

   * **Esegui utilità di migrazione**

     L’utility di migrazione rende compatibili con AEM 6.5 forms i moduli adattivi e le risorse di gestione della corrispondenza delle versioni precedenti. Puoi scaricare l’utility da AEM Software Distribution. Per informazioni dettagliate sulla configurazione e l&#39;utilizzo dell&#39;utilità di migrazione, vedere [utilità di migrazione](../../forms/using/migration-utility.md).

     Se si utilizza [Esempio per l&#39;integrazione del componente Bozze e invii](https://helpx.adobe.com/it/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con il database e l&#39;aggiornamento da una versione precedente, eseguire le query SQL seguenti dopo l&#39;aggiornamento:

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(Se si esegue l&#39;aggiornamento da AEM 6.2 Forms o solo dalle versioni precedenti) Riconfigura Adobe Sign**

     Se nella versione precedente di AEM Forms hai configurato Adobe Sign, riconfigura Adobe Sign da AEM Cloud Services. Per ulteriori dettagli, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Supporto per jQuery**

     In AEM 6.5 Forms, la versione di jQuery è aggiornata alla 3.2.1 e la versione dell’interfaccia utente jQuery è aggiornata alla 1.12.1. AEM Form utilizza JQuery in modalità **noConflict**. Pertanto, se utilizzi un’altra versione di jQuery, non vengono visualizzati problemi durante l’esecuzione di un aggiornamento. Tuttavia, quando esegui l’aggiornamento a AEM 6.5 Forms:

      * Assicurati che gli eventuali componenti personalizzati siano compatibili con le versioni di jQuery supportate.
      * Rimuovi le API non supportate dai componenti personalizzati. Per l&#39;elenco delle API rimosse, consulta la [guida all&#39;aggiornamento](https://jquery.com/upgrade-guide/3.0/). Ad esempio, viene rimosso il supporto per le API load(), .unload() ed .error(). Utilizza il metodo .on() al posto delle API di cui sopra. Ad esempio, modificare $(&quot;img&quot;).load(fn) in $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Se si esegue l&#39;aggiornamento da AEM 6.2 Forms o solo da versioni precedenti) Riconfigura analisi e report**

     In AEM 6.4 Forms, la variabile di traffico per la sorgente e l’evento di successo per le impression non sono disponibili. Pertanto, quando esegui l’aggiornamento da AEM 6.2 Forms o versioni precedenti, AEM Forms smette di inviare dati al server Adobe Analytics e i rapporti di analisi per i moduli adattivi non sono disponibili. Inoltre, AEM 6.4 Forms introduce la variabile di traffico per la versione di analisi dei moduli e l’evento di successo per la quantità di tempo trascorso su un campo. Quindi, riconfigura le analisi e i rapporti per il tuo ambiente AEM Forms. Per i passaggi dettagliati, vedi [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).

1. Verificare che il server sia stato aggiornato correttamente, che anche tutti i dati siano stati migrati correttamente e che possa funzionare normalmente.

   * **Verifica lo stato dei bundle:** Verifica che tutti i bundle siano in stato attivo.
   * **Verifica replica e replica inversa:** Pubblicare, compilare e inviare alcuni moduli migrati. Verifica anche i dati inviati.
   * **Verificare l&#39;accesso alle interfacce utente amministratore e sviluppatore:** Accedere all&#39;istanza di AEM da un account amministratore e verificare di disporre dell&#39;accesso ai seguenti URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >In AEM 6.4 Forms, la struttura dell’archivio crx è cambiata. Se esegui l’aggiornamento da Forms 6.3 a AEM 6.5 Forms, utilizza i percorsi modificati per la personalizzazione che crei nuovamente. Per l&#39;elenco completo dei percorsi modificati, vedere [Ristrutturazione dell&#39;archivio Forms in AEM](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5).
