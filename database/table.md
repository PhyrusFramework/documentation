---
description: Table ORM
---

# Table

The **DBTable** object helps you with managing database tables:

<pre class="language-php"><code class="lang-php">$t= DB::table('users');

<strong>$t->drop();
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

$t->dropColumn('email');
</code></pre>
