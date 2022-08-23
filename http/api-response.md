---
description: Standardize API responses
---

# API Response

When building an API a usual problem is not having standard, organized and structured responses. An API should always return the same structure and inform the client correctly about any error.

To help you with this, the framework offers this **optional** tool, a class named **APIResponse**. This class will handle the response structure for you:

<pre class="language-php"><code class="lang-php"><strong>return ApiResponse::success($data);
</strong>
ApiResponse::badRequest();
ApiResponse::badRequest($message);
ApiResponse::badRequest($message, $data);

ApiResponse::forbidden();
ApiResponse::notAuthorized();
ApiResponse::notFound();
ApiResponse::error();</code></pre>

You can also use the generic method **failRequest** and specify the response type as the first parameter:

```php
ApiResponse::fail('method-not-allowed', $message?, $data?);
```

{% hint style="info" %}
The **success** method will just return the response as an array (object), you'll still have to return that to the client. But the failure methods (badRequest, forbidden, etc) **will automatically end the process** (die).
{% endhint %}

### Paginated lists

APIResponse also helps with paginating results. All you need is a list of items, and indicate the pagination settings:

```php
return ApiResponse::paginate( $items, [
    'pageSize' => 10,   // Items per page 
    'total' => 1250,    // Total items
]);
```
