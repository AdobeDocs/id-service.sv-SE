---
description: Ändra standarddomännamnet som används av anrop till Experience Cloud identitetstjänst till ditt eget underdomännamn med dessa konfigurationer.
keywords: ID-tjänst
title: auditionManagerServer och auditionManagerServerSecure
exl-id: b740eb5c-ac4e-46f4-ba7c-1080d8d9292d
source-git-commit: 7ef084bc1add5a4ea8c7be738055b0c21e247eea
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# auditionManagerServer och auditionManagerServerSecure{#audiencemanagerserver-and-audiencemanagerserversecure}

Ändra standarddomännamnet som används av anrop till Experience Cloud identitetstjänst till ditt eget underdomännamn med dessa konfigurationer.

**Syntax:**

* `audienceManagerServer: " *`ditt underdomännamn`*.demdex.net"`
* `audienceManagerServerSecure: " *`ditt underdomännamn`*.demdex.net"`

**Syfte**

Vanligtvis gör ID-tjänsten [!DNL Experience Cloud] anrop till [!DNL Adobe] vid `dpm.demdex.net`. Ibland kanske du inte vill ringa anrop till den här destinationen eftersom den ser för generisk ut eller &quot;från tredje part&quot;. Använd dessa konfigurationer för att lägga till ditt [!DNL Audience Manager]-underdomännamn i `demdex.net` så att ID-tjänstanropet ser mer ut som ett förstahandsanrop. Mer information om `dpm.demdex.net`-anropet finns i [Förstå anrop till Demdex-domänen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html).

**Krav**

Dessa konfigurationer kräver att du använder:

* Postens [!DNL Audience Manager]-underdomännamn för ditt företag. Bekräfta eller hämta det här namnet från din konsult.
* Underdomännamnet som är associerat med din [!UICONTROL Organization ID].
* *Båda*-konfigurationsparametrarna har samma underdomännamn.

**Kodexempel**

I det här exemplet ska vi säga att vi har ett mediespelarföretag som har uttryckt juridiska betänkligheter när det gäller att ringa till `dpm.demdex.net`. I [!DNL Audience Manager] är företagsunderdomännamnet för posten Musik1. I följande kodexempel visas hur ID-tjänstanropet varumärkesprofileras med det här kundspecifika underdomännamnet.

```
//Instantiate Visitor 
var visitor = Visitor.getInstance("Insert Experience Cloud Organization ID here",{ 
     ... 
     //Configure ID service call 
     audienceManagerServer: "Music1.demdex.net", 
     audienceManagerServerSecure: "Music1.demdex.net" 
     } 
);
```
