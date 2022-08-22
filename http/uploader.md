# Uploader

The **Uploader** class is a helper to handle:

* Obtain uploaded files
* Decide where to store them
* Control access to them
* Generate image sizes

```
// If there's at least one file, take the first:
$file = Uploader::getFile();

// If there are multiple, specify which:
$file = Upload::getFile('photo');
```

### Public or Private files

Files can be **public** or **private**. If they are public, they can be accessed via URL from the website by any user, if they are private they are stored in the server but are **not accessible via web**.

{% hint style="info" %}
Private files can still be accessed via endpoints of the API, which can check for authentication before displaying the files.

Public files are always accessible via direct URL to the file.
{% endhint %}

### Store directory

By default, public files will be stored in **/public/uploads** and private files will be stored in **/uploads**. Nevertheless, this is a configuration that can be customized, found in **config/project.yaml**:

```
uploads:
  publicDir: "uploads"
  privateDir: "uploads"
```

Change it as you like. However keep in mind that the public directory starts from the **/public** directory, while the private starts from the root.

### Store the file

Here's an example of saving an uploaded file:

```
$file = Uploader::getFile();

$file->savePrivate('documents/doc.pdf');
// Saved in /uploads/documents/doc.pdf

$file->savePublic('documents/doc.pdf');
// Saved in /public/uploads/documents/doc.pdf
// url: https://mysite.com/uploads/documents/doc.pdf
```

If the file already existed, you need to confirm you want to **overwrite** it (delete the previous file) by adding **true** as second parameter:

```
Uploader::savePublic('doc.pdf', true);
```

{% hint style="info" %}
If you don't want to think how to name the uploaded file, you can just use the **GUID()** method to generate a unique identifier.
{% endhint %}

```
Uploader::savePublic( GUID() . '.pdf');
```

### Save images

Images are a bit more tricky, because ideally a good Back-End should save different and compressed sizes of the same image. Normally these sizes are **small**, **medium**, **large**.

To handle this, in your configuration (**/config/project.yaml**) the sizes are defined:

```
uploads:
  ...
  images:
    dir: "images"
    sizes:
      small: 300
      medium: 550
      large: 900
      hd: 1500
```

{% hint style="info" %}
Images saved with this method are **always public**, so the directory is relative to **/public/uploads.**
{% endhint %}

These sizes are the **limit** of the image size, width or height, keeping the aspect ratio. This means that if the **small** limit is **300**, and the uploaded image is 600x400, the image will be resized to 300x200.

Then, the **Uploader** will handle this resizing and compressing process for you, just use **saveImage** instead of savePublic. The image will be stored with a unique name generated with **GUID()**:

```
$imageName = Uploader::getFile()
    ->saveImage()
    ->name;    // xxxxxxxxx.jpg

// Generates the following files:
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

### Get path to the stored file

To get the path to the stored file use:

```
$uploader->relativePath();
$uploader->absolutePath();

// For images
$uploader->getSize('medium');  // relative
```
