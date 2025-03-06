---
title: Creare tabelle complesse accessibili in moduli HTML5
description: Scopri come creare tabelle accessibili nei moduli di HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: e6e6c08a-3bed-4713-a0e0-2a02607c7fc7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Creare tabelle complesse accessibili in moduli HTML5 {#create-accessible-complex-tables-in-html-forms}

L’implementazione predefinita delle tabelle in HTML5 Forms utilizza gli elementi DIV di HTML per eseguire il rendering di una tabella. Il rendering prevede l’utilizzo dei ruoli ARIA per soddisfare i requisiti di accessibilità.

Per evitare problemi di accessibilità con gli assistenti vocali che non supportano completamente i ruoli ARIA utilizzati con le tabelle dati, HTML5 Forms fornisce una rappresentazione alternativa per le tabelle. Queste tabelle si basano sul nuovo formato di tabella introdotto in Designer che supporta anche:

* Intestazioni di riga
* Estensione riga

Per utilizzare il nuovo formato in HTML5 Forms, contrassegna la tabella come complessa. Per contrassegnare la tabella come complessa, aggiungere il tag `extras` nell&#39;origine XML della sottomaschera di tabella nel modo seguente:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Le tabelle contrassegnate come *complexTable* seguono il rendering nativo di HTML e forniscono un migliore supporto per l&#39;accesso facilitato ad alcuni assistenti vocali.  Per creare un&#39;estensione di riga, selezionare celle consecutive di una tabella nella stessa colonna, fare clic con il pulsante destro del mouse sulla selezione e quindi scegliere **[!UICONTROL Unisci celle]**.

>[!NOTE]
>
>La creazione di un&#39;estensione di riga funziona solo per le celle più a sinistra.

Per contrassegnare una riga come intestazione di riga, selezionare tutte le celle nella riga, fare clic con il pulsante destro del mouse sulla selezione e quindi scegliere **[!UICONTROL Contrassegna intestazione]**.

Per contrassegnare una cella come intestazione di colonna, selezionare una cella qualsiasi nella colonna, fare clic con il pulsante destro del mouse sulla selezione e quindi scegliere **[!UICONTROL Contrassegna intestazione]**.

Limitazioni nel nuovo formato *AccessibleTable*:

* Mancanza di supporto per i campi espandibili se nella tabella viene utilizzato rowspan
* Tabelle nidificate (tabelle all’interno di celle di tabella) non supportate
* Il supporto per rowspan è limitato alle righe e alle celle di intestazione
* Il supporto è limitato alle tabelle regolari
* Nelle tabelle con rowspan > 1 non è supportato alcun tipo di precompilazione dei dati
