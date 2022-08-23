---
description: Uploading files through HTTP Requests
---

# File uploads

To upload a file, first the client will make a request to the server sending the file. That part is not explained here. The server will receive that file. In PHP this file is listed in the global $\_FILES variable, but Phyrus lets you use the same **RequestData** object that is used for POST data:

```php
$req = new RequestData();

// Check if at least 1 file received
if (!$req->hasFiles())
    ApiResponse::badRequest();

// specific file named 'photo'
if (!$req->hasFile('photo'))
    ApiResponse::badRequest();

// or directly
$req->requireFile('photo');

$photo = $req->getFile('photo');
$photo->tmp;  // Path to temporary file
$photo->name; // 'my_photo.jpg'
$photo->type; // 'image/jpeg'
$photo->extension;  // 'jpg' (if name includes it)

```

**$file->tmp** is the path to the uploaded file. This file will be deleted when the request ends, so you must copy it to another location to save it. You can do that with the **File** class:

```php
File::instance($file->tmp)->copyTo($newpath);
```

{% hint style="info" %}
If the file is an image, perhaps you want to resize it or generate thumbnails. You can do that with the [**Image**](../utilities/images.md) **** class, check it in the section **Utilities**.
{% endhint %}
