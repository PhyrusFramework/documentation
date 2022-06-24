---
description: Uploading files through HTTP Requests
---

# File uploads

To upload a file the client will make a request to the server sending the file as data.

The server will receive that file. In PHP this file is received in the global $\_FILES variable, however with Phyrus you can just use the same **RequestData** object:

```
$req = new RequestData();

if (!$req->hasFiles()) // at least 1
    response_die('bad');

if (!$req->hasFile('photo')) // specific file named 'photo'
    response_die('bad');

// or directly
$req->requireFile('photo');

$photo = $req->getFile('photo');
$photo->tmp;  // Path to uploaded temporary file
$photo->name; // 'my_photo.jpg'
$photo->type; // 'image/jpeg'
$photo->extension;  // 'jpg' (if name includes it)

```

**$file->tmp** is the path to the uploaded file. This file will be deleted when the request ends, so you must copy it to another location to save it. You can do that with the **File** class:

```
File::instance($file->tmp)->copyTo($newpath);
```

{% hint style="info" %}
If the file is an image, perhaps you want to resize it first, or generate thumbnails. You can do that with the **Image** class, check it in the section **Utilities**.
{% endhint %}
