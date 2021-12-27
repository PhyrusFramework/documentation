---
description: Search ORM objects in the database
---

# Search ORMs

Both simple ORMs and Advanced ORMs have methods to easily search and find entries in the database.

All ORMs have the methods **find** (list) and **findOne** (item):

```
$users = User::find(); // find all
$products = Product::find('stock > 0'); // WHERE

$user = User::findOne('email = :email', [
    'email' => $email
]);

$users = User::find('1 ORDER BY email DESC');
```

This is the **best way** to find an existing row, **rather** than using the constructor:

```
$user = new User(34);
// Incorrect, because user ID 34 could not exist.

$user = User::findOne('ID = 34');
user == null ?
```

### Advanced ORM search

In the case of AdvancedORM, additionally we have other methods to find and sort by meta values or translations:

```
$products = Product::byMeta('active');
$products = Product::byMeta('active', '1');
$products = Product::byMeta('category', ['electronics', 'furniture']);

// Like search
$products = Product::byMeta('category', '%electronic%');

$products = Product::byTranslation('name', '%fridge%');
$products = Product::byTranslation('name', '%fridge%', 'en');
$products = Product::byTranslation('category', 
                ['Fridge', 'Refrigerador'], ['en', 'es']);
                
$products = Product::sortByMeta('position', [
    'asNumber' => true,
    'sort' => 'ASC LIMIT 10'
]);

$products = Product::sortByTranslation('name', [
    'locale' => 'en'
]);
```
