---
description: Upload a file using a HTTP request with javascript
---

# Upload a file

Phyrus includes the Javascript method **uploadFile** to handle file uploads on client-side.

```
uploadFile({
    url: 'https://....',

    // Use one of these
    file: file,
    selector: '#fileInput'

    // Optional parameters
    maxSize: 15,   // mb
    filename: 'uploadedfile',  // name received in php
    data: { user: 236 },   // POST data
    method: 'POST',   // default POST
    timeout: 30,  // default 60
    headers: { ... }
    
}).then( response => {
    // do
}).catch(error => {

   if (error == 'maxSizeExceeded') {
      alert( 'File too big' );
   } else if (error == 'timeout') {
      alert( 'Time exceeded' );
   } else {
      alert( 'Unknown error' );
   }

});
```
