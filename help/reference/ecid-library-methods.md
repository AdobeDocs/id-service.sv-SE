---
title: ECID-biblioteksmetoder i en Safari ITP-värld
description: Dokumentation för Adobe ECID-bibliotek (ID Service).
exl-id: ac1d1ee1-2b5f-457a-a694-60bb4c960ae7
source-git-commit: cb89ac70e37f35d5e4e2b971f2df9645304522f8
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# ECID-biblioteksmetoder i en Safari ITP-värld

>[!NOTE]
>
>Uppdateringar har gjorts för att återspegla de senaste ändringarna av ITP som släpptes den 12 november 2020 som en del av Big Sur OS-versionen.

Eftersom Safari effektiviserar spårningen över domäner via ITP måste Adobe upprätthålla bästa praxis för bibliotek som stöder kunder samt konsumentintegritet och -val.

Från och med den 10 november 2020 har alla beständiga cookies från första part som anges via API:t document.cookie, som ofta kallas&quot;cookies på klientsidan&quot;, och cookies som anges via CNAME-implementeringar från första part i Safari och iOS-webbläsare på mobila enheter en utgångsgräns på sju dagar. Cookies från tredje part kommer även fortsättningsvis att blockeras, vilket anges i tidigare versioner av ITP. Mer information om ITP 2.1 och hur Adobe påverkar lösningar finns i [Safari ITP 2.1 Impact on Adobe Experience Cloud and Experience Platform Customers](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).

## ITP-relaterade ändringar, metoder och konfigurationer

När ytterligare metoder skapas för spårning i Safari läggs de till som referens till den här sidan.

>[!NOTE]
>
>*ECID* = *MID* = *MCID* i all dokumentation nedan.

Nedan finns information om insatser för användning av ITP- och ECID-bibliotek.

## Aktuellt ECID-biblioteksbeteende med ITP och Apple WebKit

ITP 2.1 förhindrar möjligheten att skriva cookies på klientsidan, vilket försämrar möjligheten att ge kunderna korrekt besöksspårningsinformation. En förändring införs i Adobe CNAME-spårningsservrar för att lagra besökarens Experience Cloud ID (ECID) i en cookie från en annan leverantör.

Den här ändringen är bara användbar för ECID-kunder som använder en CNAME från Analytics i förstahandskontext. Om du är en analyskund som för närvarande inte använder CNAME, eller till och med en icke-analyskund, är du fortfarande berättigad till en CNAME-post. Kontakta kundtjänst eller din kontorepresentant för att starta registreringen av en [CNAME](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=sv-SE).

Uppgradera till ECID-bibliotek v. 4.3.0 + för att utnyttja denna förändring.

Följande visar hur ECID-biblioteket fungerar med ITP 2.1 och de senaste ändringarna som gjorts av Apple som en del av Big Sur-versionen

**Design**

När en ID-begäran har gjorts på demdex.net och ett ECID har hämtats görs en ID-begäran till kundens domän om en spårningsserver har angetts i ditt ECID-bibliotek. Den här slutpunkten läser den ecid-param från frågesträngen och ställer in en ny [cookie](/help/introduction/cookies.md) som endast omfattar ECID och ett förfallodatum två år framåt. Varje gång den här slutpunkten anropas på det här sättet skrivs cookien `s_ecid` om med ett förfallodatum två år från tidpunkten för anropet. ECID-biblioteket måste uppdateras till v 4.3.0 så att värdet för denna cookie kan hämtas.

>[!IMPORTANT]
>
>Som en del av Big Sur-uppdateringarna hålls även en `s_ecid`-cookie som angetts via CNAME till sju dagars utgång.

Den nya `s_ecid`-cookien följer samma avanmälningsstatus som AMCV-cookien. Om e-id:t läses från `s_ecid`-cookien anropas alltid DEDEX omedelbart för att hämta den senaste avanmälningsstatusen för det ID:t och lagras i AMCV-cookien.

Om din konsument har avanmält sig från Analytics-spårning via den här [metoden](https://experienceleague.adobe.com/docs/analytics/implementation/js/opt-out.html?lang=sv-SE) tas den här `s_ecid`-cookien bort.

Spårningsservernamnet måste anges till VisitorJS-biblioteket när biblioteket initieras med `trackingServer` eller `trackingServerSecure`. Detta bör matcha `trackingServer`-konfigurationen i Analytics-konfigurationerna.

Om du väljer att inte utnyttja den här metoden lägger du till följande konfiguration i ECID-biblioteksimplementeringen: `discardtrackingServerECID`. När den här konfigurationen är true läser Visitor-biblioteket inte det MID som angetts av den första part-spårningsservern.

![](assets/itp-proposal-v1.png)

## Använd metoden appendVisitorIDsTo för spårning mellan domäner (inom det egna företagets flera domäner)

Med den här funktionen kan du dela en besökares ECID över domäner när webbläsare blockerar cookies från tredje part. Om du vill använda den här funktionen måste du ha implementerat ID-tjänsten och äga käll- och måldomänerna. Finns i VisitorAPI.js version 1.7.0 eller senare (men inte i version 1.10.0).

**Design**

* När en besökare bläddrar till dina andra domäner returnerar Visitor.appendVisitorIDsTo(url) en URL med ett ECID som tillägg som frågeparameter.

  Använd den här URL:en för att omdirigera från den ursprungliga domänen till måldomänen.

* ID-tjänstkoden på måldomänen extraherar ECID från URL:en i stället för att skicka en begäran till Adobe för besökarens ID.

  Denna begäran innehåller cookie-ID från tredje part, som inte är tillgängligt i det här fallet.

* ID-tjänstkoden på målsidan använder det inskickade ECID:t för att spåra besökaren.

  >[!NOTE]
  >Om målsidan redan har ett ECID från tidigare besök styrs beslutet att skriva över den befintliga cookien av den här konfigurationen overwriteCrossDomainMCIDAndAID. Mer information om den här konfigurationen finns i [overwriteCrossDomainMCIDAndAID](/help/library/function-vars/overwrite-visitor-id.md).
  >
  >Mer information om den här metoden finns på referenssidan för [appendVisitorIDsTo (spårning av korsdomän)](/help/library/get-set/appendvisitorid.md).
