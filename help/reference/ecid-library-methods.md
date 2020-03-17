---
title: ECID-biblioteksmetoder i en Safari ITP-värld
seo-title: ECID-biblioteksmetoder i en Safari ITP-värld
description: Dokumentation för Adobe ECID-bibliotek (ID Service).
seo-description: Dokumentation för Adobe ECID-bibliotek (ID Service).
translation-type: tm+mt
source-git-commit: 8f4175b942ed4228ccd1f96791aa668be8aff95d

---


# ECID-biblioteksmetoder i en Safari ITP-värld

Eftersom Safari effektiviserar spårningen över domäner via ITP måste Adobe upprätthålla bästa praxis för bibliotek som stöder kunder samt konsumentintegritet och valmöjligheter.

Den 21 februari 2019 meddelade Apple sin senaste uppdatering av ITP (Intelligent Tracking Prevention). Till skillnad från tidigare versioner som fokuserar på cookies från tredje part innehåller den här versionen information om nya spårningsåtgärder för cookies från första part. Alla beständiga cookies från första part som anges via API:t document.cookie, som ofta kallas &quot;cookies på klientsidan&quot;, har en tidsgräns på 7 dagar. Cookies från tredje part kommer även fortsättningsvis att blockeras, vilket tidigare versioner av ITP har. Mer information om ITP 2.1 och hur Adobes lösningar påverkar finns i [Safari ITP 2.1 Impact on Adobe Experience Cloud and Experience Platform Customers](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).

## Vanliga frågor om Adobe ECID för Safari ITP

**Varför påverkas AMCV-cookien, som anges av Experience Cloud ID-biblioteket (ECID) i en kunds första partsdomän, av ITP 2.1?**

AMCV-cookien är för närvarande beroende av API:t document.cookie och ställs in via&quot;klient-side&quot;. Safari prioriterar cookies som anges från en kunds server.

**Varför är en cookie som ställs in via en CNAME-spårningsserver ett bättre alternativ för spårning i Safari?**

ITP:s regler fokuserar på att ge utvecklarna kontroll. Implementeringar via CNAME-certifikat kan inte göras enbart via JavaScript. Adobes CNAME-certifieringsprogram (spårning på serversidan) är i linje med ITP och har varit en del av Adobes strategi i många år. ECID-biblioteket frigör metoder som fokuserar på att flytta ECID-biblioteksfunktioner till en CNAME-implementering.

**Varför fokuserar Adobe på ECID-biblioteket när andra metoder för att spåra besökare i Analytics används med CNAME idag?**

ECID-biblioteket, AMCV cookie och ECID (även MID) började som en metod för att integrera alla Adobe-lösningar med ett ID. Detta ID fortsätter att vara det prioriterade cookie-nivå-ID:t i Adobes produktutvecklingskarta och är standardcookie-ID:t för Adobe Experience Platform.

**Hjälper CNAME kunder att aktivera spårning av flera domäner?**

Samma regler och kavattar som tidigare har funnits med CNAME finns fortfarande. I vissa fall kan CNAME hjälpa till i ett flerdomänscenario. Om du har en huvudstartwebbplats där användare kan identifieras innan de besöker andra domäner kan en CNAME aktivera multi-domain tracking i webbläsare som inte accepterar cookies från tredje part. CNAME kan dock i vissa scenarier hjälpa till med multidomäner, men orsaken till att ECID flyttas till CNAME-implementeringar är för beständig besöksidentifiering, inte för multikörning. Mer information om CNAME och flera domäner finns i [Datainsamlings-CNAME och Spårning](/help/reference/analytics-reference/cname.md)mellan domäner.

Fler vanliga frågor och svar kommer att läggas till här när ytterligare ITP-ändringar släpps. Mer information finns på [Adobe Experience League](https://experienceleague.adobe.com/#recommended/solutions/analytics).

## ITP-relaterade ändringar, metoder och konfigurationer

När ytterligare metoder skapas för spårning i Safari läggs de till som referens till den här sidan.

>[!NOTE] *ECID* = *MID* = *MCID* i all dokumentation nedan.

Nedan finns information om insatser för användning av ITP- och ECID-bibliotek.

## Använd ECID-bibliotek och CNAME-spårning för att förlänga giltigheten för besökar-ID

ITP 2.1 förhindrar möjligheten att skriva cookies på klientsidan, vilket försämrar möjligheten att ge kunderna korrekt besöksspårningsinformation. En ändring införs i Adobes CNAME-spårningsservrar för att lagra besökarens Experience Cloud ID (ECID) i en cookie från en första part.

Den här ändringen är bara användbar för ECID-kunder som använder en CNAME från Analytics i förstahandskontext. Om du är en analyskund som för närvarande inte använder CNAME, eller till och med en icke-analyskund, är du fortfarande berättigad till en CNAME-post. Kontakta kundtjänst eller din kontorepresentant för att starta registreringen av en [CNAME](https://marketing.adobe.com/resources/help/en_US/whitepapers/first_party_cookies/adobe_managed_cert_pgm.html).

Uppgradera till ECID-bibliotek v. 4.3.0 + för att utnyttja denna förändring.

**Design**

När en ID-begäran har gjorts i demdex.net och ett ECID har hämtats görs en ID-begäran i kundens domän om en spårningsserver har angetts i ditt ECID-bibliotek. Den här slutpunkten läser den ecid-param från frågesträngen och ställer in en ny [cookie](/help/introduction/cookies.md) som endast innehåller ECID och ett förfallodatum två år framåt. Varje gång den här slutpunkten anropas på det här sättet skrivs cookien om med ett förfallodatum två år från tidpunkten för anropet. `s_ecid` ECID-biblioteket måste uppdateras till v 4.3.0 så att värdet för denna cookie kan hämtas.

Denna nya `s_ecid` cookie följer samma avanmälningsstatus som AMCV-cookien. Om e-id:t läses från `s_ecid` cookien anropas alltid demdex omedelbart för att hämta den senaste avanmälningsstatusen för det ID:t och lagras i AMCV-cookien.

Om din konsument dessutom har avanmält sig från Analytics-spårning via den här [metoden](https://marketing.adobe.com/resources/help/en_US/sc/implement/opt_out_link.html)kommer denna `s_ecid` cookie att tas bort.

Spårningsservernamnet ska anges till VisitorJS-biblioteket när biblioteket initieras med trackingServer eller trackingServerSecure. Detta bör matcha konfigurationen trackingServer i Analytics-konfigurationerna.

Om du väljer att inte utnyttja den här metoden lägger du till följande konfiguration i implementeringen av ECID-biblioteket: discardtrackingServerECID. När den här konfigurationen är true läser Visitor-biblioteket inte det MID som angetts av spårningsservern för första part.

![](assets/itp-proposal-v1.png)

## Använd metoden appendVisitorIDsTo för spårning mellan domäner (inom det egna företagets flera domäner)

Med den här funktionen kan du dela en besökares ECID över domäner när webbläsare blockerar cookies från tredje part. Om du vill använda den här funktionen måste du ha implementerat ID-tjänsten och äga käll- och måldomänerna. Finns i VisitorAPI.js version 1.7.0 eller senare (men inte i version 1.10.0).

**Design**

* När en besökare bläddrar till dina andra domäner returnerar Visitor.appendVisitorIDsTo(url) en URL med ett ECID som tillägg som frågeparameter.

   Använd den här URL:en för att omdirigera från den ursprungliga domänen till måldomänen.

* ID-tjänstkoden på måldomänen extraherar ECID från URL:en i stället för att skicka en begäran till Adobe om besökarens ID.

   Denna begäran innehåller cookie-ID från tredje part, som inte är tillgängligt i det här fallet.

* ID-tjänstkoden på målsidan använder det inskickade ECID:t för att spåra besökaren.

   >[!NOTE]
   >Om målsidan redan har ett ECID från tidigare besök styrs beslutet att skriva över den befintliga cookien av den här konfigurationen overwriteCrossDomainMCIDAndAID. Mer information om den här konfigurationen finns i [overwriteCrossDomainMCIDAndAID](/help/library/function-vars/overwrite-visitor-id.md).
   >
   >Mer information om den här metoden finns på [referenssidan för appendVisitorIDsTo (Cross Domain Tracking)](/help/library/get-set/appendvisitorid.md) .