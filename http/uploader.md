# Uploader

The **Uploader** class is an Uploads manager to help you store the uploaded files.

```
// Detect automatically any file in the data
$file = Uploader::getFile();

// Specific file:
$file = Upload::getFile('photo');
```

Files can be **public** or **private**. If they are public, that means they can be accessed via URL from the website, if they are private they are stored in the server but are not accessible.

Public files will be stored in **/public/uploads**

Private files will be stored in **/uploads**

```
$file = Uploader::getFile();
if (!$file) return;

$file->savePrivate('documents/doc.pdf');
// Saved in /uploads/documents/doc.pdf

$file->savePublic('documents/doc.pdf');
// Saved in /public/uploads/documents/doc.pdf
// url: https://mysite.com/uploads/documents/doc.pdf
```

If the file already existed, you need to confirm you want to overwrite it (delete previous file):

```
Uploader::savePublic('doc.pdf', true);
```

{% hint style="info" %}
If you don't want to think how to name the uploaded file, you can just use the **GUID()** method to generate a unique identifier.
{% endhint %}

### Change the uploads directory name

Perhaps you'd like to change the name of the directory where uploads are stored. This is actually a configuration value you can find in **/config/project.yaml**:

```
uploads:
  publicDir: "uploads"
  privateDir: "uploads"
```

### Save images

Images are a bit more tricky, because ideally a good server should save different and compressed sizes of the same image. Normally these sizes are **small**, **medium**, **large** and **original**.

To handle this, in your configuration files (**/config/project.yaml**) the sizes are defined:

```
uploads:
  publicDir: "uploads"
  privateDir: "uploads"
  images:
    dir: "images"
    sizes:
      small: 300
      medium: 550
      large: 900
      hd: 1500
```

These sizes are the limit of the image size, width or height, keeping the aspect ration. This means: if the **small** limit is **300**, and the uploaded image is 600x400, the image will be resized to 300x200.

Then, the **Uploader** will handle this optimization process for you, just use **saveImage** instead of savePublic. The image will be stored with a unique name generated with **GUID()**:

```
$imageName = Uploader::getFile()
    ->saveImage()
    ->name;    // xxxxxxxxx.jpg

// Generated the following files:
/public/uploads/images/small/xxxxxxxxx.jpg
/public/uploads/images/medium/xxxxxxxxx.jpg
/public/uploads/images/large/xxxxxxxxx.jpg
/public/uploads/images/hd/xxxxxxxxx.jpg

// Public URLs
/uploads/images/medium/xxxxxxxxx.jpg
```

{% hint style="info" %}
The uploader will automatically detect if the image is jpg or png
{% endhint %}
