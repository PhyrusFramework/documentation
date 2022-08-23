# Query

If you are not familiar with SQL and want an easier way to run queries, you can instead use the **Query** object:

```php
$q = DB::query('table');
```

Now you can use the query object to read or write from database:

<pre class="language-php"><code class="lang-php">$users = DB::query('users')
    ->where('active', 1)
    ->limit(10)
    ->offset($page)
    ->orderBy('created_at DESC')
    ->get();
    
$users = DB::query('users')
    ->whereIn('ID', [123, 456, 789])
    ->whereNotIn('ID', [321, 654, 987])
    ->select('name', 'email') // columns
    ->get();
    
$q = DB::query('users');
    
$count = $q->where('active', 1)->count();

$count = $q
    ->select('COUNT(*) as count')
<strong>    ->groupBy('group_id')
</strong><strong>    ->first()->count;
</strong>    
$user = $q->where('ID', 12)->first();

// Delete
$q->where('ID', 12)->delete();

// New user
$q->set('name', $name)
    ->set('email', $email)
    ->set('password', $password)
    ->insert();

// Update
$q->where('ID', 12)
    ->set('name', 'user12')
    ->set('email', $email)
    ->update();
    
$arr = DB::query('user_friends')
    ->join('users', 'user_friends.user_id = users.ID')
    ->select(
        'users.ID',
        'users.name',
        'user_friends.friend_id'
    )->get();
    </code></pre>

### Conditions

You can use a simple where condition:

```php
$q->where('status', 'active')
```

{% hint style="info" %}
Keep in mind that the value type matters. Strings are wrapped with quites, numbers are not.
{% endhint %}

Optionally, you can also use an operator:

```php
$q->where('price', '>=', 100)
$q->where('email', 'LIKE', '%gmail%');
$q->where('ID', 'IN', [1, 2, 3]);
$q->where('ID', 'NOT IN', [1, 2, 3]);
```

Sometimes you might need to write a SQL statement yourself, for that use **rawQuery**:

```php
$q->rawQuery('createdAt > NOW() - INTERVAL 1 MONTH');

// Parameters
$q->rawQuery('name = :name', [
    'name' => $name
]);
```

### OR

You can control AND and OR operators with the **or()** method:

```php
$query
    ->where('a', '1')
    ->where('b', '2')
    ->or()
    ->where('c', 3);
    
WHERE (a = '1' AND b = '2') OR (c = 3)
```

### Nested queries

Search **where in** or **where not in** another table:

```php
$users = DB::query('users')
    ->whereIn('ID', 
        DB::query('group_users')
            ->select('user_id')
            ->where('group_id', 3)
    )
    ->get();
    
SELECT * FROM users WHERE ID IN (SELECT user_id FROM group_users WHERE group_id = 3)
```

```php
DB::query('users')
    ->whereNotIn( ..., ... )
    ->get();
```
