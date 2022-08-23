# ORM Serialization

All ORMs are automatically json serializable. They can be converted to json:

```php
$json = json_encode($product);

// With phyrus:
$json = JSON::stringify($product);
```

The same method **jsonSerialize** can be used to convert the ORM to an array:

```php
$array = $product->jsonSerialize();
```

As ORMs are serializable, arrays are also automatically serialized:

```php
$products = Product::find();
$jsonArray = JSON::stringify($products);
```

### Hide columns

ORMs use its **Definition** method (where columns are listed) to build the object. So by default all columns will appear in the JSON serialization. But this can be disabled for specific columns:

```php
class User extends ORM {

    function Definition(DBBuilder $b) {
    
        $b->name('users')
            ->column(...)
            
            ->column('password')
            ->notSerializable();
    
    }

}
```

### Customize serialization

Sometimes the serialization of an object won't match the columns of the table. Perhaps you need to join columns from other tables or add a computed value to the JSON object. To do so, just override the jsonSerilize method:

```php
class User extends ORM {

    function jsonSerialize() {
        $data = parent::jsonSerialize();
        
        // Customize here
        $data['custom'] = 123;
        
        return $data;
    }

}
```

### Serialize relations

When listing the columns we can define a foreign key:

```php
function Definition(DBBuilder $b) {
    
    $b->name('users')
        ->column('group_id')
        ->references('groups(ID)'); // Foreign key
}

// Serialization:
{
    ID: 23,
    name: 'User name',
    group_id: 3
}
```

By default this column will appear in the serialization just as a simple value (group\_id). However, we can tell the ORM to include this relation and serialize also the related object by indicating the class of the related:

```php
function Definition(DBBuilder $b) {
    
    $b->name('users')
        ->column('group_id')
        ->references('groups(ID)')
        ->serializeRelation('Group'); // Class name
}

// Serialization:
{
    ID: 23,
    name: 'User name',
    group: {
        ID: 98,
        name: 'Group name'
    }
}
```

{% hint style="info" %}
Phyrus uses a **serialization tree** to avoid infinite loops or creating a huge JSON string. So an object which has already been serialized in a parent level won't be serialized again.

Imagine that A references B, B references C and C references A. That serialization would never end. Instead. C won't serialize A again, will just display A\_id.
{% endhint %}

