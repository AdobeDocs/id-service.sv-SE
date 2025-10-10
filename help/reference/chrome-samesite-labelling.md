---
title: Google Chrome SameSite-etikettändringar
description: Dokumentation för Adobe ECID-bibliotek (ID Service).
exl-id: f20b25a4-c9bc-41b9-8e49-79b8424e62a0
source-git-commit: 7ef084bc1add5a4ea8c7be738055b0c21e247eea
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 1%

---

# Google Chrome SameSite-etikettändringar {#google-chrome-samesite-labelling-changes}

Attributet SameSite talar om för webbläsare när och hur cookies ska aktiveras i första och tredje parts scenarier. Attributet SameSite kan ha ett av tre värden: `strict`, `lax` eller `none`. Chrome, Firefox, Edge, Safari och Opera har stött `strict` och `lax` sedan november 2017, medan `none` introducerades 2018. Vissa äldre webbläsare stöder dock inte den här inställningen.

I februari 2020 släppte Google Chrome 80 och ändrade standardinställningen från `none` till `lax` när en cookie inte har något angivet värde för attributet SameSite. Den här inställningen förhindrar att en cookie används i en tredjepartskontext, som också kallas för&quot;cross-site&quot;. Alla efterföljande cookies från tredje part måste anges till `SameSite=none` och märkas som säkra.

Cookies utan ett angivet SameSite-attributvärde blir som standard `lax`.

Mer information om samma webbplatsattribut finns i [cookie-standarddokumentet](https://tools.ietf.org/html/draft-ietf-httpbis-rfc6265bis-03#section-4.1).

## Attributvärden för SameSite

| Attributvärdet SameSite | Beskrivning |
| ------ | ------------ |
| `strict` | Cookies med den här inställningen skickas endast när både den hänvisande sidan och landningssidan är en del av samma domän som cookien. |
| `lax` | Cookies med den här inställningen skickas bara när domänen som visas i webbläsarens URL matchar cookie-domänen. Det här är det nya standardvärdet för cookies i Chrome. |
| `none` | Cookies med den här inställningen är tillgängliga för extern åtkomst eller åtkomst från tredje part, till exempel&quot;cross-site&quot;. Före den här ändringen var `none` standardinställningen för SameSite för cookies, så om du använder den här inställningen fungerar en cookie på det sätt den traditionellt har fungerat. Google kräver dock att alla cookies med den här inställningen nu anger flaggan secure, vilket innebär att cookien bara skapas och skickas med begäranden via HTTPS. Alla cookies mellan webbplatser utan den säkra flaggan kommer att avvisas av Google. |

## Vad ni behöver veta som Adobe Experience Cloud-kund

**Inga JavaScript-uppdateringar krävs**

Adobe-produkter har redan släppt uppdateringar på serversidan för att ange cookies från tredje part med lämpliga attribut. Våra kunder behöver inte uppdatera JavaScript-biblioteket.

**Kontrollera att slutpunkter från tredje part använder HTTPS**

Alla kunder bör bekräfta att deras JavaScript-konfiguration använder HTTPS för sina samtal till Adobe-tjänster. Target, Audience Manager och Experience Cloud Identity Service (ECID) dirigerar om HTTP-anrop från tredje part till sina respektive HTTPS-slutpunkter, vilket kan öka fördröjningen. Det innebär att du inte behöver ändra konfigurationen. Analyskunder bör uppdatera sina implementeringar så att enbart HTTPS används, eftersom omdirigeringar som är specifika för Analytics kan orsaka dataförlust.

**Korrekt märkta cookies bör samla in data som avsett**

Så länge cookies är korrekt märkta kommer webbläsarna inte att vidta några åtgärder för att blockera dem. Konsumenterna kan välja att blockera vissa typer av cookies, men för närvarande verkar detta bara vara en anmälningsinställning.

**Befintliga cookies från tredje part utan de uppdaterade etiketterna ignoreras**

Cookies från tredje part som skapades innan Chrome 80 började använda inställningarna för SameSite=`none` och säkra flaggor ignoreras av Chrome 80 om dessa flaggor inte finns.

Många av Adobe cookies från tredje part har inte dessa flaggor och måste uppdateras av Edge-servrar innan användare uppgraderar till Chrome 80, annars går cookies förlorade. Edge-servrarna uppdateras automatiskt när användare besöker en webbplats där cookien används.

De flesta Adobe-produkter har redan rätt flaggor för cookies. Undantaget är analysimplementationer som använder datainsamling från tredje part och inte använder ECID. Kunderna kan uppleva en liten tillfällig ökning av antalet nya besökare som annars skulle ha varit återkommande besökare.

**Möjlig minskning av cookie-matchning för mål- och marknadspartners (endast Audience Manager)**

Adobe har kontroll över uppdateringen av cookies, men Adobe kan inte tvinga partners att göra nödvändiga ändringar. Cookie-matchning kan minska för Audience Manager-kunder som använder målpartners eller marknadspartners som inte har gjort dessa uppdateringar.

**Analysvänlig cookies från tredje part (endast analyser `s_vi` cookies)**

Vissa analysimplementeringar använder ett CNAME-alias för Analytics för att göra det möjligt att skapa cookien `s_vi` i domänen för CNAME. Om CNAME finns i samma domän som din webbplats, kommer detta att anges som en cookie från första part. Om du däremot äger flera domäner och använder samma CNAME för datainsamling i alla dina domäner, kommer det att anges som en cookie från tredje part i dessa andra domäner.

När `lax` har blivit den nya standardinställningen för SameSite i Chrome visas inte längre CNAME i andra domäner.

För att kunna hantera ändringen anger Analytics nu explicit värdet `s_vi`-cookie till `lax` för SameSite. Om du vill använda denna cookie i en användarvänlig tredjepartskontext anger du värdet för SameSite till `none`, vilket även innebär att du alltid måste använda HTTPS. Kontakta kundtjänst om du vill ändra värdet för SameSite för dina säkra CNAME.

>[!IMPORTANT]
>
>Den här åtgärden krävs inte för Analytics-kunder som använder ECID, kunder som använder en separat CNAME för var och en av sina domäner eller kunder som bara använder datainsamling från tredje part.

## Adobe Standard Visitor Cookies

Endast vanliga cookies för besökarstandard listas i tabellen nedan. Om du vill ha fler cookie-konfigurationer läser du produktspecifik dokumentation eller kontaktar Adobe.

### ECID

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| AMCV_###@AdobeOrg | Förste part på klientsidan | Inget mervärde tillagt *Chrome har som standard `lax` inställning | Konfigurerbar |
| AMCVS_###@AdobeOrg | Förste part på klientsidan | Inget mervärde tillagt *Chrome har som standard `lax` inställning | Konfigurerbar |
| s_ecid | Förste part på serversidan | SameSite==`lax` | Ej angiven |

### Audience Manager

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| Demdex | Tredje part | `none` | Ange som säker |
| Dextp | Tredje part | `none` | Ange som säker |

### Analytics 

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| s_vi | <ul><li> Första part på serversidan om `CNAME` används </li> <li>Tredje part om du använder 2o7.net eller omtrdc.net</li></ul> | <ul><li>`lax` om förstapartsleverantör</li> <li>`none` om tredje part</li></ul> *Kunder kan redigera inställningar via kundtjänst för förstahandsdomäner* | Ange om `none`- och HTTPS-begäran används |
| s_fd | Förste part på klientsidan | Inget värde har lagts till *Chrome har som standard inställningen `lax` | Ej angiven |

### Target

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| mbox | Förste part | Inget mervärde tillagt *Chrome har som standard `lax` inställning | Ej angiven |

### Ad Cloud

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| Högsta_g_v2 | Tredje part | `none` *Endast i Google Chrome- och Chromium-baserade webbläsare* | Ange om `none`- och HTTPS-begäran används |
| data_adcloud | Förste part | Inget mervärde tillagt *Chrome har som standard `lax` inställning | Ej angiven |
| ev_tm | Tredje part | `none` *Endast i Google Chrome- och Chromium-baserade webbläsare* | Ange om `none`- och HTTPS-begäran används |

### Bizible

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| buid | Tredje part | `none` | Säker |

### Marketo Munchkin

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| _mkto_trk | Förste part på klientsidan | Inget mervärde tillagt *Chrome har som standard `lax` inställning | Kan konfigureras för externa sidor |

>
>
>Adobe cookies från tredje part är inställda på serversidan.

Mer information finns i dokumentet om [Target&#39;s Google Chrome SameSite policies](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/google-chrome-samesite-cookie-policies.html?lang=sv-SE).
