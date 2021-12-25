---
description: Launch HTTP requests as client
---

# As client

Phyrus includes an integrated HTTP client capable of easily make requests to an API.

```
http::get( $url, $options );
http::post( $url, $options );
http::put( $url, $options );
http::delete( $url, $options );

http::req( $method, $url, $options );
```

A request returns a **Promise**, a class that works exactly like in Javascript:

```
http::get( $url )

// If request was successfull:
->then(function($response)  {

})
// If request failed:
->catch(function($error) {

})
// In any of both cases
->finally(function($arg) {

});
```

These are the **options** of the request:

| Option       | Description                                                                                                                                                                          | Example                                                                     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| headers      | Array key-value                                                                                                                                                                      | \[ 'Content-Type' => 'application/json' ]                                   |
| data         | <p>Array key-value.</p><p>On GET and DELETE requests, parameters are added to the URL</p>                                                                                            | \[ 'parameter' => 'value' ]                                                 |
| format       | <p>Default 'json'. Converts the data automatically.</p><ul><li>json = json_encode </li><li>url = urlencode </li><li>http = http_build_query</li><li>none = raw</li></ul>             | 'json'                                                                      |
| content-type | Default application/json. Can also be set through headers.                                                                                                                           | 'application/json'                                                          |
| decode       | <p>Default json. Automatically decodes the response. Possible values are:</p><ul><li>json = json_decode</li><li>xml = simplexml_load_string</li><li>none = nothing, string</li></ul> | 'json'                                                                      |
| auth         | Authorization header. Can also be set through headers.                                                                                                                               | 'Bearer ey...'                                                              |
| timeout      | Default 30. Timeout time.                                                                                                                                                            | 60                                                                          |
| user-agent   | User Agent header. Can also be set through headers.                                                                                                                                  | 'Mozilla: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101' |
| curl         | Add CURL options listed in the documentation.                                                                                                                                        | \[ 'CURLOPT\_COOKIESESSION' => true, 'CURLOPT\_CERTINFO' => true ]          |

CURL options can be found in [https://www.php.net/manual/es/function.curl-setopt.php](https://www.php.net/manual/es/function.curl-setopt.php)

Additionally there are two more options: **report** and **info**. If we use the option report = true, instead of the response, the request will return a full object with this structure:

```
{
   url: "https://....",
   method: "POST",
   response: { server response.. },
   code: 200,
   redirects: [...],
   error: "",
   time: {
      dns: 0.1,
      connecting: 0.1,
      redirecting: 0.1,
      total: 0.3
   }
}
```

This "report" can be extended adding CURL info options that we can find in PHP documentation:  [https://www.php.net/manual/es/function.curl-getinfo.php](https://www.php.net/manual/es/function.curl-getinfo.php).&#x20;

\
