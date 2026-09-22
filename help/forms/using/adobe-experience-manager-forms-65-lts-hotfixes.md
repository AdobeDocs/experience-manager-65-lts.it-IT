---
title: Hotfix per Adobe Experience Manager Forms 6.5 LTS
description: Informazioni su come scaricare e installare un hotfix per AEM Forms 6.5 LTS. Per AEM 6.5 (non LTS), consulta l’articolo sugli hotfix di AEM 6.5 Forms.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: e485100f-3e16-4fd4-a8ce-af771d765dd1
source-git-commit: 989d83cfc56f7a7d4e2aea5a7ac1ca444d505859
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%
---
# Hotfix per Adobe Experience Manager Forms 6.5 LTS{#aem-form-hotfix}

Questo articolo elenca le correzioni critiche implementate per risolvere problemi noti, migliorare la stabilità del sistema e migliorare le prestazioni complessive di AEM Forms 6.5 LTS.


Questo articolo si applica ad AEM Forms 6.5 LTS. Per le distribuzioni di AEM 6.5 (non LTS), vedi [Hotfix di Adobe Experience Manager Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/release-notes/aem-forms-hotfix).

>[!NOTE]
>
> Gli hotfix sono progettati per essere cumulativi e comprendono tutte le correzioni precedenti. Quando applichi l’aggiornamento rapido più recente a una versione, questo non solo risolve il problema più recente, ma incorpora anche tutte le correzioni di bug e i miglioramenti precedenti.

## Hotfix per AEM Forms 6.5 LTS {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Collegamento per il download degli hotfix (collegamento per la distribuzione di software AEM)</strong></td>
    <td><strong>Problemi risolti</strong></td>
  </tr>
  <tr>
    <td>
      <strong>21 settembre 2026</strong><br>
      <em>Applicabile a:</em> distribuzioni AEM Forms 6.5 LTS Service Pack 2 JEE (JBoss, WebLogic, WebSphere)<br>
    </td>
    <td>
    <p><strong>Per installare questo aggiornamento rapido, completa i passaggi seguenti nell’ordine in cui:</strong></p>
    <p><strong>Passaggio 1: installare la patch</strong></p>
    <ul>
    <strong>JBoss:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-jboss.zip">Hotfix per AEM Forms 6.5 LTS SP2 su Windows per il server JEE JBoss</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-jboss.tar.gz">Hotfix per AEM Forms 6.5 LTS SP2 su Linux per il server JEE JBoss</a></li>
    <strong>WebLogic:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-weblogic.zip">Hotfix per AEM Forms 6.5 LTS SP2 su Windows per il server JEE Weblogic</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-weblogic.tar.gz">Hotfix per AEM Forms 6.5 LTS SP2 su Linux per il server JEE Weblogic</a></li>
    <strong>WebSphere:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-websphere.zip">Hotfix per AEM Forms 6.5 LTS SP2 su Windows per il server WebSphere JEE</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-websphere.tar.gz">Hotfix per AEM Forms 6.5 LTS SP2 su Linux per il server WebSphere JEE</a></li>
    </ul>
    <p>Installare la patch utilizzando la procedura standard di installazione patch di AEM Forms su JEE. <!-- TODO: link to the 6.5 LTS JEE patch installation instructions once available --></p>
    <p><strong>Passaggio 2: installare il bundle di correzione della vulnerabilità</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/SP2LTSBundles_VULN-36670.zip">Pacchetto di correzione delle vulnerabilità per AEM Forms 6.5 LTS SP2</a></li>
    </ul>
    <ol>
    <li>Apri la console OSGi in <code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>.</li>
    <li>Fare clic su <strong>Installa/Aggiorna</strong>.</li>
    <li>Selezionare le caselle di controllo <strong>Avvia bundle</strong> e <strong>Aggiorna pacchetti</strong>.</li>
    <li>Fare clic su <strong>Scegli file</strong>, quindi caricare il bundle scaricato.</li>
    <li>Attendi che il registro venga settato e che il bundle venga visualizzato come <strong>Attivo</strong>.</li>
    </ol>
    <p><strong>Passaggio 3: aggiornare il programma di installazione di AEM Forms Workbench</strong></p>
    <p>È necessario eseguire l’aggiornamento al programma di installazione di AEM Forms Workbench più recente. Scaricala dal <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/fd/workbench/6-5-0-20260902-1-45/Workbench_DVD.zip">programma di installazione di AEM Forms Workbench</a>.</p>
    <p><strong>Passaggio 4: aggiornare i file della libreria client (sviluppatori)</strong></p>
    <p>Questa patch include un aggiornamento importante alla libreria client SDK <code>adobe-livecycle-client.jar</code> (vedi <a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">Inclusi i file della libreria Java AEM Forms</a>). Se il progetto utilizza questo file JAR, aggiorna <code>adobe-livecycle-client.jar</code> nel percorso di classe del progetto dopo aver installato l'aggiornamento rapido. La versione più recente è disponibile alle <code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>.</p>
    <p>L'hotfix è cumulativo, pertanto è possibile applicarlo ad AEM Forms 6.5 LTS Service Pack 2 o a un Service Pack precedente senza prima installare Service Pack 2.</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26818</b> Dopo l'aggiornamento di Apache Shiro alla versione 2.1.0, AEM Forms su JEE non viene avviato con un <code>NoClassDefFoundError</code> per il gestore della sicurezza di Shiro. Questo hotfix ripristina l’avvio automatico riuscito.</li>
    <li><b>FORMS-26819</b> AEM Forms su JEE ha esito negativo con un errore "nessuna classe trovata" per <code>org.owasp.esapi.reference.JavaLogFactory</code>. Questo hotfix risolve la classe mancante.</li>
    <li><b>FORMS-26584, FORMS-26589</b> Dopo l'aggiornamento ad AEM Forms 6.5 LTS, gli endpoint di TaskManager vengono rimossi. Questo hotfix ripristina gli endpoint di TaskManager.</li>
    <li><b>FORMS-26569</b> In JEE il passaggio MergeEars di Configuration Manager non riesce e viene restituito un errore di dichiarazione DOCTYPE (<code>ALC-LCM-010-200</code>) a causa del generatore XML protetto. Questo hotfix consente il completamento del passaggio MergeEars.</li>
    <li><b>FORMS-25063</b> registri a livello di applicazione mancanti nelle distribuzioni IBM WebSphere Liberty. Questo aggiornamento rapido ripristina la registrazione a livello di applicazione.</li>
    <li><b>FORMS-24892</b> In JBoss, l'e-mail non riesce se "IMAPProvider non è un sottotipo". Questo aggiornamento rapido ripristina la funzionalità e-mail su JBoss.</li>
    <li><b>FORMS-24692</b> In WebSphere Liberty Profile (WLP), l'e-mail non riesce e viene visualizzato il messaggio "Impossibile convertire il socket in TLS". Questo hotfix ripristina le e-mail su TLS su WLP.</li>
    <li><b>FORMS-26688</b> Aggiorna la libreria Gibson alla versione 6.0.29665850.</li>
    <li><b>FORMS-25222</b> esegue il backport dei miglioramenti di convalida delle asserzioni SAML.</li>
    <li><b>FORMS-26733, FORMS-26734</b> Apache Log4j è stato aggiornato alla versione 2.25.5.</li>
    <li>Questo hotfix include anche correzioni di sicurezza.</li>
    </ul>
    <p><strong>Build:</strong> AEMForms-6.6.0-0008</p>
    </td>
  </tr>
  <tr>
    <td>
      <strong>9 settembre 2025</strong><br>
    <td>
    <ul>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Hotfix2 per AEM Service Pack 6.5 LTS su Windows</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Hotfix2 per AEM Service Pack 6.5 LTS su Linux</a></li>
     <li>MacOS- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">Hotfix2 per AEM Service Pack 6.5 LTS su MacOS</a></li>
    <td>
    <ul>
    <li>È stata migliorata l’affidabilità dell’invio dei moduli, risolvendo un problema che poteva causare errori nell’invio quando è stato abilitato Server-Side Validation (SSV). In caso di problemi, contatta [Supporto Adobe Experience Manager Forms](https://business.adobe.com/in/support/main.html)
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Scaricare e installare un aggiornamento rapido OSGi {#download-install-hotfix}

Per scaricare e installare l’Hotfix, effettua le seguenti operazioni:

1. Scarica [Hotfix](#hotfix-for-adaptive-forms) dal collegamento Software Distribution.
1. Estrai il file di archivio Hotfix per ottenere un pacchetto Experience Manager (.zip) e i file bundle (.jar).
1. Carica e installa il pacchetto (.zip) tramite [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Apri i bundle di Gestione configurazione `https://server:host/system/console/bundles`, carica e installa il bundle (.jar). L&#39;aggiornamento rapido è installato.
