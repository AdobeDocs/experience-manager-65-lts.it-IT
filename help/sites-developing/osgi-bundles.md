---
title: Bundle OSGi
description: Scopri alcuni suggerimenti per la gestione dei bundle OSGi in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 1688ac19-b7fb-4c52-b04f-9126a3f72ac7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Bundle OSGi{#osgi-bundles}

## Usa controllo delle versioni semantiche {#use-semantic-versioning}

Le best practice concordate per la numerazione delle versioni semantiche sono disponibili all&#39;indirizzo [https://semver.org/](https://semver.org/).

## Non incorporare più classi e file jar di quanto strettamente necessario nei bundle OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Le librerie comuni devono essere suddivise in bundle separati. Questo ne consente il riutilizzo in tutti i bundle. Quando esegui il wrapping di un *JAR* in un bundle OSGi, assicurati di controllare le origini online per verificare se qualcuno ha già eseguito l&#39;operazione in precedenza. Alcuni luoghi comuni in cui trovare i bundle wrapper esistenti sono: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes e SpringSource Enterprise Bundle Repository.

## Dipende dalle versioni più basse necessarie del bundle {#depend-on-the-lowest-needed-bundle-versions}

Per le dipendenze in fase di compilazione nei file POM, dipende sempre dalla versione minima necessaria che espone l’API necessaria. Questo consente una maggiore compatibilità con le versioni precedenti e semplifica il backporting delle correzioni per le versioni precedenti.

## Esportare un set minimo di pacchetti dai bundle OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Quando un pacchetto è stato esportato, è stata creata un’API da cui gli altri possono dipendere. Assicurati di esportare il meno possibile e assicurati che ciò che viene esportato sia un’API. È molto più facile prendere un metodo/classe privato e renderlo pubblico che prendere qualcosa che è stato precedentemente esportato e renderlo privato.

Posiziona sempre le implementazioni in un pacchetto *impl* separato. Per impostazione predefinita, *maven-bundle-plugin* esporta qualsiasi elemento del progetto il cui nome non contiene *impl*.

## Definisci sempre in modo esplicito una versione semantica per ciascun pacchetto esportato {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Questo consente ai consumatori della tua API di evolversi insieme a te. In questo caso, segui sempre le best practice per il controllo delle versioni semantiche. Questo consente ai consumatori dell’API di sapere quali tipi di modifiche aspettarsi in una nuova versione.

## Includi informazioni sul metatipo se esposte {#include-metatype-information-where-exposed}

Specificando informazioni significative sui metatipi, è più facile comprendere i servizi e i componenti nella console Felix. Un elenco di annotazioni e attributi SCR è disponibile all&#39;indirizzo: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
