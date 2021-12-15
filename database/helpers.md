---
description: Database helpers assist you with SQL Queries
---

# Helpers

Another option to use the database if you are not familiar with SQL is to use helpers. Helpers are methods in the **Database** class that will run the query for you, but making it easier:

```
$res = DB::select('users', [
    'where' => 'email = :email AND active = 1'
], [
    'email' => $email
]);

// Full example:
$res = DB::select('users', [
    'columns' => 'ID, username, email',
    'where' => 'active = 1',
    'offset' => 10,
    'limit' => 10
]);

// Single
$user = DB::row('users', [
    'where' => 'email = :email'
], [
    'email' => $email
]);

// Value
$email = DB::value('email', 'users', 'ID = :ID', ['ID' => $id]);

// Count
$num = DB::count('users');
$num = DB::count('users', 'createdAt > NOW() - INTERVAL 7 DAY');

// Delete
DB::delete('users', 'ID = :ID', ['ID' => $id]);

// Insert
DB::insert('users', [
    'email' => $email,
    'username' => $username
]);

// Update
DB::update('users', 'ID = :ID', [
    'email' => $newEmail
]);
```
