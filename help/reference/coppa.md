---
description: Enligt lagen om skydd av barns integritet online (COPPA) är det förbjudet att samla in personuppgifter online från barn som är yngre än 13 år utan verifierbart föräldrars samtycke. Kunder som är intresserade av COPPA kan lägga till en valfri variabel i Experience Cloud Identity Service-koden som förhindrar att den ställer in cookies i en webbläsares tredjepartsdomän.
keywords: ID-tjänst
title: Stöd för COPPA i Experience Cloud Identity Service
exl-id: c7579f90-3011-4e26-b908-08907bf12ba2
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Stöd för COPPA i Experience Cloud Identity Service {#coppa-support-in-the-experience-cloud-id-service}

Enligt lagen om skydd av barns integritet online (COPPA) är det förbjudet att samla in personuppgifter online från barn som är yngre än 13 år utan verifierbart föräldrars samtycke. Kunder som är intresserade av COPPA kan lägga till en valfri variabel i Experience Cloud Identity Service-koden som förhindrar att den ställer in cookies i en webbläsares tredjepartsdomän.

>[!NOTE]
>
>För version 3.0.0 eller senare.

**Cookies och spårning**

När en webbsida läses in anropar ID-tjänsten [!DNL Experience Cloud] en [!DNL Adobe] datainsamlingsserver (DCS). DCS-svaret innehåller en Experience Cloud-cookie och en demdex.net.

* Cookien Experience Cloud anges i den första partdomänen. Det kan inte användas för att spåra besökare över olika domäner, såvida inte dessa domäner fungerar tillsammans för att tillåta åtkomst.
* demdex.net cookie anges i tredjepartsdomänen. Den innehåller en unik identifierare som kan användas för att spåra besökare i olika domäner.

**Cookies och COPPA-kompatibilitet**

Cookies från tredje part som spårar besökare i olika domäner på webbplatser som dirigeras till (eller huvudsakligen till) barn, utlöser krav på samtycke från COPPA-föräldrar. Om du enklare vill följa COPPA för intern webbplatsanalys lägger du till variabeln `disableThirdPartyCookies:true` i funktionen `Visitor.getInstance` enligt nedan.

```js
//Call the ID service 
var visitor = Visitor.getInstance("insert marketing cloud ID here", { 
 
    //Set disableThirdPartyCookies configuration param 
    disableThirdPartyCookies: true 
 
    ... 
});
```

När `true` anges stoppar objektet `disableThirdPartyCookies` DCS från att returnera demdex.net cookie från tredje part. Om en besökare redan har denna cookie i sin webbläsare kommer ID-tjänsten inte att använda den för att skapa ett nytt [!DNL Experience Cloud]-ID eller returnera ett befintligt ID. I stället skapar ID-tjänsten [!DNL Experience Cloud] ett nytt slumpmässigt ID i cookie-filen för den första parten. När den är aktiverad kan du samla in data med ID-tjänsten och dela den mellan olika [!DNL Experience Cloud]-lösningar, inklusive andra interna åtgärder som tillåts av COPPA.

>[!MORELIKETHIS]
>
>* [Sekretesscenter för Adobe](http://www.adobe.com/privacy.html)
>* [Vad är COPPA?](http://www.consumer.ftc.gov/articles/0031-protecting-your-childs-privacy-online#whatis)
