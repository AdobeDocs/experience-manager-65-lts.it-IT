---
title: Strumenti di sviluppo
description: Per sviluppare applicazioni JCR, Apache Sling o Adobe Experience Manager, sono disponibili diversi set di strumenti.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: 46db0690-03e9-4b31-aa44-200f224f3707
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 4%

---

# Strumenti di sviluppo{#development-tools}

Per sviluppare applicazioni JCR, Apache Sling o Adobe Experience Manager (AEM), sono disponibili i seguenti set di strumenti:

* un set composto da [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. CRXDE Lite è incorporato in CRX/AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Lite, puoi creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione e l’integrazione con SVN.

  CRXDE Lite è consigliato quando non hai accesso diretto al server CRX/AEM, quando sviluppi un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java™ o quando non hai bisogno di un debugger dedicato, del completamento del codice e dell’evidenziazione della sintassi.

* un insieme costituito dai seguenti elementi:
   * Un ambiente di sviluppo integrato. [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md).
   * Uno strumento di generazione. Ad esempio, [Apache Maven](/help/sites-developing/ht-projects-maven.md).
   * FileVault che è stato sviluppato da Adobe per mappare un archivio su un file system, un sistema di controllo della versione. Ad esempio, Subversion.
   * Un sistema di tracciamento dei bug. Per esempio, Jira.
   * Un sistema centrale di gestione delle dipendenze. Ad esempio, Apache Archiva.
   * E un sistema di automazione della build. Ad esempio, Apache Continuum.

  Questa configurazione consente di integrare completamente l’applicazione (contenuto, codice, configurazione) in qualsiasi ambiente e processo di sviluppo. Il collegamento tra i diversi elementi è la rappresentazione del file system dell’archivio tramite FileVault, in quanto tutti gli strumenti di sviluppo precedentemente menzionati possono funzionare con i file.

## Estensioni per ambienti di sviluppo integrati {#extensions-for-integrated-development-environments}

Adobe ha rilasciato le seguenti estensioni:

* [Estensione AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Estensione AEM Brackets](/help/sites-developing/aem-brackets.md)

### Altri strumenti {#other-tools}

AEM viene fornito con altri strumenti che facilitano lo sviluppo:

* [Editor finestre di dialogo](/help/sites-developing/dialog-editor.md)
* [Utilizzo di Translator per gestire i dizionari](/help/sites-developing/i18n-translator.md)
* [Gestione dei pacchetti tramite Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Come sviluppare progetti AEM utilizzando Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Come sviluppare progetti AEM utilizzando IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md)
* [Come utilizzare lo strumento Server proxy](/help/sites-developing/ht-proxy-server.md)
* [Strumenti AEM Modernization Tools](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Strumenti che facilitano la creazione di nuovi progetti:

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [Modelli AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Il seguente tutorial potrebbe essere utile per avviare un nuovo progetto AEM:
>[Guida introduttiva ad AEM Sites Parte 1 - Configurazione del progetto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
