---
description: Search ORM objects in the database
---

# Search ORMs

Both simple ORMs and Advanced ORMs have methods to easily search and find entries in the database.

All ORMs have the methods **find** (list), **findOne** (item) and **findID** (item):

```php
$users = User::find(); // find all
$products = Product::find('stock > 0'); // WHERE

$user = User::findOne('email = :email AND active = 1', [
    'email' => $email
]);

$users = User::find('1 ORDER BY email DESC');

$user = User::findID(23);  // Find user with ID 23
```

{% hint style="info" %}
The **findID** method autoamtically converts the parameter to a number, so you can pass a string.
{% endhint %}

Another option is tu use the [Query](../database/query.md) object:

```php
$users = User::query()
        ->where('status', 'active')
        ->orderBy('username DESC')
        ->limit(10)
        ->offset($offset)
        ->get();
        
$user = User::query()
        ->where('email', $email)
        ->first();
```

### Advanced ORM search

In the case of the **AdvancedORM**, additionally there are other methods to find and sort elements by their meta values or translations:

```php
// Products with meta 'active' and any value
$products = Product::byMeta(['active']);

// Products with meta 'active' = '1'
$products = Product::byMeta(['active' => '1']);

// Products with active = '1' AND category in ('electronics', 'furniture')
$products = Product::byMeta([
    'active' => '1',
    'category' => ['electronics', 'furniture']
]);

// Products where active = '0' OR category = 'hidden'
$products = Product::byMeta(
[
    'active' => '0'
], 
[
    'category' => 'hidden'
]);

// LIKE search
$products = Product::byMeta([
    'category' => '%electronic%'
]);

// Products where the "name" translation contains "fridge"
$products = Product::byTranslation('name', '%fridge%');

// Products where the "name" translation in english contains "fridge"
$products = Product::byTranslation('name', '%fridge%', 'en');

// Products where:
// the "category" translation is "Fridge" or "Refrigerador"
// in english or spanish
$products = Product::byTranslation('category', 
                ['Fridge', 'Refrigerador'], ['en', 'es']);
                
// Products sorted by a meta value
$products = Product::sortByMeta('position', [
    'asNumber' => true,
    'sort' => 'ASC LIMIT 10'
]);

// Products sorted by name in english
$products = Product::sortByTranslation('name', [
    'locale' => 'en'
]);
```

If you need more complex queries, then you should consider using the **Query** object:

```php
$users = User::query()
    ->whereIn( 'ID', DB::query('users_meta')
                        ->where('meta_key', 'verified')
                        ->where('meta_value', '1') )
    ->or(function($q) {
        $q->whereIn( 'ID', DB::query('users_translations')
                        ->where('locale', 'en')
                        ->where('name', 'name')
                        ->where('value', 'The name')
       ->or(function($q) {
           $q->rawWhere('phone IS NOT NULL')
       });
    })
    ->get();
```
