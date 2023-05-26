---
title: Google Chrome SameSite-etikettändringar
description: Dokumentation för Adobe ECID-bibliotek (ID Service).
exl-id: f20b25a4-c9bc-41b9-8e49-79b8424e62a0
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 1%

---

# Google Chrome SameSite-etikettändringar {#google-chrome-samesite-labelling-changes}

Attributet SameSite talar om för webbläsare när och hur cookies ska aktiveras i första och tredje parts scenarier. Attributet SameSite kan ha ett av tre värden: `strict`, `lax`, eller `none`. Chrome, Firefox, Edge, Safari och Opera har stöd `strict` och `lax` sedan november 2017, medan `none` infördes 2018. Vissa äldre webbläsare stöder dock inte den här inställningen.

I februari 2020 släppte Google Chrome 80 och ändrade standardinställningen från `none` till `lax` när en cookie inte har ett angivet SameSite-attributvärde. Den här inställningen förhindrar att en cookie används i en tredjepartskontext, som också kallas för&quot;cross-site&quot;. Alla efterföljande cookies från tredje part måste anges till `SameSite=none` och märkas som säker.

Cookies utan ett angivet SameSite-attributvärde får standardvärdet `lax`.

Besök [standarddokument för cookie](https://tools.ietf.org/html/draft-ietf-httpbis-rfc6265bis-03#section-4.1) om du vill ha mer information om samma webbplatsattribut.

## Attributvärden för SameSite

| Attributvärdet SameSite | Beskrivningar |
| ------ | ------------ |
| `strict` | Cookies med den här inställningen skickas endast när både den hänvisande sidan och landningssidan är en del av samma domän som cookien. |
| `lax` | Cookies med den här inställningen skickas bara när domänen som visas i webbläsarens URL matchar cookie-domänen. Det här är det nya standardvärdet för cookies i Chrome. |
| `none` | Cookies med den här inställningen är tillgängliga för extern åtkomst eller åtkomst från tredje part, till exempel&quot;cross-site&quot;. Före denna ändring `none` var standardinställningen för SameSite för cookies, så om du använder den här inställningen fungerar en cookie på det sätt den traditionellt har fungerat. Google kräver dock att alla cookies med den här inställningen nu anger flaggan secure, vilket innebär att cookien bara skapas och skickas med begäranden via HTTPS. Alla cookies mellan webbplatser utan den säkra flaggan kommer att avvisas av Google. |

## Vad ni behöver veta som Adobe Experience Cloud-kund

**Inga JavaScript-uppdateringar krävs**

Adobe-produkter har redan släppt uppdateringar på serversidan för att ange cookies från tredje part med lämpliga attribut. Inga JavaScript-biblioteksuppdateringar behövs av våra kunder.

**Kontrollera att slutpunkter från tredje part använder HTTPS**

Alla kunder bör bekräfta att deras JavaScript-konfiguration använder HTTPS för sina anrop till Adobe-tjänster. Target, Audience Manager och Experience Cloud Identity Service (ECID) dirigerar om HTTP-anrop från tredje part till sina respektive HTTPS-slutpunkter, vilket kan öka fördröjningen. Det innebär att du inte behöver ändra konfigurationen. Analyskunder bör uppdatera sina implementeringar så att enbart HTTPS används, eftersom omdirigeringar som är specifika för Analytics kan orsaka dataförlust.

**Korrekt märkta cookies bör användas för att samla in de data som avses**

Så länge cookies är korrekt märkta kommer webbläsarna inte att vidta några åtgärder för att blockera dem. Konsumenterna kan välja att blockera vissa typer av cookies, men för närvarande verkar detta bara vara en anmälningsinställning.

**Befintliga cookies från tredje part utan de uppdaterade etiketterna kommer att ignoreras**

Cookies från tredje part som skapades innan Chrome 80 började använda SameSite=`none` och inställningarna för säkra flaggor ignoreras av Chrome 80 om dessa flaggor inte finns.

Många av de befintliga cookies från tredje part från Adobe har inte dessa flaggor och måste uppdateras av Edge-servrar innan användare uppgraderar till Chrome 80, annars går dessa cookies förlorade. Edge-servrarna uppdateras automatiskt när användare besöker en webbplats där cookien används.

De flesta Adobe-produkter har redan rätt flaggor för cookies. Undantaget är analysimplementationer som använder datainsamling från tredje part och inte använder ECID. Kunderna kan uppleva en liten tillfällig ökning av antalet nya besökare som annars skulle ha varit återkommande besökare.

**Möjlig minskning av cookie-matchning för mål- och marknadspartners (endast Audience Manager)**

Adobe har kontroll över uppdateringen av cookies, men Adobe kan inte tvinga sina partner att göra nödvändiga ändringar. Cookie-matchning kan minska för Audience Manager-kunder som använder målpartners eller marknadspartners som inte har gjort dessa uppdateringar.

**Analytics Friendly third-party Cookies (Analytics `s_vi` endast cookies)**

Vissa analysimplementeringar använder ett CNAME-alias för Analytics för att göra det möjligt att skapa `s_vi` cookie i domänen för CNAME. Om CNAME finns i samma domän som din webbplats, kommer detta att anges som en cookie för första part. Om du däremot äger flera domäner och använder samma CNAME för datainsamling i alla dina domäner, kommer det att anges som en cookie från tredje part i dessa andra domäner.

Med `lax` CNAME blir nu standard för samma plats i Chrome och är inte längre synlig i andra domäner.

För att anpassa ändringen anges värdet för SameSite explicit i Analytics `s_vi` cookie till `lax`. Om du vill använda denna cookie i en användarvänlig tredjepartskontext anger du värdet för SameSite till `none`, vilket även innebär att du alltid måste använda HTTPS. Kontakta kundtjänst om du vill ändra värdet för SameSite för dina säkra CNAME.

>[!IMPORTANT]
>
>Den här åtgärden krävs inte för Analytics-kunder som använder ECID, kunder som använder en separat CNAME för var och en av sina domäner eller kunder som bara använder datainsamling från tredje part.

## Cookies för Adobe standardbesökare

Endast vanliga cookies för besökarstandard listas i tabellen nedan. Om du vill ha fler cookie-konfigurationer läser du produktspecifik dokumentation eller kontaktar din Adobe-representant.

### ECID

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| AMCV_###@AdobeOrg | Förste part på klientsidan | Inget mervärde tillagt *Chrome har standardvärdet `lax` inställning | Konfigurerbar |
| AMCVS_###@AdobeOrg | Förste part på klientsidan | Inget mervärde tillagt *Chrome har standardvärdet `lax` inställning | Konfigurerbar |
| s_ecid | Förste part på serversidan | SameSite==`lax` | Ej angiven |

### Audience Manager

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| Demdex | Tredje part | `none` | Ange som säker |
| Dextp | Tredje part | `none` | Ange som säker |

### Analytics 

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| s_vi | <ul><li> Första part på serversidan om använder `CNAME` </li> <li>Tredje part om 2o7.net eller omtrdc.net används</li></ul> | <ul><li>`lax` om första part</li> <li>`none` om tredje part</li></ul> *Kunder kan redigera inställningar via kundtjänst för förstahandsdomäner* | Ange, om du använder `none` och HTTPS-begäran |
| s_fd | Förste part på klientsidan | Inget värde tillagt *Chrome har standardvärdet `lax` inställning | Ej angiven |

### Target

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| mbox | Första part | Inget mervärde tillagt *Chrome har standardvärdet `lax` inställning | Ej angiven |

### Ad Cloud

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| Högsta_g_v2 | Tredje part | `none` *Endast i Google Chrome- och Chromium-baserade webbläsare* | Ange, om du använder `none` och HTTPS-begäran |
| data_adcloud | Första part | Inget mervärde tillagt *Chrome har standardvärdet `lax` inställning | Ej angiven |
| ev_tm | Tredje part | `none` *Endast i Google Chrome- och Chromium-baserade webbläsare* | Ange, om du använder `none` och HTTPS-begäran |

### Bizible

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| buid | Tredje part | `none` | Säker |

### Marketo Munchkin

| Cookie | Typ | Attributet SameSite | Säkert attribut |
| ------ | ---- | ------------------ | ---------------- |
| _mkto_trk | Förste part på klientsidan | Inget mervärde tillagt *Chrome har standardvärdet `lax` inställning | Kan konfigureras för externa sidor |

> !![IMPORTANT] Cookies från tredje part från Adobe är inställda på serversidan

Mer information finns i dokumentet om [Målets Google Chrome SameSite-principer](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/google-chrome-samesite-cookie-policies.html).
