---
description: Tillsammans med besökar-ID:t för Experience Cloud kan du koppla ytterligare kund-ID:n och en autentiseringsstatus till varje besökare.
keywords: ID-tjänst
title: Kund-ID:n och autentiseringstillstånd
exl-id: 0215225c-20f5-4e44-a368-b2df683aca9d
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 6%

---

# Kund-ID:n och autentiseringstillstånd {#customer-ids-and-authentication-states}

Tillsammans med besökar-ID:t för Experience Cloud kan du koppla ytterligare kund-ID:n och en autentiseringsstatus till varje besökare.

## Autentiseringstillstånd {#section-68ad4065dfaa437d9070832d6e2bf85c}

Metoden `setCustomerIDs` accepterar flera kund-ID:n för samma besökare. Detta hjälper er att identifiera eller rikta in er på en enskild användare på olika enheter. Du kan till exempel överföra dessa ID:n som [kundattribut](https://docs.adobe.com/content/help/sv-SE/core-services/interface/customer-attributes/attributes.html) till [!DNL Experience Cloud] och få tillgång till dessa data via olika lösningar.

>[!IMPORTANT]
>
>`setCustomerIDs` (synkronisering av kund-ID) krävs av kundattribut och centrala tjänster. Synkroniserande kund-ID:n är en valfri identifieringsmetod för [!DNL Analytics]. [!DNL Target] kräver  `Visitor.AuthState.AUTHENTICATED` att kundattribut fungerar. Se [bastjänster - Så här aktiverar du dina lösningar](https://docs.adobe.com/content/help/en/core-services/interface/about-core-services/core-services.html) för exempel.

Med början från Experience Cloud identitetstjänst v1.5+ inkluderar `setCustomerIDs` det valfria `AuthState`-objektet. `AuthState` identifierar besökare utifrån deras autentiseringsstatus (t.ex. inloggad, utloggad). Du anger autentiseringstillståndet med ett statusvärde i tabellen. Autentiseringsstatus returneras som ett heltal.

<table id="table_8547671CC97145529981FBF6C302BEC5"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Autentiseringsstatus </th> 
   <th colname="col2" class="entry"> Statusheltal </th> 
   <th colname="col3" class="entry"> Användarstatus </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> Visitor.AuthState.UNKNOWN  </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> 0  </span> </p> </td> 
   <td colname="col3"> <p>Okänd eller aldrig autentiserad. </p> <p> Okänd används som standard när <span class="codeph"> AuthState </span> inte används med ett besökar-ID eller inte uttryckligen anges på varje sida eller i appkontext. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> Visitor.AuthState.AUTHENTICATED  </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> 3  </span> </p> </td> 
   <td colname="col3"> <p>Autentiserad för en viss instans, sida eller app. </p> <p> <p>Obs!  För att kundattributen för <span class="keyword">-målet </span> ska fungera på rätt sätt krävs den här statusen. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> Visitor.AuthState.LOGGED_OUT  </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> 2  </span> </p> </td> 
   <td colname="col3"> <p>Utloggad. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Använd ärenden för autentiseringslägen {#section-fe9560cc490943b29dac2c4fb6efd72c}

Du kan tilldela autentiseringstillstånd till dina användare, beroende på vilka åtgärder de utför på dina webbegenskaper och om de är autentiserade. Se några exempel i tabellen nedan:

<table id="table_3769E79304014C4F87094B87A8ACE4E0"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Autentiseringsstatus </th> 
   <th colname="col2" class="entry"> Användningsfall </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> Visitor.AuthState.UNKNOWN  </span> </p> </td> 
   <td colname="col2"> <p>Det här läget kan användas för scenarier som: </p> <p> 
     <ul id="ul_086C7446D258443DA7AF5BB96A6AAEC7"> 
      <li id="li_7845BBD62D7B4362AD3FE33DEDA8FBA1">Läsa ett e-postmeddelande (den här åtgärden innebär troligtvis att läsaren är den avsedda mottagaren, men e-postmeddelandet kan också ha vidarebefordrats). </li> 
      <li id="li_FAB7ACFC69624631BD01FC0ED84B23C5">Klicka igenom från ett e-postmeddelande till en landningssida. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> Visitor.AuthState.AUTHENTICATED  </span> </p> </td> 
   <td colname="col2"> <p>Användaren autentiseras för närvarande med en aktiv session på din webbplats eller i din app. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> Visitor.AuthState.LOGGED_OUT  </span> </p> </td> 
   <td colname="col2"> <p>Användaren autentiserades men loggades aktivt ut. Användaren avsåg att koppla från det autentiserade läget. Användaren vill inte längre behandlas som autentiserad. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Ange kund-ID och autentiserade tillstånd {#section-ec4b367d16ad4ac1a1baca9b01f4ee98}

Kund-ID:n kan innehålla kombinationer av ID:n och autentiserade tillstånd som visas i följande exempel.

>[!IMPORTANT]
>
>* ID:n är skiftlägeskänsliga.
>* Använd bara okodade värden för dina ID:n.
>* Kund-ID:n och autentiseringstillstånd lagras inte i cookien för besökar-ID. De måste anges för varje sida eller programkontext.
>* Du bör inte inkludera någon personligt identifierbar information (PII) i kund-ID:n. Om du använder PII för att identifiera en besökare (till exempel en e-postadress) rekommenderar vi att du lagrar en hashad eller krypterad version av informationen i stället. ECID-biblioteket har stöd för att hash-koda användaridentifierare. Se [SHA256 Hashing Support for setCustomerIDs](/help/reference/hashing-support.md).


```js
// Single ID with a single authentication state 
visitor.setCustomerIDs({ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    } 
}); 
 
/* 
Multiple IDs with only the first ID explicitly assigned an authentication state. 
The second ID is not explicitly assigned an authentication state and is implicitly 
assigned Visitor.AuthState.Unknown by default. 
*/ 
visitor.setCustomerIDs({ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    }, 
    "dpuuid":"550e8400-e29b-41d4-a716-446655440000" 
}); 
 
// Multiple IDs with identical authentication states 
visitor.setCustomerIDs({ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    }, 
    "dpuuid":{ 
        "id":"550e8400-e29b-41d4-a716-446655440000", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    } 
}); 
 
// Multiple IDs with different authentication states 
visitor.setCustomerIDs({ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    }, 
    "dpuuid":{ 
        "id":"550e8400-e29b-41d4-a716-446655440000", 
        "authState":Visitor.AuthState.LOGGED_OUT 
    } 
}); 
```

## Returnera kund-ID:n och autentiserade tillstånd {#section-71a610546188478fa9a3185a01d6e83b}

Använd `getCustomerIDs` för att returnera kund-ID:n och relaterade autentiserade tillstånd. Den här metoden returnerar en besökares autentiserade tillstånd som ett heltal.

**Syntax**

`getCustomerIDs` returnerar data med följande syntax.

```js
{ 
    [customerIDType1]:{ 
        "id":[customerID1], 
        "authState":[authState1] 
    }, 
    [customerIDType2]:{ 
        "id":[customerID2], 
        "authState":[authState2] 
    } 
    ... 
}
```

**Exempel**

Returnerade kund-ID:n och autentiseringsstatusdata ska se ut ungefär som i följande exempel.

```js
Object customerIDs = visitor.getCustomerIDs(); 
  
// No setCustomerIDs call on this instance 
{} 
  
// setCustomerIDs call on this instance with {"userid":{"id":"67312378756723456"}} 
{ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":0 
    } 
} 
  
// setCustomerIDs call on this instance with {"userid":{"id":"67312378756723456","authState":Visitor.AuthState.AUTHENTICATED}} 
{ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":1 
    } 
} 
  
// setCustomerIDs call on this instance with {"userid":{"authState":Visitor.AuthState.LOGGED_OUT}} 
{ 
    "userid":{ 
        "authState":2 
    } 
} 
  
// setCustomerIDs call on this instance with {"userid":{"authState":Visitor.AuthState.LOGGED_OUT},"dpuuid":{"id":"550e8400-e29b-41d4-a716-446655440000"}} 
{ 
    "userid":{ 
        "authState":2 
    }, 
    "dpuuid":{ 
        "id":"550e8400-e29b-41d4-a716-446655440000", 
        "authState":0 
    } 
 }
```

## SDK-stöd {#section-861c6b3b1ba645dda133dccb22ec7bb0}

ID-tjänsten [!DNL Experience Cloud] stöder kund-ID:n och autentiseringstillstånd i vår Android- och iOS SDK-kod. Se följande kodbibliotek:

* [Android SDK-metoder](https://docs.adobe.com/content/help/sv-SE/mobile-services/android/overview.html)
* [iOS SDK-metoder](https://docs.adobe.com/content/help/sv-SE/mobile-services/ios/overview.html)

## Meddelande till Analytics- och Audience Manager-kunder {#section-3a8e9d51e71c4c6e865184b81ed9d99b}

Om du skickar deklarerade ID:n till [!DNL Audience Manager] måste `userid`-objektet matcha integrationskoden som är associerad med en datakälla. Mer information finns i avsnittet [!UICONTROL Visitor ID Service] i dokumentationen [Konfigurera kod för kopplingsregler](https://docs.adobe.com/help/en/audience-manager/user-guide/features/profile-merge-rules/merge-rules-start.html#configure-merge-rule-code).
