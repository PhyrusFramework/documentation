# DBBuilder

The **DBBuilder** class lets you create tables in a very fast and easy way:

```
$builder = new DBBuilder();

$builder->name('posts')  // Table 'posts'

    ->column('ID', 'BIGINT')
        ->autoIncrement()

    ->column('url', 'TEXT')
        ->unique()
    
    ->column('title') // by default VARCHAR(255)
    
    ->column('description', 'TEXT')
        ->nullable()
        
    ->column('author', 'BIGINT')
        ->references('users(ID)')
    
    ->execute();
```
