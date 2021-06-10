---
description: setCustomerIDs anger 1 eller flera nyckelvärdepar som definierar kund-ID:n och deras autentiseringstillstånd.
keywords: ID-tjänst
title: setCustomerIDs
exl-id: 8fc549d3-2a6f-4214-bb0d-3e0bc1501ce2
source-git-commit: 06e935a4ba4776baa900d3dc91e294c92b873c0f
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 1%

---

# setCustomerIDs{#setcustomerids}

setCustomerIDs anger 1 eller flera nyckelvärdepar som definierar kund-ID:n och deras autentiseringstillstånd.

**Syntax:** `visitor.setCustomerIDs()`

Du kan ange ett eller flera ID:n enligt exemplet nedan. Mer information och exempel finns i [Kund-ID och autentiseringstillstånd](../../reference/authenticated-state.md).

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
