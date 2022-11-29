---
description: Make SQL queries
---

# Database

The **DATABASE** class holds the connection to a database. By default, the project has only one database with the credentials specified in the configuration file (database.yaml).

&#x20;This database can be used by the shortcut **DB**:

```php
$res = DB::run('SELECT * FROM users');
```

However you can connect to another database creating a new **Database** object:

```php
$db = new DATABASE([
    'host' => 'localhost',
    'database' => 'name',
    'username' => 'user',
    'password' => 'pass
]);

$res = $db->run('SELECT * FROM users');
```

### QueryResult

When you run a query, the method will return a **DBQueryResult** object.

```php
$res = DB::run("SELECT * FROM users");
$res->query;        // "SELECT * FROM users"
$res->error;        // null
$res->count;        // 34
$res->something;    // true (if at least one result)
$res->result;       // array of results
$res->first;        // first result

foreach($res->result as $user) {
    $email = $user->email;
}
$res->first->email;
```

### Prepared statements

When using parameters inside of queries, you need to be **very careful**, since it might lead to a **SQL Injection attack**, especially if the parameter comes from user input.

Example: imagine your front-end allows to search a user by email, so your users write in an \<input type="email">, and then you run:

```sql
SELECT * FROM users WHERE email = $email
```

Then, instead of an email, a user decides to write _"; DELETE FROM users;"_. The final query would look like this:

~~SELECT \* FROM users WHERE email = ;~~ DELETE FROM users;

The first query would fail, but the second would work, and all the users in your database would be gone. 😱 To protect you from these kind of attacks, queries use **prepared statements**. This basically means that you pass parameters aside:

```php
DB::query("SELECT * FROM users WHERE email = :email", [
    'email' => $email
]);
```

The framework will place the parameters for you to prevent any kind of SQL injection.

{% hint style="info" %}
Be aware that the variable type is important. If the parameter is a string it will be treated as text and will be wrapped with quotes, but if the parameter is a number, it won't.
{% endhint %}

### Using insecure strings

Using prepared statements will convert html special characters before writing them, but this can be a problem if you willingly wanted to insert HTML in your database.

To write HTML, you need to use an **InsecureString** object:

```php
DB::query("INSERT INTO htmlBlocks (body) VALUES (:body)", [
    'body' => new InsecureString('<p>HTML body</p>');
]);
```

However, your HTML body might contain a \<script> tag inserted by the user with malicious intentions, which would lead to a **XSS Attack.** To prevent this attack, you must **remove script tags** from the body:

```php
$str = new InsecureString('Code: <script>alert('error!')</script>');
$str->removeScriptTags();

echo $str->getString();
// Output: 'Code: '

DB::query("INSERT INTO htmlBlocks (body) VALUES (:body)", [
    'body' => $str
]);
```
