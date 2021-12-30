# Tests

Tests are tasks that validate that the website/API is working correctly.

For example, tests can be used to validate that all endpoints in an API return the correct response, and are not crashing with an error 500 after making changes.

Tests can be run manually by terminal, but also automated with a cronjob and log errors into a file or send an email to warn the developer about it.

To create tests, create a directory /tests in the root. There add php files and declare classes extending the **Test** class. Then **create an instance** to enable the test.

```
class MyTest extends Test { 

    function run() { }

}
new MyTest();
```

{% hint style="info" %}
You can comment the last line (new MyTest()) to disable the test.
{% endhint %}

Then you can run all tests or a specific one from cli:

```
php cli test run
php cli test run <name>
```

### Generate a test by terminal

Using the CLI command **generate**, you can generate a new test file automatically:

```
php cli generate test MyTest
```

### Display and log errors

A test will do checks and then, if everything goes right (success!), the terminal will display a green message:

```
TEST SUCCESSFUL
```

If, instead, there are errors, they must be logged. Inside the test, this can be done with the method **addError**():

```
lass MyTest extends Test { 

    function run() {
    
        if (!checkSomething()) {
            $this->addError($message);
        }
    
    }
}
```

```
addError($message, $detail?, $file?, $line?)
```

Then, the terminal will list the found errors:

```
TEST FAILED
Found errors:
    - ...
    - ...
```

### Verbose

You have the option to give additional information. During the test, use the method **addLog**:

```
$this->addLog($msg)
```

By default these messages won't be shown, but they will display by using the flag --verbose

```
php cli test run --verbose
```

### Check response 200 OK

You can check that your routes still work with a single line:

```
$this->check200('/login');
```

This method **will automatically add the error** if fails, you don't need to do that. However, the method returns a boolean if you need to know if it was successful.

When testing an API, you will probably need more control over the HTTP Request (method, data, headers, etc). You can do that with a second parameter:

```
$this->check200('/api/signup', [
    'method' => 'POST',
    'data' => [...],
    'headers' => [...]
]);
```

### Log results

If you decide to automate tests to be executed by themselves, then you will need to know what happened while you were out.

Use the flag --log to automatically create a text file in the tests folder, where the result will be logged (the same you see in the terminal).

```
php cli test run --log
```

### Alternative database

A common problem when running tests is that some of them require operations that write or delete data from the database. That's a problem in production, of course, you can't play with the database 😱

To solve this problem, Phyrus gives you the option to have an additional secondary database to be used when running tests. To configure it, use the object **tests.alternativeDatabase** in the configuration file:

```
"tests": {
    "alternativeDatabase": {
        "type": "mysql",
        "host": "localhost",
        "database": "name",
        "username": "root",
        "password": ""
    }
}
```

When running tests and using the class DB, this database will be used instead of the production database:

```
DB::query('...');
```
