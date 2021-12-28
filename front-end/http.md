---
description: HTTP client Javascript
---

# HTTP

The Javascript **http** object lets you make HTTP requests to any URL from a self or a third API.

```
http.get(url).then(response => ...);
http.post(url, {...});
http.put(url, {...});
http.delete(url, {...});
http.patch(url, {...});

http.<method>(url, options?);

// or generic
http.request({
    url: xxx,
    method: 'POST',
    ....
});

// ALL OPTIONS
http.request({
    url: 'https://...',
    method: 'POST',
    format: 'json',
    data: { ... },
    headers: {...}
})
.then(response => {...})
.catch(error => {...});
```
