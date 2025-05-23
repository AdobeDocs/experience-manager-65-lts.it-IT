---
title: Definizione dei test case
description: I test case devono essere basati sui casi d’uso e sulle specifiche dettagliate dei requisiti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 29943019-6ff2-440e-8cf8-4b92b0408021
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Definizione dei test case{#defining-your-test-cases}

I test case devono essere basati su:

**Casi d’uso**

* Definiscono le funzionalità richieste in termini di interazione tra gli attori (ruoli che avviano determinate azioni) e il sistema.
* I casi d’uso devono essere definiti dal cliente.

**Specifiche dettagliate dei requisiti**

* Tutti i requisiti funzionali e prestazionali devono essere testati.

I test dovrebbero definire chiaramente:

* Prerequisiti, che possono riguardare sistemi, configurazioni o esperienze tester specifiche.
* Passaggi da seguire; a un livello di dettaglio adeguato.
* Risultati previsti.
* Cancella i criteri per il superamento o il fallimento.

La prospettiva di automatizzare i test case è interessante perché elimina le attività ripetitive.

## Test manuali e automatizzati {#manual-versus-automated-tests}

Tuttavia, automatizzare i test case è un investimento significativo, pertanto alcuni aspetti dovrebbero essere presi in considerazione:

* Richiedi tempo, fatica ed esperienza per l&#39;impostazione e la configurazione.
* Se basati su browser, aumenta il rischio di problemi durante l’installazione degli aggiornamenti del browser, che richiedono ulteriore tempo per la correzione.
* Valido solo per grandi progetti.
* Questa opzione è utile quando vengono generate più versioni a scopo di test o nel piano di rilascio a lungo termine.

## Verifica di aspetti specifici {#testing-specific-aspects}

Durante il test di AEM, sono di particolare interesse alcuni dettagli specifici:

**Ambienti Author e Publish**

Anche se trattato in [Ambienti](/help/sites-developing/the-basics.md#environments), vale la pena evidenziare un fattore decisivo di AEM riguardo ai test.

Considera AEM come due applicazioni:

* ambiente *Author*
Questa istanza consente agli autori di inserire e pubblicare contenuti.
Questo ha un piccolo(i) set prevedibile di utenti, per i quali sono fondamentali funzionalità e prestazioni specifiche.

* ambiente *Pubblica*
Questa istanza presenta il sito web nel relativo modulo pubblicato per l’accesso da parte dei visitatori.
Questo di solito ha un set più ampio di utenti, dove il volume di traffico non è sempre prevedibile al 100%. Le prestazioni sono ancora cruciali, quando si risponde alle richieste. Considera anche la memorizzazione nella cache e il bilanciamento del carico.

Anche se lo stesso software come tale, essi:

* per scopi diversi
* hanno requisiti diversi in termini di funzionalità e prestazioni
* sono configurati in modo diverso
* sono sintonizzati separatamente
* ciascuno di essi dispone di una propria serie di test di accettazione

In altre parole, devono essere testati separatamente e con test case diversi.

**Personalizzazione**

Durante il test di personalizzazione, ogni singolo caso d’uso deve essere ripetuto utilizzando più account utente per dimostrare il comportamento.

Verificare il comportamento corretto anche nella cache.

**Dispatcher**

La maggior parte dei progetti installa il Dispatcher per il caching e il bilanciamento del carico.

Il test è difficile (la memorizzazione in cache si verifica a vari livelli e in varie posizioni) e deve essere eseguito in modalità black box. Gli aspetti chiave da testare per sono:

* **Precisione**
Assicura che gli aggiornamenti dei contenuti vengano visualizzati dal visitatore del sito web.

* **Continuità**
Verificare che il sito Web sia ancora disponibile quando un server viene arrestato.

* **Cluster**
Utilizzato per fornire quanto segue:

   * **Failover**
Se un server ha esito negativo, l&#39;elaborazione verrà ripresa dagli altri server del cluster.

   * **Prestazioni**
Il bilanciamento del carico con failover completo aumenta le prestazioni di un cluster.
Se utilizzato per un progetto del cliente, il cluster deve essere testato per confermare il corretto funzionamento della configurazione.

## Verifica del software di terze parti {#testing-third-party-software}

Qualsiasi software di terze parti interfacciato con AEM sarà referenziato nelle Specifiche dettagliate dei requisiti.

Tutte le prove necessarie (a seconda dell’ambito definito) devono essere analizzate e si deve ottenere una prova pulita.
