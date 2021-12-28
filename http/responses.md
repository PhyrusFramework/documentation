---
description: HTTP Responses
---

# Responses

By default, any page (except for 404 Not found) will automatically return a response 200 OK.

However, especially if developing an API, you will want to return specific response codes and messages (400, 401, 403, 404, 405...).

For that, Phyrus helps you with this task so you don't have to remember every code and what it means. You can just use the method **response**:

```
response('bad');
response('forbidden');
response('unauthorized');
response('not-found');
response('ok');
response('method-not-allowed');
```

Optionally, you can add a second parameter which will be the body of the response:

```
response('bad', 'Name field is missing');
```

If the parameter is an array, it will be automatically parsed to **JSON**:

```
response('bad', [
    'message' => 'Name field is missing'
]);
```

If you want to finalize the execution right after the response, you could just use **die**(), but you can also use the method **response\_die**(), which is the same:

```
response_die('bad');
// Program ends here
```

### List of response codes

| Name                   | Code | Meaning                                                                                            |
| ---------------------- | ---- | -------------------------------------------------------------------------------------------------- |
| ok                     | 200  | All ok.                                                                                            |
| created                | 201  | Content created successfully.                                                                      |
| accepted               | 202  | Request accepted, but action not made yet.                                                         |
| development            | 203  | Request successfull, but this action is still in development.                                      |
| no-content             | 204  | Success without response body.                                                                     |
| reset-view             | 205  | Success, but client has to reload to see the change.                                               |
| partial-content        | 206  | The response is only part of the whole response (ex: downloads).                                   |
| multiple-choice        | 300  | This request has multiple possible responses, so the client cannot know which one received.        |
| moved-permanently      | 301  | Permanent redirection.                                                                             |
| found                  | 302  | URL is valid, but content still has to change soon.                                                |
| see-other              | 303  | The server asks you to visit another URL instead of this one.                                      |
| not-modified           | 304  | Used for cache purposes.                                                                           |
| bad                    | 400  | The request is not valid.                                                                          |
| unauthorized           | 401  | Authentication failed.                                                                             |
| forbidden              | 403  | This user does not have access to this route.                                                      |
| not-found              | 404  | This page does not exist.                                                                          |
| method-not-allowed     | 405  | The method used for this request is not allowed.                                                   |
| not-acceptable         | 406  | After analyzing the request body, data does not comply with the expected format.                   |
| proxy-unauthorized     | 407  | Proxy is not authorized.                                                                           |
| timeout                | 408  | The request timed out.                                                                             |
| conflict               | 409  | There is a conflict between the state of the server, and what the client is requesting.            |
| gone                   | 410  | The requested resource has been deleted.                                                           |
| condition-failed       | 412  | The server requires conditions (headers, method, data) that the request does not fullfill.         |
| unsupported-media-type | 415  | The sent media file format is not accepted.                                                        |
| error                  | 500  | Code error.                                                                                        |
| not-implemented        | 501  | This functionality is not implemented yet.                                                         |
| bad-gateway            | 502  | The request cannot be completed because the server got error from a third service.                 |
| unavailable            | 503  | This path is not available now, but should be fixed soon.                                          |
| gateway-timeout        | 504  | The request cannot be completed because the server made another request to a third that timed out. |
