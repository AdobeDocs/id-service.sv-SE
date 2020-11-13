---
title: Använd Opt-in för att styra Experience Cloud-aktiviteter baserat på användargodkännande
description: Objektet Adobe Opt-in är ett tillägg till Adobe Experience Platform Identity Service, som är utformat för att hjälpa dig att kontrollera om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor eller initiera beacons, baserat på slutanvändarens samtycke.
translation-type: tm+mt
source-git-commit: 3aba8820ef40d068c732a637be5ab67652a8d35d
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---


# Åtgärder för kontroll av Experience Cloud baserat på användares samtycke

Adobe [!UICONTROL Opt-in] Object är ett tillägg till Adobe [!UICONTROL Experience Platform Identity Service]som hjälper dig att styra om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor eller initiera beacons, baserat på vad slutanvändaren samtycker till.

## Grunderna i [!UICONTROL Opt-In]

En viktig aspekt av reglerna för integritetsskydd är förvärv och överföring av användarnas samtycke över hur deras personuppgifter får användas och av vem. Den senaste versionen av [!UICONTROL Identity Service] innehåller funktioner som är placerade mellan användaren (användargränssnittet) och Adobe och som ger villkorlig utsändning (t.ex. före och efter samtycke) av Adobe Experience Cloud-lösningstaggar baserat på om slutanvändaren har gett sitt samtycke. Detta visas i följande bild:

![Diagram över hur [!UICONTROL Opt-in] fungerar](assets/opt-in.png)

[!UICONTROL Opt-in] är gateekeeper... eller är det keymasten? Du bestämmer.

Det handlar om följande:

**Om [!UICONTROL Opt-in] är aktiverat i identitetstjänsten (via en boolesk variabel) försenas Experience Cloud-lösningsbiblioteken från att bränna taggar eller ange cookies tills man har gett sitt samtycke till den lösningen.**

[!UICONTROL Opt-in] ger dig även möjlighet att bestämma om några taggar avfyras även *innan* användaren ger sitt samtycke, och sedan lagras denna information (tillsammans med det medgivande som slutanvändaren gett) så att den kan användas vid efterföljande träffar. Lagring av samtycke finns tillgängligt i [!UICONTROL Opt-in] alternativen, eller så kan du integrera med en CMP och låta den lagra val av samtycke.

## Aktivera och konfigurera [!UICONTROL Opt-In]

[!UICONTROL Opt-in] är också enklare att konfigurera med Adobe Experience Platform Launch. I följande korta video ser du hur det fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/26431/?quality=12)

Om du inte använder Experience Platform Launch kan du ange [!UICONTROL Opt-in]konfigurationen i initieringen av det globala Visitor-objektet, vilket visas i [dokumentationen](https://marketing.adobe.com/resources/help/en_US/mcvid/getting-started.html).

## Implementera [!UICONTROL Opt-In] på sidan

Allt detta är under förberedelser för att ge besökarna ett gränssnitt som kan presenteras med samtycke. Det här användargränssnittet kan skapas av dig eller så kan du använda en CMP-partner (Consent Management Platform) för att skapa användargränssnittet.

När du konfigurerar ett användargränssnitt så att det används [!UICONTROL Opt-in] för att samla in samtycke bör det konfigureras att anropa API:er som kan ansluta till [!UICONTROL Opt-in] och informera det om att ge sitt samtycke till vissa eller alla Adobe Experience Cloud-lösningar. Detaljerad information om dessa API:er finns i [Opt-in Reference-dokumentationen](https://marketing.adobe.com/resources/help/en_US/mcvid/api.html). Ytterligare information om deltagande finns också på de omgivande dokumentationssidorna.

## [!UICONTROL Opt-In] Demo

I följande video visas en kort demonstration av hur du [!UICONTROL Opt-in] arbetar med sidan och hur det kan påverka om Experience Cloud-lösningar kan ställa in cookies, initiera beacons osv.

>[!VIDEO](https://video.tv.adobe.com/v/26432/?quality=12)

**OBS!** Det är viktigt att notera att när denna artikel skrevs [!UICONTROL Opt-in] har den inte byggts in i biblioteken för alla Experience Cloud-lösningar. Följande bibliotek stöds för närvarande [!UICONTROL Opt-in] :

* Identitetstjänst
* Analytics 
* Audience Manager
* [!DNL Target]
