---
title: Hotfix per Adobe Experience Manager Forms 6.5 LTS SP1
description: Informazioni su come scaricare e installare un hotfix per AEM Forms 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 504240bdad9e964460a9fcdc555228c7cb02e314
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# Hotfix per Adobe Experience Manager Forms 6.5 LTS{#aem-form-hotfix}

Questo articolo elenca le correzioni critiche implementate per risolvere problemi noti, migliorare la stabilità del sistema e migliorare le prestazioni complessive di AEM Forms 6.5 LTS.

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
