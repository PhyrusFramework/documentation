---
description: Object Relational Model
---

# ORM

The framework includes an **ORM** class. An ORM (**Object Relational Model**) is a class that represents an entity of the database (for example a User).

Through the ORM object we can automatically modify the database without making any queries, just by using the object:

```
$user = new User();
$user->email = $email;
$user->username = $username;
$user->setPassword($pass);
$user->save();  // Insert into DB

$id = $user->ID;
$user = new User($id);

$user->email = $newEmail;
$user->save();        // Update
// or
$user->save('email'); // Update only email column

$user->delete();

User::deleteWhere('active = 0');
```

### Database columns

The ORM class **must** declare a **Definition** method which defines the columns of the database table. This method receives a [**DBBuilder** ](../database/create-tables.md)object that you need to use to define the name and columns of the table:

```
class Product extends ORM {

    function Definition(DBBuilder $builder) {
        
        $builder->table('products')
        
        ->column('name')
        ->column('stock', 'INTEGER')
        ->column('price', 'FLOAT(12, 3)');
    }

}

$product = new Product();
$product->name = 'Guitar',
$product->stock = 23;
$product->price = 149.99;
$product->save();
```

### The constructor

An ORM object can be initialized:

* as new (nothing)
* by ID
* by a query row

```
$product = new Product();    // New ID = 0
$product = new Product(34);  // Load ID = 34

$query = DB::run('SELECT * FROM products WHERE ID = 34');
$product = new Product($query->first);
```

After saving, the ID is updated with the new ID:

```
$product = new Product();    // ID = 0
$product->save();            // Now ID = 34
```

### Manage table

{% hint style="warning" %}
The ORM class automatically adds two columns to the table, one named **ID (INT AUTO\_INCREMENT)** at the beginning and another named **createdAt(DATETIME)** at the end.
{% endhint %}

While in **development mode** (project.yaml -> development\_mode: true), the **ORM Table will be created automatically** whenever you try to use the model.

Otherwise, you can force the creation of the table by using:

```
$product->CheckTable();
// or
Product::CreateTable();
```

The name of the table can be obtained from an instance or statically:

```
$table= $product->getTable();
$table = Product::Table();
```

You can drop the table with:

```
Product::dropTable();
```

You can delete multiple rows using a condition with **deleteWhere**:

```
Product::deleteWhere('active = 0');
Product::deleteWhere('name = :name', ['name' => $name]);
```
