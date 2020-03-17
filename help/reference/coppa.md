---
description: Enligt lagen om skydd av barns integritet online (COPPA) är det förbjudet att samla in personuppgifter online från barn som är yngre än 13 år utan verifierbart föräldrars samtycke. Kunder som är intresserade av COPPA kan lägga till en valfri variabel i sin Experience Cloud Identity Service-kod som förhindrar att den ställer in cookies i en webbläsares tredjepartsdomän.
keywords: ID Service
seo-description: Enligt lagen om skydd av barns integritet online (COPPA) är det förbjudet att samla in personuppgifter online från barn som är yngre än 13 år utan verifierbart föräldrars samtycke. Kunder som är intresserade av COPPA kan lägga till en valfri variabel i sin Experience Cloud Identity Service-kod som förhindrar att den ställer in cookies i en webbläsares tredjepartsdomän.
seo-title: Stöd för COPPA i Experience Cloud Identity Service
title: Stöd för COPPA i Experience Cloud Identity Service
uuid: 621b5ebd-92e7-4635-be85-8d7e36589fcb
translation-type: tm+mt
source-git-commit: c4c0b791230422f17292b72fd45ba5689a60adae

---


# COPPA Support in the Experience Cloud Identity Service {#coppa-support-in-the-experience-cloud-id-service}

Enligt lagen om skydd av barns integritet online (COPPA) är det förbjudet att samla in personuppgifter online från barn som är yngre än 13 år utan verifierbart föräldrars samtycke. Kunder som är intresserade av COPPA kan lägga till en valfri variabel i sin Experience Cloud Identity Service-kod som förhindrar att den ställer in cookies i en webbläsares tredjepartsdomän.

>[!NOTE]
>
>För version 3.0.0 eller senare.

**Cookies och spårning**

När en webbsida läses in anropas en DCS-server (Data Collection Server) av [!DNL Experience Cloud] ID-tjänsten [!DNL Adobe] . DCS-svaret innehåller en Experience Cloud-cookie och en demdex.net-cookie.

* Experience Cloud-cookie är inställd i den första partdomänen. Det kan inte användas för att spåra besökare över olika domäner, såvida inte dessa domäner fungerar tillsammans för att tillåta åtkomst.
* Den här cookie-filen för demdex.net har angetts i tredjepartsdomänen. Den innehåller en unik identifierare som kan användas för att spåra besökare i olika domäner.

**Cookies och COPPA-överensstämmelse**

Cookies från tredje part som spårar besökare i olika domäner på webbplatser som dirigeras till (eller huvudsakligen till) barn, utlöser krav på samtycke från COPPA-föräldrar. Om du enklare vill följa COPPA för intern webbplatsanalys lägger du till variabeln `disableThirdPartyCookies:true` i `Visitor.getInstance` funktionen enligt nedan.

```js
//Call the ID service 
var visitor = Visitor.getInstance("insert marketing cloud ID here", { 
 
    //Set disableThirdPartyCookies configuration param 
    disableThirdPartyCookies: true 
 
    ... 
});
```

När det är inställt på `true`stoppar `disableThirdPartyCookies` objektet DCS från att returnera cookie-filen demdex.net från tredje part. Om en besökare redan har denna cookie i sin webbläsare kommer ID-tjänsten inte att använda den för att skapa ett nytt [!DNL Experience Cloud] ID eller returnera ett befintligt ID. I stället skapar [!DNL Experience Cloud] ID-tjänsten ett nytt slumpmässigt ID i cookie-filen för första part. När den är aktiverad kan du samla in data med ID-tjänsten och dela dem med olika [!DNL Experience Cloud] lösningar, inklusive andra interna åtgärder som tillåts av COPPA.

>[!MORELIKETHIS]
>
>* [Adobes sekretesscenter](http://www.adobe.com/privacy.html)
>* [Vad är COPPA?](http://www.consumer.ftc.gov/articles/0031-protecting-your-childs-privacy-online#whatis)

