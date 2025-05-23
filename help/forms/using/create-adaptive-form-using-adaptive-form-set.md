---
title: Creare un modulo adattivo utilizzando un set di moduli adattivi
description: Con AEM Forms, riunisci i moduli adattivi per creare un singolo modulo adattivo di grandi dimensioni e comprenderne le funzioni.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 1e9926ca-70ef-4777-8a79-f608df80ada1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Creare un modulo adattivo utilizzando un set di moduli adattivi{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

In un flusso di lavoro, ad esempio un&#39;applicazione per l&#39;apertura di un conto bancario, gli utenti compilano più moduli. Anziché richiedere la compilazione di un set di moduli, è possibile sovrapporre i moduli e creare un modulo di grandi dimensioni (modulo padre). Quando aggiungi un modulo adattivo a un modulo più grande, questo viene aggiunto come pannello (modulo figlio). Aggiungere un set di moduli figlio per creare un modulo padre. Puoi mostrare o nascondere i pannelli in base all’input dell’utente. I pulsanti del modulo padre, ad esempio submit e reset, sovrascrivono i pulsanti del modulo figlio. Per aggiungere un modulo adattivo al modulo principale, puoi trascinare il modulo adattivo dal browser di risorse (ad esempio i frammenti di modulo adattivo).

Le funzioni disponibili sono:

* Authoring indipendente
* Mostrare/nascondere i moduli appropriati
* Caricamento lento

Funzioni quali l’authoring indipendente e il caricamento lento migliorano le prestazioni rispetto all’utilizzo di singoli componenti per creare il modulo principale.

>[!NOTE]
>
>Non è possibile utilizzare frammenti o moduli adattivi basati su XFA come moduli figlio o padre.

## Dietro le quinte {#behind-the-scenes}

Puoi aggiungere frammenti e moduli adattivi basati su XSD nel modulo principale. La struttura del modulo principale è uguale a [qualsiasi modulo adattivo](../../forms/using/prepopulate-adaptive-form-fields.md). Quando aggiungi un modulo adattivo come modulo secondario, questo viene aggiunto come pannello nel modulo principale. I dati di un modulo figlio associato vengono memorizzati nella radice `data` della sezione `afBoundData` dello schema XML del modulo padre.

Ad esempio, i tuoi clienti compilano un modulo di richiesta. I primi due campi del modulo sono nome e identità. Il codice XML è:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

Aggiungere un altro modulo nell&#39;applicazione che consenta ai clienti di compilare l&#39;indirizzo dell&#39;ufficio. La radice dello schema del modulo secondario è `officeAddress`. Applica `bindref` `/application/officeAddress` o `/officeAddress`. Se `bindref` non viene fornito, il modulo secondario verrà aggiunto come sottoalbero `officeAddress`. Vedere il codice XML del modulo riportato di seguito:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

Se si inserisce un altro modulo che consente ai clienti di fornire l&#39;indirizzo dell&#39;abitazione, applicare `bindref` `/application/houseAddress or /houseAddress.`Il codice XML è simile al seguente:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

Se si desidera mantenere lo stesso nome di sottodirectory della directory principale dello schema ( `Address` in questo esempio), utilizzare i bindref indicizzati.

Applicare ad esempio bindrefs `/application/address[1]` o `/address[1]` e `/application/address[2]` o `/address[2]`. Il codice XML del modulo è:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

È possibile modificare la sottostruttura predefinita del modulo/frammento adattivo utilizzando la proprietà `bindRef`. La proprietà `bindRef` consente di specificare il percorso che punta a una posizione nella struttura dello schema XML.

Se il modulo secondario non è associato, i relativi dati vengono memorizzati nella radice `data` della sezione `afUnboundData` dello schema XML del modulo principale.

È possibile aggiungere più volte un modulo adattivo come modulo secondario. Assicurati che `bindRef` sia modificato correttamente in modo che ogni istanza utilizzata del modulo adattivo punti a una sottodirectory diversa sotto la directory principale dei dati.

>[!NOTE]
>
>Se diversi moduli/frammenti sono mappati alla stessa radice secondaria, i dati vengono sovrascritti.

## Aggiunta di un modulo adattivo come modulo secondario mediante il browser di risorse {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

Per aggiungere un modulo adattivo come modulo secondario utilizzando il browser di risorse, effettua le seguenti operazioni.

1. Apri il modulo principale in modalità di modifica.
1. Nella barra laterale, fai clic su **Assets** ![assets-browser](assets/assets-browser.png). In Assets, seleziona **Modulo adattivo** dal menu a discesa.
   [![Selezione di un modulo adattivo in Assets](assets/asset.png)](assets/asset-1.png)

1. Trascina il modulo adattivo da aggiungere come modulo secondario.
   [![Trascina il modulo adattivo nel sito](assets/drag-drop.png)](assets/drag-drop-1.png)Il modulo adattivo rilasciato viene aggiunto come modulo secondario.
