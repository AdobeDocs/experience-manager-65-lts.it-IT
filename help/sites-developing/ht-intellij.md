---
title: Come sviluppare progetti AEM utilizzando IntelliJ IDEA
description: Scopri come utilizzare IntelliJ IDEA per sviluppare progetti Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: 4def21ee-d7de-45a8-a7df-062dd2d1a3ba
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 2%

---

# Come sviluppare progetti AEM utilizzando IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Panoramica {#overview}

Per iniziare a sviluppare AEM su IntelliJ, sono necessari i seguenti passaggi.

Ogni passaggio è descritto più dettagliatamente nel resto di questo argomento.

* Installa IntelliJ
* Configurare il progetto AEM basato su Maven
* Preparare il supporto JSP per IntelliJ nel POM Maven
* Importare il progetto Maven in IntelliJ

>[!NOTE]
>
>Questa guida si basa su IntelliJ IDEA Ultimate Edition 12.1.4 e AEM 5.6.1.

### Installa IntelliJ IDEA {#install-intellij-idea}

Scarica IntelliJ IDEA da [la pagina Download in JetBrains](https://www.jetbrains.com/idea/download/).

Quindi, seguire le istruzioni di installazione riportate in quella pagina.

### Configurare il progetto AEM basato su Maven {#set-up-your-aem-project-based-on-maven}

Quindi, configura il tuo progetto utilizzando Maven come descritto in [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md).

Per iniziare a utilizzare i progetti AEM in IntelliJ IDEA, è sufficiente la configurazione di base in [Guida introduttiva tra 5 minuti](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html).

### Preparare il supporto JSP per IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA può anche fornire supporto nell’utilizzo di JSP, ad esempio:

* completamento automatico delle librerie di tag
* conoscenza degli oggetti definiti da `<cq:defineObjects />` e `<sling:defineObjects />`

Affinché ciò funzioni, segui le istruzioni in [Come lavorare con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importare il progetto Maven {#import-the-maven-project}

1. Apri la finestra di dialogo **Importa** in IntelliJ IDEA tramite

   * se non hai ancora aperto un progetto, seleziona **Importa progetto** nella schermata di benvenuto
   * selezionando **File > Importa progetto** dal menu principale

1. Nella finestra di dialogo Importa, seleziona il file POM del progetto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continua con le impostazioni predefinite, come mostrato nella finestra di dialogo seguente.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continuare le seguenti finestre di dialogo facendo clic su **Avanti** e **Fine**.
1. Ora sei configurato per lo sviluppo AEM utilizzando IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Debug di JSP con IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Per il debug di JSP con IntelliJ IDEA sono necessari i passaggi seguenti

* Configurare un facet web nel progetto
* Installare il plug-in di supporto JSR45
* Configurare un profilo di debug
* Configurare AEM per la modalità di debug

#### Configurare un facet web nel progetto {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA deve capire dove trovare le JSP per il debug. Poiché IDEA non è in grado di interpretare le impostazioni di `content-package-maven-plugin`, è necessario configurarle manualmente.

1. Vai a **File > Struttura progetto**
1. Seleziona il modulo **Contenuto**
1. Fai clic su **+** sopra l&#39;elenco dei moduli e seleziona **Web**
1. Come directory delle risorse Web, seleziona `content/src/main/content/jcr_root subdirectory` del progetto come mostrato nella schermata seguente.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Installare il plug-in di supporto JSR45 {#install-the-jsr-support-plugin}

1. Vai al riquadro **Plug-in** nelle impostazioni IntelliJ IDEA
1. Passa al plug-in **Integrazione JSR45** e seleziona la casella di controllo accanto
1. Fai clic su **Applica**
1. Riavvia IntelliJ IDEA quando richiesto a

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configurare un profilo di debug {#configure-a-debug-profile}

1. Vai a **Esegui > Modifica configurazioni**
1. Premi **+** e seleziona **JSR45 Remote**
1. Nella finestra di dialogo di configurazione, seleziona **Configura** accanto a **Server applicazioni** e configura un server generico
1. Impostare la pagina iniziale su un URL appropriato per aprire un browser all&#39;avvio del debug
1. Rimuovi tutte le **attività Prima del lancio** se utilizzi la sincronizzazione automatica vlt o configura le attività Maven appropriate se non la esegui
1. Nel riquadro **Avvio/Connessione**, regolare la porta, se necessario
1. Copiare gli argomenti della riga di comando proposti da IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurare AEM per la modalità di debug {#configure-aem-for-debug-mode}

L’ultimo passaggio necessario consiste nell’avviare AEM con le opzioni JVM proposte da IntelliJ IDEA.

Avvia direttamente il file jar di AEM e aggiungi queste opzioni, ad esempio, con la seguente riga di comando:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

È inoltre possibile aggiungere queste opzioni allo script iniziale in `crx-quickstart/bin/start` come illustrato di seguito.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Avvia debug {#start-debugging}

Ora è tutto configurato per il debug dei JSP in AEM.

1. Seleziona **Esegui > Debug > Profilo di debug**
1. Impostare i punti di interruzione nel codice del componente
1. Accedere a una pagina nel browser

![chlimage_1-52](assets/chlimage_1-52a.png)

### Debug dei bundle con IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

È possibile eseguire il debug del codice nei bundle utilizzando una connessione di debug remoto standard generica. Puoi seguire la [documentazione di Jetbrain sul debug remoto](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
