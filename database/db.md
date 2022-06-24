---
description: Make SQL queries
---

# DB

Using the class **DB** you can access and use the database configured in your YAML configuration file:

```
DB::run('SELECT * FROM users');
```

However you can connect to another database creating a new **Database** object:

```
$db = new Database([
    'host' => 'localhost',
    'database' => 'name',
    'username' => 'user',
    'password' => 'pass
]);
$db->run('SELECT * FROM users');
```

### QueryResult

When you run a query, the method will return a **DBQueryResult** object.

```
$res = DB::run("SELECT * FROM users");
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

When using parameters inside of queries, you need to be **very careful**, since it might lead to a **SQL Injection attack**, especially if the parameter comes from user input.

Example: imagine your front-end allows to search a user by email, so your users write in an \<input type="email">, and then you run:

```
SELECT * FROM users WHERE email = $email
```

Then, instead of an email, a user decided to write _"; DELETE FROM users;"_. The final query would look like this:

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

### Using insecure strings

Using prepared statements will convert html special characters before writing them in the database, but this can be a problem if you willingly wanted to insert HTML in your database.

To write HTML, you need to use an **InsecureString** object:

```
DB::query("INSERT INTO htmlBlocks (body) VALUES (:body)", [
    'body' => new InsecureString('<p>HTML body</p>');
]);
```

However, your HTML body might contain a \<script> tag inserted by the user with malicious intentions, which would lead to a **XSS Attack**, to prevent this attack, you must **remove script tags** from the body:

```
$str = new InsecureString('Code: <script>alert('error!')</script>');
$str->removeScriptTags();

echo $str->getString();
// Output: 'Code: '
```
