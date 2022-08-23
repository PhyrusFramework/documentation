---
description: Table ORM
---

# Table

The **DBTable** object helps you with managing database tables:

<pre><code>$t= DB::table('users');
<strong>
</strong><strong>$t->drop();
</strong>
$t->empty(); // Remove everything inside

if ($t->exists()) { }

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

$t->dropColumn('email');</code></pre>
