---
title: Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK
description: Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 4aa45f02-ff89-4e40-a15d-e62c5879a87d
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%
---
# Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

Il problema si applica alle seguenti versioni:

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problema {#issue}

L’utente riscontra la seguente eccezione:
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Motivo {#reason}

L’eccezione si verifica quando si esegue Experience Manager Forms con la versione di Oracle JDK (Java Development Kit) maggiore o uguale alle seguenti versioni:

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

La versione di Java sopra e le versioni successive includono nuovi limiti di elaborazione XML nella JVM (Java Virtual Machine) che causano il mancato funzionamento di alcune operazioni specifiche di Forms.

## Soluzione alternativa {#workaround}

1. Arresta il server Experience Manager Forms.
1. Configura il seguente argomento JVM per il server applicazioni:

   `-Djdk.xml.xpathExprGrpLimit=100`
   `-Djdk.xml.xpathExprOpLimit=10000`
   `-Djdk.xml.xpathTotalOpLimit=10000`

   Imposta la proprietà di sistema in JVM a un valore ragionevolmente alto in modo che il limite predefinito non venga raggiunto.

1. Avvia il server Experience Manager Forms.
