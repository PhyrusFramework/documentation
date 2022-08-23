---
description: Manage files and folders from the code
---

# Files & Folders

The classes **File** and **Folder** let you easily manage your filesystem:

```php
// FILE
$file = new File($path);
$file = File::instance($path);

// Folder
$folder = new Folder($path);
$folder = Folder::instance($path);

if ($file->exists())
    $file->delete();
    
$name = $file->name( $withExtension? = true );
$ext = $file->extension();
$path = $file->folder();
$content = $file->content();
$file->copyTo($path, $overwrite? = false);
$file->moveTo($path, $overwrite? = false);

$file = new File($path);
$file->write('TEXT');
$file->prepend('START:');
$file->append(':END');
// result:  "START:TEXT:END"

$date = $file->modification_date();

$file->getMime(); // image/jpeg

$base64 = $file->toBase64();
$file = File::parseBase64($base64, $outputfilepath);

// FOLDER
$folder = new Folder($path);
$folder = Folder::instance($path);

if (!$folder->exists())
    $folder->create();
$folder->delete();

$files = $folder->subfiles();
$phpFiles = $folder->subfiles('php');
$directories = $folder->subfolders();
$contents = $folder->ls();  // List everything inside

// Delete everything inside
$folder->empty();

$folder->parent()->delete();

$folder->cd('../assets/css');  // Displace path

$folder->getFile('style.css')->delete();

$folder->copyTo($path);
$folder->moveTo($newPath);

$folder->merge($anotherFolder);
```

{% hint style="info" %}
In order to execute some of this actions the system may require write permissions.
{% endhint %}
