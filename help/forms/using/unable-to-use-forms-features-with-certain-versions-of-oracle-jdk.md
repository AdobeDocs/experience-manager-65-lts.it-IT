---
title: Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK
description: Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

Il problema si applica alle seguenti versioni:

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problema   {#issue}

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

   `-Djdk.xml.xpathExprOpLimit=2000`

   Imposta la proprietà di sistema in JVM a un valore ragionevolmente alto in modo che il limite predefinito non venga raggiunto.

1. Avvia il server Experience Manager Forms.
