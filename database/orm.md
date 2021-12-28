---
description: Object Relational Model
---

# ORM

The framework includes an **ORM** class. An ORM (**Object Relational Model**) is a class that represents an entity of the database (for example User).

Through the ORM we can automatically modify the database without making queries, just by modifying the object. Example:

```
$user = new User();
$user->email = $email;
$user->username = $username;
$user->setPassword($pass);
$user->save();  // Inserted into DB

$id = $user->ID;
$user = new User($id);

$user->email = $newEmail;
$user->save();    // Updated

$user->delete();

User::deleteWhere('active = 0');
```

An ORM class must extend the **ORM** class and include a method named **Definition** with a table definition as seen in **DBGen:**

```
class Product extends ORM {

    function Definition() {
        return [
            'name' => 'products',
            'columns' => [
                 [
                     'name' => 'name',
                     'type' => 'VARCHAR(100)'
                 ],
                 [
                     'name' => 'stock',
                     'type' => 'INTEGER'
                 ],
                 [
                     'name' => 'price',
                     'type' => 'FLOAT(12, 3)'
                 ]
            ]
        ];
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
* by query row

```
$product = new Product();  // New ID = 0
$product = new Product(34);  // Load ID = 34

$query = DB::query('SELECT * FROM products WHERE ID = 34');
$product = new Product($query->first);
```

After saving, the ID updates with the inserted ID:

```
$product = new Product();    // ID = 0
$product->save();            // Now ID = 34
```

### Manage table

{% hint style="warning" %}
The ORM class automatically includes two columns in the table, one named **ID (INT AUTO\_INCREMENT)** at the beginning, and another named **createdAt(DATETIME)** at the end.
{% endhint %}

While in **development mode** (config.json -> development\_mode: true), the **ORM Table will be created automatically** whenever you try to use the model.

Otherwise, you can force the creation of the table by using:

```
$product->CheckTable();
```

The name of the table can be obtained from an instance or statically:

```
$name = $product->getTable();
$name = Product::Table();
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

### ORM to Array or JSON

Any ORM can be converted to array with the method **toArray**:

```
$arr = $product->toArray();
$json = JSON::stringify($arr);
```

If we have an array of ORM objects, we can use the **arr** method that converts an array to an **Arr** object, and then use the **map** method which acts like in Javascript:

```
$products = Product::find();

$array = arr($products)->map(function($product) {
    return $product->toArray();
})->toArray();

$json = JSON::stringify($array);
```
