---
title: Salva moduli come modelli
description: Scopri come creare modelli da moduli con dati richiesti ripetutamente.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 5e5ce783-8d0c-421c-b938-7020215682a0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Salva moduli come modelli {#save-forms-as-templates}

A volte, quando gli utenti compilano un modulo, gli input per alcuni campi rimangono gli stessi. Per tali istanze, è possibile compilare i campi che richiedono valori identici in ogni istanza e salvare il modulo o la bozza come modello. Ora, ogni volta che crei un’istanza del modello, i campi specificati sono già compilati con i valori specificati nel modello. Consente di risparmiare tempo e fatica per compilare il modulo.

Per creare un modello, effettua le seguenti operazioni:

1. Aprire un modulo e selezionare o compilare i campi con valori pressoché identici ogni volta che lo si utilizza. È possibile includere un allegato con il modello che viene in genere aggiunto durante la compilazione del modulo.
1. Seleziona l&#39;icona **Salva come modello** ![salva_come_modello](assets/save_as_template.png). Viene visualizzata una finestra di dialogo che consente di specificare il nome del modello.
1. Specifica il nome del modello e seleziona **Salva**. Il modello viene visualizzato nella cartella dei modelli.

   Se esiste già un modello con lo stesso nome, viene visualizzata una finestra di dialogo per confermare la sovrascrittura del modello esistente. Per sostituire il modello esistente con un nuovo modello, selezionare **Continua** oppure per salvare il modello con un nome diverso, selezionare **Annulla**.

Ora è possibile aprire il modello salvato. Ogni volta che si apre un modello, viene creato un nuovo modulo o un nuovo task e nel modulo vengono visualizzati i dati e le opzioni salvati. Con i modelli è possibile modificare i dati precompilati, aggiungere un allegato, salvare come bozza, inviare l’operazione o creare un altro modello utilizzandolo. I modelli sono specifici per i dispositivi mobili e non sono sincronizzati con il server Adobe Experience Manager Forms.

È inoltre possibile eliminare un modello se non è più necessario. Per eliminare un modello, passare alla cartella dei modelli, selezionare i puntini di sospensione, quindi selezionare **Elimina modello**.

>[!NOTE]
>
>Un modello è disponibile localmente e non è sincronizzato con il server. Se si cancellano i dati locali dell’app, il modello viene eliminato.
