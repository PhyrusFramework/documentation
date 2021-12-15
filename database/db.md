---
description: Make SQL queries
---

# DB

In your configuration file (/config.json) you have the credentials for your database. Then you can connect to your Database using the class **DB**.

```
DB::query('SELECT * FROM users');
```

However you can connect to another database creating a new **Database** object:

```
$db = new Database([
    'host' => 'localhost',
    'database' => 'name',
    'username' => 'user',
    'password' => 'pass
]);
$db->query('SELECT * FROM users');
```

### QueryResult

When you make a query to the database, the method will return a **DBQueryResult** object.

```
$res = DB::query("SELECT * FROM users");
$res->query;        // "SELECT * FROM users"
$res->error;        // null
$res->count;        // 34
$res->something;    // true (at least one result)
$res->result;       // array of results

foreach($res->result as $user) {
    $email = $user->email;
}
$res->first->email;
```

### Prepared statements

When using parameters inside of queries, you need to be **very careful**, since it may lead to a **SQL Injection attack**, especially if the parameter comes from user input.

Example: imagine you can search a user by email, so your users write in an \<input type="email">, and then you run:

```
SELECT * FROM users WHERE email = $email
```

Then, a user instead of an email, coud write "; DELETE FROM users;". The query would look like:

```
SELECT * FROM users WHERE email = ; DELETE FROM users;
```

The first query would fail, but the second would work, and all the users in your database would be gone. 😱

To protect you from these kind of attacks, queries use **prepared statements**. This basically means that you pass parameters aside:

```
DB::query("SELECT * FROM users WHERE email = :email", [
    'email' => $email
]);
```

The framework will place the parameters for you to prevent any kind of SQL injection.

{% hint style="info" %}
Be aware that the variable type is important. If the parameter is a string it will be treated as text and will be wrapped with quotes, but if the parameter is a number, it won't.
{% endhint %}
