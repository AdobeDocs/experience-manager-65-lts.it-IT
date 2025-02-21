---
title: Importazione ed esportazione di file di configurazione di PDF Generator
description: Scopri come importare ed esportare i file di configurazione di PDF Generator.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Importazione ed esportazione di file di configurazione di PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il file di configurazione contiene le informazioni sulla conversione di PDF Generator, inclusi PDF, tipo di file e impostazioni di protezione.

>[!NOTE]
>
>Non è possibile modificare l&#39;impostazione di timeout per PDF Generator importando un file nativo2pdfconfig.xml personalizzato. L’impostazione di timeout in tale file è solo a scopo informativo e mostra l’impostazione corrente in PDF Generator. Per modificare l&#39;impostazione del timeout, vedere &quot;Impostazione dei parametri delle prestazioni di PDF Generator&quot; in [Installazione e distribuzione di AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Esporta il file di configurazione corrente {#export-your-current-configuration-file}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Esporta configurazione.
1. Per esportare le impostazioni, selezionare l&#39;opzione appropriata:

   * Per esportare tutte le impostazioni denominate, selezionare Scarica configurazione completa.
   * Per esportare solo un&#39;impostazione di Adobe PDF, un&#39;impostazione di protezione o un&#39;impostazione del tipo di file, selezionare Scarica configurazione minima.

     Se stai esportando una configurazione minima, seleziona le impostazioni Adobe PDF, sicurezza e tipo di file da esportare.

1. Fare clic su Scarica e salvare il file XML nella posizione appropriata.

## Importare un file di configurazione {#import-a-configuration-file}

>[!NOTE]
>
>Il sistema verrà riconfigurato in base alle informazioni contenute nel file importato.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Seleziona Importa Un File Di Configurazione Esistente.
1. Per specificare il percorso del file nella casella File di configurazione, fare clic su Sfoglia per trovare e selezionare il file, quindi fare clic su **Importa**.

## Convertire tutti i livelli all&#39;interno di file AutoCAD {#convert-all-layers-within-autocad-files}

Per default, PDF Generator converte in PDF solo il livello di default dei file AutoCAD, anziché tutti i livelli all&#39;interno del file. Per convertire tutti i livelli, seguite questa procedura.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Esporta configurazione.
1. Seleziona Scarica configurazione completa e fai clic su Scarica.
1. In un editor di testo, aprire il file scaricato e aggiungere il testo `convertAllPages="true"` sotto il tag `AutoCAD` all&#39;interno del tag `PDFMaker`.
1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Selezionate Importa file di configurazione esistente (Import An Existing Configuration File), specificate il file aggiornato e fate clic su Importa (Import).

   Tutti i file AutoCAD convertiti utilizzando il file di configurazione modificato avranno tutti i livelli convertiti.

## Ripristina le impostazioni originali installate con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Seleziona Ripristina configurazione predefinita e fai clic su Importa.
