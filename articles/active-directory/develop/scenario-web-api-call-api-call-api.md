---
title: 'Web-API, die Web-APIs aufruft: Microsoft Identity Platform | Azure'
description: Hier erfahren Sie, wie Sie eine Web-API erstellen, die Web-APIs aufruft.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: b756d7df03bd3c06b703617dbf84a194d716f1e3
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "87026372"
---
# <a name="a-web-api-that-calls-web-apis-call-an-api"></a>Eine Web-API, die Web-APIs aufruft: Aufrufen einer API

Sobald Sie über ein Token verfügen, können Sie eine geschützte Web-API aufrufen. Dafür verwenden Sie den Controller Ihrer Web-API.

## <a name="controller-code"></a>Controllercode

# <a name="aspnet-core"></a>[ASP.NET Core](#tab/aspnetcore)

Der folgende Code setzt den Beispielcode fort, den Sie hier finden: [Eine Web-API, die Web-APIs aufruft: Abrufen eines Tokens für die App](scenario-web-api-call-api-acquire-token.md). Der Code wird in den Aktionen der API-Controller aufgerufen. Er ruft eine nachgelagerte API namens *todolist* auf.

Nachdem Sie das Token abgerufen haben, können Sie es als Bearertoken zum Aufrufen der nachgelagerten API verwenden.

```csharp
private async Task CallTodoListService(string accessToken)
{

// After the token has been returned by Microsoft Identity Web, add it to the HTTP authorization header before making the call to access the To Do list service.
_httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

// Call the To Do list service.
HttpResponseMessage response = await _httpClient.GetAsync(TodoListBaseAddress + "/api/todolist");
...
}
```

# <a name="java"></a>[Java](#tab/java)

Der folgende Code setzt den Beispielcode fort, den Sie hier finden: [Eine Web-API, die Web-APIs aufruft: Abrufen eines Tokens für die App](scenario-web-api-call-api-acquire-token.md). Der Code wird in den Aktionen der API-Controller aufgerufen. Er ruft die Downstream-API von Microsoft Graph auf.

Nachdem Sie das Token abgerufen haben, können Sie es als Bearertoken zum Aufrufen der nachgelagerten API verwenden.

```Java
private String callMicrosoftGraphMeEndpoint(String accessToken){
    RestTemplate restTemplate = new RestTemplate();

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_JSON);

    headers.set("Authorization", "Bearer " + accessToken);

    HttpEntity<String> entity = new HttpEntity<>(null, headers);

    String result = restTemplate.exchange("https://graph.microsoft.com/v1.0/me", HttpMethod.GET,
            entity, String.class).getBody();

    return result;
}
```

# <a name="python"></a>[Python](#tab/python)
Ein Beispiel zur Veranschaulichung dieses Flows mit MSAL Python ist noch nicht verfügbar.

---

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Eine Web-API, die Web-APIs aufruft: Übergang in die Produktion](scenario-web-api-call-api-production.md)
