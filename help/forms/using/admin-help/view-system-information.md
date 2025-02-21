---
title: Visualizza informazioni di sistema
description: Scopri come visualizzare i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Visualizza informazioni di sistema {#view-system-information}

Nella scheda Sistema vengono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server che esegue AEM Forms. Per accedere a queste informazioni, nella console di amministrazione fare clic su Health Monitor nell&#39;angolo superiore destro della pagina. Se si eseguono AEM Forms in un ambiente cluster, le informazioni visualizzate si riferiscono al nodo selezionato dall&#39;elenco Server.

Per salvare le informazioni di sistema correnti come file delle proprietà, fare clic su Salva.

Nel riquadro destro della scheda Sistema vengono visualizzate rappresentazioni grafiche delle seguenti informazioni:

* Elementi di lavoro e numero lavori
* Utilizzo heap e heap confermato
* Utilizzo non heap e non heap confermato

È possibile trascinare il puntatore lungo la linea temporale per ottenere i valori di un particolare punto nel tempo.

>[!NOTE]
>
>I dati del grafico, i valori delle informazioni sul server e l’ora di clock vengono aggiornati ogni 10 minuti. Le informazioni non vengono visualizzate in tempo reale.

Nel riquadro sinistro della scheda Sistema vengono visualizzate le seguenti informazioni sul server o sul nodo:

**Macchina virtuale:** versione di Java Virtual Machine (JVM) nel server.

**Fornitore macchina virtuale:** produttore della JVM.

**Versione macchina virtuale:** Numero versione JVM

**Nome computer:** Nome host del server in cui è installato AEM Forms.

**Tempo di attività:** il tempo, in ore e minuti, in cui il server è in esecuzione.

**Compilatore JIT:** Nome del compilatore utilizzato.

**Tempo di compilazione:** Tempo impiegato per la compilazione.

**Numero di Live Threads:** il numero totale di thread attualmente presenti nel sistema AEM Forms.

**Numero massimo di Threads:** Il numero massimo di thread live mai registrati nel sistema.

**Numero di classi caricate:** Numero di classi caricate nella JVM.

**Numero di classi scaricate:** Numero di classi scaricate dalla JVM.

**Heap minimo:** La quantità minima di heap utilizzata.

**Memoria heap massima:** La quantità massima di heap utilizzata.

**Nome sistema operativo:** Il nome del sistema operativo in esecuzione sul server AEM Forms.

**Versione sistema operativo:** Numero di versione del sistema operativo in esecuzione sul server AEM Forms.

**Arco sistema operativo:** Architettura del sistema operativo su cui è in esecuzione JVM.

**Numero di processori:** Numero di processori nel sistema.

**Argomenti macchina virtuale:** Argomento utilizzato da JVM.

**Percorso classe:** Percorso di classe utilizzato da JVM.

**Percorso libreria:** Percorso della libreria utilizzato da JVM.

**Percorso classe di avvio:** Percorso della classe di avvio utilizzato dalla JVM.

**Tipo di server applicazioni:** Tipo di server applicazioni utilizzato per eseguire AEM Forms.

**Versione server applicazioni:** Numero di versione del server applicazioni utilizzato per eseguire AEM forms.

**Fornitore server applicazioni:** Produttore del server applicazioni utilizzato per eseguire AEM Forms.

**Data di installazione:** Data (in formato aaaa-mm-gg) in cui è stato installato AEM Forms.

**AEM Forms versione:** versione di AEM Forms installata.

**Versione patch:** numero patch AEM Forms.

**Nome database:** Tipo di database utilizzato da AEM Forms.

**Versione database:** Numero di versione del database utilizzato da AEM Form.

**Nome unità di database:** Il nome del driver utilizzato dalla JVM per connettersi al database.

**Versione driver di database:** versione del driver utilizzata dalla JVM per connettersi al database.

Il pulsante **Salva** consente di salvare le informazioni di sistema in un file delle proprietà.
