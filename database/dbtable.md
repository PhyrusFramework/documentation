---
description: Table ORM
---

# DBTable

Another option to interact with the database is to use the class **DBTable**. Each instance is created for a table of the database:

```
$users = new DBTable('users');
// or also
$users = DBTable::instance('users');
```

Then we can operate using this object:

```
$users->select('*', [
    'email' => ['=', $email]
]);

$users->select('email', [
    'email' => ['LIKE', '%@gmail.com']
]);

$users->insert([
    'email' => $email,
    'username' => $username
]);

$users->update([
    'active' => '0'    // set active = 0
], [
    'last_activity' => [ '<', $date ]
    // where last_activity < $date
]);

$users->delete([
    'ID' => [ 'IN', $ids ]
]);
```

### Edit table

The DBTable class also allows you to modify, create or drop tables.

```
$table = DBTable::create([
   'name' => 'products',
   'columns' => [
      [
         'name' => 'ID',
         'type' => 'BIGINT',
         'primary' => true,
         'notnull' => true,
         'auto_increment' => true
      ],
      [
          'name' => 'price',
          'type' => 'FLOAT(12, 3)'
      ]
   ]
]);

$table->addColumn([
   'name' => 'code',
   'type' => 'VARCHAR(100)',
   'unique' => true,
   'after' => 'ID'
]);

$table->dropColumn('price');

$table->drop();
```
