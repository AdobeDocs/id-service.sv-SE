---
title: Använd Opt-in för att styra Experience Cloud-aktiviteter baserat på användargodkännande
description: Objektet Adobe Opt-in är ett tillägg till Adobe Experience Platform Identity Service, som är utformat för att hjälpa dig att kontrollera om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor eller initiera beacons, baserat på slutanvändarens samtycke.
exl-id: ac44e628-01ca-401c-864b-30fed0450e5f
source-git-commit: 0dca594c090095a01dfa2d02a98dfeba7ca02dca
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Åtgärder för kontroll av Experience Cloud baserat på användares samtycke

Objektet Adobe [!UICONTROL Opt-in] är ett tillägg till Adobe [!UICONTROL Experience Platform Identity Service] som är utformat för att hjälpa dig att kontrollera om och vilka Experience Cloud-lösningar som kan skapa cookies på webbsidor eller initiera beacons, baserat på slutanvändarens samtycke.

## Grunderna för [!UICONTROL Opt-In]

En viktig aspekt av reglerna för integritetsskydd är förvärv och överföring av användarnas samtycke över hur deras personuppgifter får användas och av vem. Den senaste versionen av [!UICONTROL Identity Service] innehåller funktioner som ger villkorsstyrd utsändning (till exempel före och efter samtycke) av lösningstaggar för Experience Cloud, baserat på om slutanvändaren ger sitt samtycke. Den här processen visas i följande bild:

![Diagram över hur [!UICONTROL Opt-in] fungerar](assets/opt-in.png)

[!UICONTROL Opt-in] fungerar så här:

**Om [!UICONTROL Opt-in] är aktiverat i identitetstjänsten (via en boolesk variabel) fördröjs Experience Cloud-lösningsbiblioteken från att aktivera taggar eller ange cookies tills du har gett ditt medgivande till den lösningen.**

I [!UICONTROL Opt-in] kan du också bestämma om taggar ska aktiveras innan användaren ger sitt samtycke, och sedan lagras den här medgivandeinformationen (tillsammans med det medgivande som slutanvändaren gett) så att den kan användas vid efterföljande träffar. Lagring av medgivandet är tillgängligt i alternativen för [!UICONTROL Opt-in], eller så kan du integrera med en CMP och låta den lagra val av samtycke.

## Aktivera och konfigurera [!UICONTROL Opt-In]

[!UICONTROL Opt-in] är enklast att konfigurera med Adobe Experience Platform-taggar (tidigare Launch). I följande korta video ser du hur det fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/26431/?quality=12)

Om du inte använder Experience Platform-taggar kan du ange konfigurationen för [!UICONTROL Opt-in] i initieringen av det globala Visitor-objektet, vilket visas i [dokumentationen](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/getting-started.html?lang=sv-SE).

## Implementera [!UICONTROL Opt-In] på sidan

Allt detta är under förberedelser för att ge besökarna ett gränssnitt som kan presenteras med samtycke. Det här användargränssnittet kan skapas av dig eller så kan du använda en CMP-partner (Consent Management Platform) för att skapa användargränssnittet.

När du konfigurerar ett användargränssnitt för att använda [!UICONTROL Opt-in] för att samla in samtycke, bör det konfigureras att anropa API:er som ansluter till [!UICONTROL Opt-in] och informera det om att ge sitt samtycke till vissa eller alla Adobe Experience Cloud-lösningar. Detaljerad information om dessa API:er finns i [Opt-in Reference-dokumentationen](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/api.html?lang=sv-SE). Ytterligare information om deltagande finns också på de omgivande dokumentationssidorna.

## [!UICONTROL Opt-In] demo

I följande videofilm visas en snabb demonstration av [!UICONTROL Opt-in] som fungerar på sidan och hur den kan påverka om Experience Cloud-lösningar kan ställa in cookies, initiera beacons och så vidare.

>[!VIDEO](https://video.tv.adobe.com/v/26432/?quality=12)

**Obs!** Observera att [!UICONTROL Opt-in] inte har byggts in i biblioteken för alla Experience Cloud-program när den här artikeln skrevs. Biblioteken som för närvarande stöds för [!UICONTROL Opt-in] är:

* Identitetstjänst
* Analytics 
* Audience Manager
* [!DNL Target]
