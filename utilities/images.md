# Images

{% hint style="info" %}
This class requires the **gd** php extension.
{% endhint %}

The Image class will let you easily manipulate, compress and save images. A common use is resizing images on file upload.

```
$image = new Image($file);
$image = Image::instance($file);

$image->width();
$image->height();

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

Image::instance( $uploaded )->cap( 800, 600 )->save( $path );
```

If images get rotated when you upload them, use this method to correct the orientation:

```
$image->correctOrientation();
```
