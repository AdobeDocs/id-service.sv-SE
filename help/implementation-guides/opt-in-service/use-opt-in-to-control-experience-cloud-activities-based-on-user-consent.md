---
title: Använd Opt-in för att styra Experience Cloud-aktiviteter baserat på användargodkännande
description: Objektet Adobe Opt-in är ett tillägg till Adobe Experience Platform Identity Service, som är utformat för att hjälpa dig att kontrollera om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor eller initiera beacons, baserat på slutanvändarens samtycke.
exl-id: ac44e628-01ca-401c-864b-30fed0450e5f
source-git-commit: 0dca594c090095a01dfa2d02a98dfeba7ca02dca
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Åtgärder för kontroll av Experience Cloud baserat på användares samtycke

Adobe [!UICONTROL Opt-in] Objektet är ett tillägg till Adobe [!UICONTROL Experience Platform Identity Service], som är utformat för att hjälpa dig att kontrollera om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor eller initiera beacons, baserat på slutanvändarens samtycke.

## Grunderna i [!UICONTROL Opt-In]

En viktig aspekt av reglerna för integritetsskydd är förvärv och överföring av användarnas samtycke över hur deras personuppgifter får användas och av vem. Den senaste versionen av [!UICONTROL Identity Service] innehåller funktioner som ger villkorlig utsändning (t.ex. före och efter samtycke) av Experience Cloud-lösningstaggar, baserat på huruvida slutanvändaren ger sitt samtycke. Den här processen visas i följande bild:

![Diagram över hur [!UICONTROL Opt-in] verk](assets/opt-in.png)

[!UICONTROL Opt-in] fungerar på följande sätt:

**If [!UICONTROL Opt-in] är aktiverat i identitetstjänsten (via en boolesk variabel), vilket gör att Experience Cloud-lösningsbiblioteken inte kan aktivera taggar eller ange cookies förrän du har gett sitt samtycke till den lösningen.**

[!UICONTROL Opt-in] ger dig även möjlighet att bestämma om taggar ska aktiveras innan användaren ger sitt medgivande, och sedan lagras den här informationen (tillsammans med det medgivande användaren ger) så att den kan användas vid efterföljande träffar. Godkännandet finns tillgängligt i [!UICONTROL Opt-in] eller så kan du integrera med en CMP och låta den lagra val av samtycke.

## Aktivera och konfigurera [!UICONTROL Opt-In]

[!UICONTROL Opt-in] är enklast att konfigurera med Adobe Experience Platform-taggar (tidigare Launch). I följande korta video ser du hur det fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/26431/?quality=12)

Om du inte använder Experience Platform-taggar kan du ange [!UICONTROL Opt-in]konfigurationen i initieringen av det globala Visitor-objektet, vilket visas i [dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/getting-started.html?lang=en).

## Implementering [!UICONTROL Opt-In] på sidan

Allt detta är under förberedelser för att ge besökarna ett gränssnitt som kan presenteras med samtycke. Det här användargränssnittet kan skapas av dig eller så kan du använda en CMP-partner (Consent Management Platform) för att skapa användargränssnittet.

När du konfigurerar ett användargränssnitt som ska användas [!UICONTROL Opt-in] för att samla in samtycke bör den konfigureras att anropa API:er som kan kopplas till [!UICONTROL Opt-in] och informera om att ge sitt samtycke till vissa eller alla Adobe Experience Cloud-lösningar. Detaljerad information om dessa API:er finns i [Referensdokumentation för deltagande](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/api.html?lang=en). Ytterligare information om deltagande finns också på de omgivande dokumentationssidorna.

## [!UICONTROL Opt-In] Demo

I följande video finns en kort demonstration av [!UICONTROL Opt-in] och hur det kan påverka cookies, initiera beacons och så vidare i Experience Cloud-lösningar.

>[!VIDEO](https://video.tv.adobe.com/v/26432/?quality=12)

**OBS!** Det är viktigt att notera att när denna artikel skrivs ska [!UICONTROL Opt-in] har inte byggts in i biblioteken för alla Experience Cloud-program. Biblioteken som för närvarande stöds av [!UICONTROL Opt-in] är:

* Identitetstjänst
* Analytics 
* Audience Manager
* [!DNL Target]
