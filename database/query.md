# Query

If you are not familiar with SQL and want an easier way to run queries, you can instead use the **Query** object:

```
$q = DB::query('table');
```

Now you can use the query object to read or write from database:

```
$users = $q
    ->where('active', 1)
    ->where('created_at', '<', 'NOW() - INTERVAL 1 YEAR')
    ->limit(10)
    ->offset($page)
    ->orderBy('created_at DESC')
    ->get();
    
$users = $q
    ->whereIn('ID', [123, 456, 789])
    ->whereNotIn('ID', [321, 654, 987])
    ->select('name', 'email') // columns
    ->get();
    
$count = $q->where('active', 1)->count();

$count = $q->groupBy('group_id')->count();
    
$user = $q->where('ID', 12)->first();

$q->where('ID', 12)->delete();

// New user
$q->set('name', $name)
    ->set('email', $email)
    ->set('password', $password)
    ->insert();

$q->where('ID', 12)
    ->set('name', 'user12')
    ->set('email', $email)
    ->update();
    
$r = DB::query('user_friends')
    ->join('users', 'user_friends.user_id = users.ID')
    ->select(
        'users.ID',
        'users.name',
        'user_friends.friend_id'
    )->get();
    
```
