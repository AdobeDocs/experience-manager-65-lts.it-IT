---
title: Configura il progetto Android&trade; studio e crea l’app Android&trade;
description: Passaggi per configurare il progetto Android&trade; Studio e creare il programma di installazione per l’app Forms Adobe Experience Manager (AEM)
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 425c6194-0b87-4b01-a013-f620755072b3
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 2%

---

# Configurate il progetto Android™ studio e create l&#39;app Android™ {#set-up-the-android-studio-project-and-build-the-android-app}

Questo articolo è destinato alla creazione dell&#39;app AEM Forms 6.3.1.1 e versioni successive. Per creare un&#39;app dal codice sorgente dell&#39;app AEM Forms 6.3, vedi [Configurare il progetto Eclipse e creare l&#39;app Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms fornisce il codice sorgente completo dell’app AEM Forms. L’origine contiene tutti i componenti per creare un’app AEM Forms personalizzata. L&#39;archivio del codice sorgente `adobe-lc-mobileworkspace-src-<version>.zip` fa parte del pacchetto `adobe-aemfd-forms-app-src-pkg-<version>.zip` in Distribuzione software.

Per ottenere l’origine dell’app AEM Forms, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](/help/sites-administering/package-manager.md) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

Nell&#39;immagine seguente viene visualizzato il contenuto estratto di `adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenuto estratto dall&#39;origine Android™ compresso](assets/mws-content-1.png)

Nell&#39;immagine seguente viene visualizzata la struttura di directory della cartella `android` nella cartella `src`.

![Struttura di directory della cartella Android in src](assets/android-folder.png)

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

1. Per configurare un progetto in Android™ Studio e fornire un’identità di firma, effettua le seguenti operazioni:

   Accedere a un computer in cui è installato e configurato Android™ Studio.

1. Copia l&#39;archivio `adobe-lc-mobileworkspace-src-<version>.zip` scaricato in:

   **Per utenti Mac**: `[User_Home]/Projects`

   **Per utenti Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Per Windows®, si consiglia di mantenere il progetto Android™ nell&#39;unità di sistema.

1. Estrai l’archivio nella seguente directory:

   **Per utenti Mac**: `[User_Home]/Projects/[your-project]`

   **Per utenti Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Si consiglia di mantenere il progetto Android estratto nell&#39;unità di sistema prima di importarlo in Android™ Studio.

1. Avvia Android™ Studio.

   **Per gli utenti di Mac**: aggiorna il file `local.properties` presente nella cartella `[User_Home]/Projects/[your-project]/android` e punta la variabile `sdk.dir` alla posizione `SDK` sul desktop.

   **Per gli utenti Windows®**: aggiorna il file `local.properties` presente nella cartella `%HOMEPATH%\Projects\[your-project]\android` e punta la variabile `sdk.dir` alla posizione `SDK` sul desktop.

1. Fai clic su **[!UICONTROL Fine]** per generare il progetto.

   Il progetto è disponibile in Gestione progetti ADT.

   ![progetto eclipse dopo la generazione dell&#39;app](assets/eclipsebuildmws.png)

1. In Android™ Studio, selezionare **[!UICONTROL Importa progetto (Eclipse ADT, Gradle, ecc.)]**.
1. In Esplora progetti selezionare la directory principale del progetto che si desidera compilare nella casella di testo **Directory principale**:

   **Per utenti Mac:** [Home_Utente]/Projects/MobileWorkspace/src/android

   **Per gli utenti Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Dopo l’importazione del progetto, viene visualizzato un pop-up con l’opzione di aggiornamento di Android™ plugin Gradle. Fai clic sul pulsante appropriato a seconda delle tue esigenze.

   ![dontremindmeagainwithisproject](assets/dontremindmeagainforthisproject.png)

1. Dopo aver generato la gradle, viene visualizzata la seguente schermata. Connettere il dispositivo o l&#39;emulatore appropriato al sistema e fare clic su **[!UICONTROL Esegui Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio visualizza i dispositivi collegati e gli emulatori disponibili. Selezionare il dispositivo su cui si desidera eseguire l&#39;applicazione e quindi fare clic su **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Dopo aver creato il progetto, puoi scegliere di installare l’app utilizzando Android™ Debug Bridge o Android™ Studio.

### Utilizzo di Android™ Debug Bridge {#andriod-debug-bridge}

Puoi installare l&#39;applicazione su un dispositivo Android™ tramite [Android™ Debug Bridge](https://developer.android.com/tools/adb) con il seguente comando:

**Per utenti Mac**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Per utenti Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
