---
description: Easily generate a database backup
---

# Backup

The database object has a method named **Backup** that lets you export the database into a .sql file:

```php
DB::backup( __DIR__ . '/backup.sql' );

DB::backup( $path, [
    'charset' => 'utf-8',   // Default utf-8
    'zip' => true,  // Compress? Default false
    'batchSize' => 500,
    'tables' => ['a', 'b', 'c'] // By default all
]);
```
