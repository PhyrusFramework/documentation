# Zip

{% hint style="info" %}
This class requires the **zlib** php extension.
{% endhint %}

The Zip class lets you easily compress and uncompress files using zip files.

```php
// Create an empty zip
$zip = new Zip();

// Load existing zip
$zip = new Zip($path);
$zip = Zip::instance($path);

// Add files to zip
$zip->add( $filepath );

// Add a file to a folder inside the zip:
$zip->add( $image, '/resources/' );

// Add file and rename it:
$zip->add( $image, '/resources/', 'logo.png' );    
```

Besides using the path to a file, you can also directly add Data into the zip:

```php
$data = file_get_contents( $file );
$zip->addData( $data, 'image.jpg' );
```

You can add a full directory and all files inside:

```php
$zip->addDirectory( $path );
```

Finally the ZIP file can be saved to a file:

```php
$zip->save( $path );
```

An existing Zip can be extracred:

```php
Zip::instance( $path )->extract( __DIR__ ); 
// Extract in this directory
```
