---
description: setCustomerIDs anger 1 eller flera nyckelvärdepar som definierar kund-ID:n och deras autentiseringstillstånd.
keywords: ID Service
seo-description: setCustomerIDs anger 1 eller flera nyckelvärdepar som definierar kund-ID:n och deras autentiseringstillstånd.
seo-title: setCustomerIDs
title: setCustomerIDs
uuid: 4f960f98-cec2-4db6-84ea-0259e2128ea2
translation-type: tm+mt
source-git-commit: 21fb12b817b7c8cd34e6022ca6c188229228d1df
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# setCustomerIDs{#setcustomerids}

setCustomerIDs anger 1 eller flera nyckelvärdepar som definierar kund-ID:n och deras autentiseringstillstånd.

**Syntax:** `visitor.setCustomerIDs()`

Du kan ange ett eller flera ID:n enligt exemplet nedan. Mer information och exempel finns i [Kund-ID:n och autentiseringstillstånd](../../reference/authenticated-state.md) .

```js
// Single ID with a single authentication state 
visitor.setCustomerIDs({ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    } 
}); 
 
//Multiple IDs with a single authentication state 
visitor.setCustomerIDs({ 
    "userid":{ 
        "id":"67312378756723456", 
        "authState":Visitor.AuthState.AUTHENTICATED 
    }, 
    "dpuuid":"550e8400-e29b-41d4-a716-446655440000" 
});
```

