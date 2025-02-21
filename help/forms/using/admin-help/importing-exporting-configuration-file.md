---
title: Importazione ed esportazione del file di configurazione
description: Scopri come importare ed esportare il file di configurazione per modificare le preferenze del server o configurare un’altra istanza di prodotto di AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Importazione ed esportazione del file di configurazione {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizzare la pagina Configurazione manuale per scaricare una copia delle impostazioni di configurazione in formato XML. Le impostazioni di questo file controllano tutte le preferenze del server. Puoi quindi modificare il file e caricarlo nuovamente sul server. È inoltre possibile utilizzare il file per configurare un&#39;altra istanza del prodotto AEM Forms.

Per evitare rischi di protezione, il valore della password di associazione per il server delle directory non viene incluso in un file di configurazione esportato. Aggiornare la password nel file XML prima di importare il file in un nuovo sistema.

>[!NOTE]
>
>L’importazione del file di configurazione riconfigura i moduli AEM in base alle informazioni contenute nel file. Solo un amministratore di sistema o un consulente di servizi professionali che ha familiarità con il prodotto AEM Forms e con il linguaggio XML può valutare la possibilità di modificare il file di configurazione. Potrebbe essere necessario modificare il file di configurazione, ad esempio, per riconfigurare un&#39;impostazione danneggiata.

**Esporta le informazioni di configurazione**

1. In Administration Console, fare clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Esporta. Se si utilizza Microsoft Internet Explorer, viene richiesto di specificare il percorso in cui salvare il file. Se utilizzi Firefox, il file viene salvato sul desktop.

**Importa le informazioni di configurazione**

1. In Administration Console, fare clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Sfoglia per trovare il file di configurazione, su Importa e quindi su OK.
