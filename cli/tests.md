# Tests

Tests are tasks that validate automatically that your routes or functionalities are working correctly.

For example, tests can be used to validate that all endpoints in an API return the correct response, and are not crashing with an error 500 after making changes.

Tests can be run manually by terminal, but also automated with a cronjob to be logged into a file or sent via email to warn the developers about it.

To create a test run:

```
php cli test create <name>
```

This will create a file inside a directory named **/tests** in the root directory, extending the **Test** class. Then **create an instance** to enable the test.

```
class MyTest extends Test { 

    function run() { }

}

new MyTest();
```

{% hint style="info" %}
You can comment the last line to disable the test.
{% endhint %}

Then you can run all tests at once or only a specific one from cli:

```
php cli test run
php cli test run <name>
```

### Display and log errors

A test will do some checks and then, if everything goes right, the terminal will display a success message:

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
    - Message: this is the detail. File(line)
    - ...
    - ...
```

### Verbose

You have the option to log additional information. During the test, use the method **addLog**:

```
$this->addLog($msg)
```

By default these messages **won't be shown**, but they will display by using the flag **--verbose**:

```
php cli test run --verbose
```

### Check routes return 200 OK

You can check that your API routes still work with a single line:

```
$this->check200('/login');
```

This method **will automatically add an error** if fails. However, the method only returns a boolean. When testing an API, you will probably need more control over the HTTP Request (method, data, headers, etc). You can do that with a second parameter:

```
$this->check200('/api/signup', [
    'method' => 'POST',
    'data' => [...],
    'headers' => [...]
]);
```

### Log results

If you decide to automate tests to be executed by themselves, then you will need to know what happened while you were out.

Use the flag **--log** to automatically create a text file in the tests folder, where the result will be logged (the same you see in the terminal).

```
php cli test run --log
```

### Alternative database

A common problem when running tests is that some of them require operations that write or delete data from the database. That's a problem in production, of course, you can't play with the database 😱

To solve this problem, Phyrus gives you the option to have an additional secondary database to be used when running tests. To configure it, set the credentials in the configuration file  **database.yaml -> forTests**:

```
type: mysql
host: localhost
database: prodDB
username: root
password: root

forTests:
    type: mysql
    host: localhost
    database: testsDB
    username: root
    password: root
```

From now on you can freely create, update and delete data form the database when running tests, and that will be stored in this second database.
