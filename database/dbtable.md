---
description: Table ORM
---

# DBTable

The **DBTable** object lets you manage database tables:

```
$t= DB::table('users');

$t = DBTable::create([
    'name' => 'users',
    'columns' => [
        [
            'name' => 'username',
            'type' => 'VARCHAR(255)',
            'notnull' => true
        ],
        ...
    ]
]);
```

Then we can operate using this object:

```
$t->drop();

$t->empty(); // Remove everything inside

if ($t->exists())

$t->addColumn([
    'name' => 'email',
    'type' => 'VARCHAR(255)',
    'notnull' => true,
    'after' => 'name'
]);

$t->addColumn([
    'name' => 'parent_id',
    'type' => 'BIGINT',
    'foreign' => 'users(ID)'
]);

$t->dropColumn('email');
```
