---
title: Modificare l’ordine di valutazione per l’autenticazione
description: Puoi modificare l’ordine in cui AEM Forms valuta più provider di autenticazione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5f9f96ab-4c0a-4a75-856b-d4eceddefbf9
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 100%

---

# Modificare l’ordine di valutazione per l’autenticazione {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Se hai configurato più provider di autenticazione, puoi modificare l’ordine in cui vengono valutati da AEM Forms per l’autenticazione. L’ordine dei provider di autenticazione elencati nel file config.xml determina l’ordine di valutazione per l’autenticazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l’impostazione di configurazione corrente in un file, fai clic su Esporta e salva il file di configurazione in un’altra posizione.
1. Trova il seguente nodo nel file:

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   In `<entry key="order" value="3" />`, modifica il valore di ogni nodo per impostare l’ordine di valutazione per l’autenticazione.

1. Per importare il file aggiornato, in Gestione utenti fai clic su Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Sfoglia per trovare il file, fai clic su Importa e quindi su OK.
