# Translations

```php
$post->setTranslation('title', 'en', 'This is the title');
$post->setTranslation('title', 'es', 'Este es el título');
$title = $post->getTranslation('title', 'en');
```

Sometimes translations could be missing in some languages but exist in others. In that case, you can use **getAnyTranslation**:

```
$title = $post->getAnyTranslation('title', ['es', 'en', '*']);

1. Get translation in spanish (es)
2. If not exists -> in english (en)
3- If not exists -> in any available (*)
```
