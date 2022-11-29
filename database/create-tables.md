---
description: Generate tables from specification
---

# Create tables

Phyrus has a method **create\_tables** that allows you to store the definition of one or multiple tables in a JSON or PHP (array) file and then easily re-create those tables with a single line. Example:

```
// JSON
{
   "users": [
        {
            "name": "ID",
            "type": "BIGINT",
            "notnull": true,
            "primary": true
        },
        {
           "name": "username",
           "type": "VARCHAR(300)",
           "notnull": true,
           "unique": true
        },
        {
           "name": "partner",
           "type": "BIGINT",
           "foreign": "users(ID)"
        }
   ]
}

// PHP
[
   'users' => [
      [
         'name' => 'ID',
         'type' => 'BIGINT',
         'notnull' => true,
         'primary' => true
      ],
      ...
   ]
]
```

```php
$json = JSON::fromFile($file);

DB::create_tables($json);             // Create all
DB::create_table($name, $columns);    // Create single
```

### DBBuilder

Another alternative is using the **DBBuilder** class. This lets you create tables in a much more visual and simple way:

```php
$builder = new DBBuilder();

$builder->name('posts')  // Table 'posts'

    ->column('ID', 'BIGINT')
        ->autoIncrement()
        ->primary()

    ->column('url', 'TEXT')
        ->unique()
    
    ->column('title') // by default VARCHAR(255)
    
    ->column('description', 'TEXT')
        ->nullable()
        
    ->column('author', 'BIGINT')
        ->references('users(ID)') // foreign key
    
    ->execute();
```
