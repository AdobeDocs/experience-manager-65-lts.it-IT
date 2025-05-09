---
title: 'Operazioni Granite: amministrazione di utenti e gruppi'
description: Scopri l’amministrazione di utenti e gruppi Granite.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: ba02f9d4-5286-41d6-995c-307d6e13431b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---

# Operazioni Granite: amministrazione di utenti e gruppi{#granite-operations-user-and-group-administration}

Poiché Granite incorpora l’implementazione dell’archivio CRX della specifica API JCR, ha una propria amministrazione di utenti e gruppi.

Questi account sono la base sottostante degli [account AEM](/help/sites-administering/security.md) ed eventuali modifiche apportate all&#39;account con l&#39;amministrazione Granite verranno applicate se/quando si accede agli account dalla [console Utenti AEM](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (ad esempio, `http://localhost:4502/useradmin`). Dalla console Utenti di AEM puoi anche gestire i privilegi e altre specifiche di AEM.

Le console di amministrazione di utenti e gruppi Granite sono entrambe disponibili nella console **[Strumenti](/help/sites-administering/tools-consoles.md)** dell&#39;interfaccia utente ottimizzata per il tocco:

![Console Strumenti](assets/chlimage_1-72a.png)

Scegliendo **Utenti** o **Gruppi** dalla console Strumenti, viene aperta la console appropriata. In entrambi è possibile eseguire azioni utilizzando la casella di selezione e quindi le azioni dalla barra degli strumenti oppure aprendo i dettagli dell&#39;account tramite il collegamento in **Nome**.

* [Amministrazione utente](#user-administration)

  ![chlimage_1-73](assets/chlimage_1-73a.png)

  La console **Utenti** elenca:

   * il nome utente
   * il nome di accesso dell’utente (nome account)
   * qualsiasi titolo assegnato all’account

* [Amministrazione gruppo](#group-administration)

  ![Console di gestione utenti](assets/chlimage_1-74a.png)

  La console **Gruppi** elenca:

   * il nome del gruppo
   * la descrizione del gruppo
   * il numero di utenti/gruppi nel gruppo

## Amministrazione utente {#user-administration}

### Aggiunta di un nuovo utente {#adding-a-new-user}

1. Utilizza l&#39;icona **Aggiungi utente**:

   ![Icona Aggiungi utente](do-not-localize/chlimage_1-1.png)

1. Verrà aperto il modulo **Crea utente**:

   ![Modulo dettagli utente](assets/chlimage_1-75a.png)

   Qui puoi immettere i dettagli utente per l’account (la maggior parte sono standard e auto-esplicativi):

   * **ID**

     Identificazione univoca dell&#39;account utente. È obbligatorio e non può contenere spazi.

   * **Indirizzo e-mail**
   * **Password**

     La password è obbligatoria.

   * **Password Retype**

     Questo è obbligatorio in quanto è necessario per la conferma della password.

   * **Nome**
   * **Cognome**
   * **Numero di telefono**
   * **Qualifica**
   * **Via**
   * **Mobile**
   * **Città**
   * **Codice Postale**
   * **Paese**
   * **Stato**
   * **Titolo**
   * **Genere**
   * **Informazioni su**
   * **Impostazioni account**

      * **Stato**
È possibile contrassegnare l&#39;account come **attivo** o **inattivo**.

   * **Foto**

     Qui puoi caricare una foto da usare come avatar.

     Tipi di file accettati: `.jpg .png .tif .gif`

     Dimensione preferita: `240x240px`

   * **Aggiungi utente a gruppi**

     Utilizza il menu a discesa di selezione per selezionare i gruppi di cui l’utente deve essere membro. Una volta selezionata, utilizza **X** con il nome da deselezionare prima di salvare.

   * **Gruppi**

     Elenco di gruppi di cui l&#39;utente è attualmente membro. Utilizza **X** con il nome per deselezionare prima di salvare.

1. Dopo aver definito l’account utente, utilizza:

   * **Annulla** per interrompere la registrazione.
   * **Salva** per completare la registrazione. La creazione dell’account utente verrà confermata con un messaggio.

### Modifica di un utente esistente {#editing-an-existing-user}

1. Accedi ai dettagli utente dal collegamento posto sotto il nome utente nella console Utenti.

1. È ora possibile modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

1. Accedi ai dettagli utente dal collegamento posto sotto il nome utente nella console Utenti.

1. È ora possibile modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user).

### Modifica della password per un utente esistente {#changing-the-password-for-an-existing-user}

1. Accedi ai dettagli utente dal collegamento posto sotto il nome utente nella console Utenti.

1. È ora possibile modificare i dettagli come in [Aggiunta di un nuovo utente](#adding-a-new-user). In **Impostazioni account** è presente un collegamento per **Modifica password**.

   ![Finestra di dialogo Impostazioni account](assets/chlimage_1-76a.png)

1. Viene visualizzata la finestra di dialogo **Modifica password**. Immettere e ridigitare la nuova password, insieme alla password. Utilizza **OK** per confermare le modifiche.

   ![Finestra di dialogo Modifica password](assets/chlimage_1-77a.png)

   Un messaggio conferma che la password è stata cambiata.

### Assegnazione gruppo rapido {#quick-group-assignment}

1. Utilizza la casella di selezione per contrassegnare uno o più utenti.
1. Utilizza l&#39;icona **Gruppi**:

   ![Utilizzo dell&#39;icona Gruppi](do-not-localize/chlimage_1-2.png)

   Per aprire il menu a discesa di selezione del gruppo:

   ![Selettore gruppi](assets/chlimage_1-78a.png)

1. Nella casella di selezione è possibile selezionare o deselezionare i gruppi a cui deve appartenere l&#39;account utente.

1. Quando hai assegnato, o non hai assegnato, i gruppi come richiesto, utilizza:

   * **Annulla** per annullare le modifiche
   * **Salva** per confermare le modifiche

### Eliminazione dei dettagli utente esistenti {#deleting-existing-user-details}

1. Utilizza la casella di selezione per contrassegnare uno o più utenti.
1. Utilizza l&#39;icona **Elimina** per eliminare i dettagli utente:

   ![Elimina dettagli utente esistenti](do-not-localize/chlimage_1-3.png)

1. Ti verrà chiesto di confermare l’eliminazione, quindi un messaggio confermerà che l’effettiva eliminazione ha avuto luogo.

## Amministrazione gruppo {#group-administration}

### Aggiunta di un nuovo gruppo {#adding-a-new-group}

1. Utilizza l’icona Aggiungi gruppo:

   ![Aggiungi un nuovo gruppo](do-not-localize/chlimage_1-4.png)

1. Viene aperto il modulo **Crea gruppo**:

   ![Modulo dettagli gruppo](assets/chlimage_1-79a.png)

   Qui puoi immettere i dettagli del gruppo:

   * **ID**

     Identificatore univoco del gruppo. Questo è obbligatorio e non può contenere spazi.

   * **Nome**

     Un nome per il gruppo; viene visualizzato nella console Gruppi.

   * **Descrizione**

     Descrizione del gruppo.

   * **Aggiungi membri al gruppo**

     Utilizza il menu a discesa di selezione per selezionare gli utenti da aggiungere al gruppo. Una volta selezionata, utilizza **X** con il nome da deselezionare prima di salvare.

   * **Membri gruppo**

     Elenco di utenti del gruppo. Utilizza **X** con il nome per deselezionare prima di salvare.

1. Dopo aver definito il gruppo, utilizzare:

   * **Annulla** per interrompere la registrazione.
   * **Salva** per completare la registrazione. La creazione del gruppo verrà confermata con un messaggio.

### Modifica di un gruppo esistente {#editing-an-existing-group}

1. Accedi ai dettagli del gruppo dal collegamento posto sotto il nome del gruppo nella console Gruppi.

1. È ora possibile modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Copia di un gruppo esistente {#copying-an-existing-group}

1. Utilizza la casella di selezione per contrassegnare un gruppo.
1. Utilizza l&#39;icona **Copia** per copiare i dettagli del gruppo:

   ![Copia un gruppo esistente](do-not-localize/chlimage_1-5.png)

1. Il modulo **Modifica impostazioni gruppo** verrà aperto.

   L&#39;ID gruppo sarà lo stesso dell&#39;originale, ma con il prefisso `Copy of`. Modifica questo ID perché non può contenere spazi. Tutti gli altri dettagli sono gli stessi dell&#39;originale.

   È ora possibile modificare e salvare i dettagli come in [Aggiunta di un nuovo gruppo](#adding-a-new-group).

### Eliminazione di un gruppo esistente {#deleting-an-existing-group}

1. Utilizza la casella di selezione per contrassegnare uno o più gruppi.
1. Utilizza l&#39;icona **Elimina** per eliminare i dettagli del gruppo:

   ![Eliminazione di un gruppo esistente](do-not-localize/chlimage_1-6.png)

1. Ti verrà chiesto di confermare l’eliminazione, quindi un messaggio confermerà che l’effettiva eliminazione ha avuto luogo.
