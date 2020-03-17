---
description: Experience Cloud ID Service (ECID) stöder SHA-256-algoritmen som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n. Detta är en valfri JavaScript-metod för att skicka hash-kodade identifierare till Experience Cloud. Du kan fortsätta att använda dina egna metoder för hashning innan du skickar kund-ID:n.
keywords: ID Service
seo-description: Experience Cloud ID Service (ECID) stöder SHA-256-algoritmen som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n. Detta är en valfri JavaScript-metod för att skicka hash-kodade identifierare till Experience Cloud. Du kan fortsätta att använda dina egna metoder för hashning innan du skickar kund-ID:n.
seo-title: SHA256 Hash-stöd för setCustomerIDs
title: SHA256 Hash-stöd för setCustomerIDs
translation-type: tm+mt
source-git-commit: ac1131be75fd04b51cd1d646086e1802a43afb18

---


# SHA256 Hash-stöd för `setCustomerIDs`{#hashing-support}

Experience Cloud ID Service (ECID) stöder SHA-256-algoritmen som gör att du kan skicka in kund-ID:n eller e-postadresser och skicka ut hash-kodade ID:n. Detta är en valfri JavaScript-metod för att skicka hash-kodade identifierare till Experience Cloud. Du kan fortsätta att använda dina egna metoder för hashning innan du skickar kund-ID:n.
Det finns två sätt att implementera hash-stöd med setCustomerID, vilket beskrivs i avsnitten nedan:

* [Använd metoden setCustomerIDs i ECID](/help/reference/hashing-support.md#use-setcustomerids-method)
* [Lägg till en åtgärd i Adobe Experience Platform Launch](/help/reference/hashing-support.md#add-action-launch)

## Använda `setCustomerIDs` metoden i ECID {#use-setcustomerids-method}

Den första metoden använder metoden [`setCustomerIDs`](/help/library/get-set/setcustomerids.md) (`customerIDs<object>`, `hashType<string>`).

ECID-biblioteket utför datavypnormalisering på kund-ID:n innan hash inträffar. Den här processen trimmar de tomma områdena för användar-ID:n i båda ändar och konverterar alla tecken till gemener. Exempel: &quot; ecid@adobe.com &quot; blir &quot;ecid@adobe.com&quot;

Nedan visas ett kodexempel på hur du anger ett enda kund-ID (den e-postadress som nämns ovan) med SHA-256-hash.

```
// Set single customerID with SHA-256 hashing
visitor.setCustomerIDs({email: {id: "ecid@adobe.com", authState: 1}}, "SHA-256");
```

<br> 

Tillsammans med besökar-ID:t för Experience Cloud kan du koppla ytterligare kund-ID:n, autentiseringsstatus och hash-typ (SHA-256) till varje besökare. Om du inte anger någon hash-typ betraktas den som ingen hash.

Metoden accepterar flera kund-ID:n för samma besökare `setCustomerIDs` . Detta hjälper er att identifiera eller rikta in er på en enskild användare på olika enheter. Du kan till exempel överföra dessa ID:n som [kundattribut](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/attributes.html) till Experience Cloud och få tillgång till dessa data via olika lösningar.

Kund-ID, autentiserade tillstånd och hash-typ *lagras inte* i en cookie som kan användas senare. I stället ska Kund-ID, autentiserade tillstånd och hash-typ lagras i en instansvariabel som ska hämtas med [`getCustomerIDs`](/help/library/get-set/getcustomerids.md)enligt nedan:

```
> visitor.getCustomerIDs();
< {email: {…}}
    email: {id: "a6ea4cde5da5ae7cc68baae894d1d6544fca26254433b0fff7c2cb4843b4a097", authState: 1, hashType: "SHA-256"}
    __proto__: Object
```

<br> 

Om du använder `setCustomerIDs` metoden anropas till Experience Cloud ID-tjänsten, `dpm.demdex.net`med tillägg av `d_cid_ic` frågeparametern, som innehåller det hashas-ID:t. Ett exempelanrop kan se ut som det nedan. Radbrytningar lades till för tydlighet.

```
http://dpm.demdex.net/id?d_visid_ver=4.4.0&d_fieldgroup=AAM&d_rtbd=json&d_ver=2&
d_orgid=12A3F3F459CE0AD80A495CBE%40AdobeOrg&d_nsid=0&d_mid=12349850857640731290890207735189050123&
d_blob=6G1ynYcLPuiQxYZrsz_pkqfLG9yMXBpb2zX5dvJdYQJzPXImdj0y&
d_cid_ic=email%a6ea4cde5da5ae7cc68baae894d1d6544fca26254433b0fff7c2cb4843b4a097%011&
ts=1563299964843
```

<br> 

I tabellen nedan finns en beskrivning av `d_cid_ic` parametern och autentiseringstillståndet.

| Parameter | Beskrivning |
|------------|----------|
| `d_cid_ic` | Skickar integreringskoden, det unika användar-ID:t (DPUID) och ett autentiserat tillstånds-ID till ID-tjänsten. Separera integreringskoden och DPUID med kontrolltecknet som inte skrivs ut, %01</code>: <br> Exempel: d_cid_ic=Integration_code%01DPUID%01Authentication_state</code> <br> <b>Autentiseringstillstånd</b> <br> Detta är ett valfritt ID i parametern d_cid_ic. Uttryckt som ett heltal identifierar det användare utifrån deras autentiseringsstatus enligt nedan: <br> <ul><li>0 (Okänd eller aldrig autentiserad)</li><li>1 (autentiserad för den här instansen/sidan/appkontexten)</li><li>2 (utloggad)</li></ul> <br> Exempel: <br> <ul><li>Okänd: ...d_cid=123%01456%01<b>0</b></li><li>Autentiserad: ...d_cid=123%01456%01<b>1</b></li><li>Utloggad: ...d_cid=123%01456%01<b>2</b></li></ul> |

## Lägg till en åtgärd i Adobe Experience Platform Launch {#add-action-launch}

Experience Platform Launch är nästa generation av tagghanteringsfunktioner från Adobe. Läs mer om Launch i [Launch-produktdokumentationen](https://docs.adobe.com/content/help/en/launch/using/overview.html).

Om du vill lägga till en åtgärd i Launch läser du [regeldokumentationen](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html) i Adobe Launch och läser skärmbilden nedan:

![](/help/reference/assets/hashing-support.png)

<br> 

När du har bekräftat din konfiguration kapslar Launch in data i ett objekt, som nedan:

```
{
    integration_code: {
        id: "value",
        authState: auth_state,
        hashType: "hash_algorithm"
    }
}
```

Här följer ett kodexempel:

```
// Set single customer ID with hash type
setCustomerIDs(Ingeration code: {
    id: "string_value",
    authState: auth_state,
    hashType: "hash_algorithm"
});
```

På samma sätt som den `setCustomerIDs` metod som beskrivs i det första avsnittet, resulterar detta i ett anrop till Experience Cloud ID-tjänsten, med tillägg av `d_cid_ic` frågeparametern.