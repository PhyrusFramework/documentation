---
description: Manage files and folders from the code
---

# Files\&Folders

Phyrus offers you two classes: **File** and **Folder**. These will let you easily manage your files from the code:

```
$file = new File($path);
$file = File::instance($path);

$folder = new Folder($path);
$folder = Folder::instance($path);

if ($file->exists())
    $file->delete();
    
$name = $file->name( $withExtension? = true );
$ext = $file->extension();
$path = $file->folder();
$content = $file->content();
```
