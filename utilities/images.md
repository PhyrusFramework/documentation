# Images

{% hint style="info" %}
This class requires the **gd** php extension.
{% endhint %}

The **Image** class will let you easily manipulate, compress and save images. A common use is resizing images.

```php
$image = new Image($file);
$image = Image::instance($file);

echo 'Width: ' . $image->width();
echo 'Height: ' . $image->height();

// Limit image size
$image->cap( 560 );  // Limit size to 560px width or height
$image->cap( 800, 600 ); // Limit size to 800, 600

$copy = $image->copy();  // Generate a copy
$image->copy()->cap( 300 );

$str = $image->base64();
$image = Image::fromBase64( $str );

$image->save( $path, $format? = 'jpg', $quality = 100 );
$image->save( $file );
$image->save( $file, 'png' );
$image->save( $file, 'jpg', 85 );

// Resize an uploaded image:
Image::instance( $upload->tmp )->cap( 800, 600 )->save( $path );
```

If images get rotated when you upload them, use this method to correct the orientation:

```php
$image->correctOrientation();
```

### Compose images

This class also lets you compose images by merging multiple images, writing text on them, etc.

```php
// Print an image on another image
$img->append( $img2, [ 50, 50 ]);
```

**$img** and **$img2** are both **Image** objects. **$img2** has a size, perhaps you need to **resize** it before appending it. Then **$img2** is appended to **$img1** at position \[50px, 50px].

Now write text on the image:

```php
$img->writeText( 'Hello!', [
    'color' => [$r, $g, $b],
    'size' => 12,
    'font' => $pathToFontFile
]);
```
