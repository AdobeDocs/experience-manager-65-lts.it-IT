---
title: Esecuzione dello script non riuscita in AEM Forms 6.5 LTS con JBoss EAP 8 (Linux)
description: Durante la configurazione di JBoss EAP 8.0 in un ambiente Linux, è possibile che si verifichino alcuni errori durante l'esecuzione di script della shell o di file di avvio
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: d397e6a51ad2a52da5ccb0a690e1acd3fafcee3c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Esecuzione dello script non riuscita in AEM Forms 6.5 LTS con JBoss EAP 8 (Linux)

## Problema

Durante la configurazione di **JBoss EAP 8.0 (AEM Forms 6.5.1 LTS)** in un ambiente **Linux**, è possibile che si verifichino uno dei seguenti errori durante l&#39;esecuzione di script di shell o file di avvio:

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

Questi errori si verificano quando gli script della shell o i file di configurazione sono stati creati o modificati in un sistema **Windows** e contengono **CRLF (Carriage Return + Line Feed)** terminazioni di riga.
I sistemi Linux supportano solo **LF (Line Feed)** terminazioni di riga e le terminazioni di riga in stile Windows causano errori di esecuzione dello script.

## Si applica a

* **JBoss EAP 8.0**
* **Sistemi operativi basati su Linux/UNIX**

## Passaggi per la risoluzione dei problemi

1. **Identificare il file interessato**

   * Esaminare l&#39;output dell&#39;errore per identificare lo script o il file di configurazione `.sh` che ha causato l&#39;errore.

2. **Converti il file in formato Unix**

   * Utilizzare l&#39;utilità `dos2unix` per convertire le terminazioni di riga in stile Windows nel formato Unix:

     ```bash
     dos2unix <file_name>
     ```

   * Sostituire `<file_name>` con lo script o il file di configurazione effettivo che ha generato l&#39;errore.

3. **Ripeti se necessario**

   * Se sono interessati più script, ripetere la conversione per tutti i file `.sh` rilevanti (ad esempio gli script di avvio del programma di installazione, LCM o JBoss).

4. **Rieseguire lo script**

   * Dopo la conversione, esegui nuovamente lo script per confermare la risoluzione del problema.

Dopo aver convertito i file in terminazioni di riga Unix (LF), gli errori `/bin/sh^M` e `$'\r': command not found` vengono risolti e gli script JBoss vengono eseguiti correttamente su Linux.
