---
description: Standardize API responses
---

# API Response

When building an API a usual problem is not having standard, organized and useful responses, whether if it's a success o an error.

To help you with this, the framework gives you this **optional** tool, a class named **APIResponse**. This class will handle the response structure for you:

```
APIResponse::success($data);

APIResponse::badRequest();
APIResponse::badRequest($message);
APIResponse::badRequest($message, $data);

APIResponse::forbidden();
APIResponse::notAuthorized();
APIResponse::notFound();
APIResponse::error();
```

You can also use the generic method **failRequest** and specify the response type as the first parameter:

```
APIResponse::failRequest('method-not-allowed', $message?, $data?);
```

{% hint style="info" %}
You can find the list of response types in a table in the section HTTP > Responses
{% endhint %}

### Authentication responses

This class also gives you responses for the login management:

```
APIResponse::tokenExpired($message?);

APIResponse::logged($token, $refreshToken?, $extraData?);
APIResponse::logged($tk, null, [
    'userId' => $uid
]);
```
