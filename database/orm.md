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

{% hint style="warning" %}
The ORM class automatically includes two columns in the table, one named **ID (INT AUTO\_INCREMENT)** at the beginning, and another named **createdAt(DATETIME)** at the end.
{% endhint %}

While in **development mode** (config.json -> development\_mode: true), the **ORM Table will be created automatically** whenever you try to use the model.

Otherwise, you can force the creation of the table by using:

```
$product->CheckTable();
```
