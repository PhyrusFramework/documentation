# Tests

Tests are automatic tasks that validate that your code, routes, API or functionalities are working correctly as expected. For example, tests can be used to validate that all endpoints in an API return the correct response, and are not crashing with a 500 error after making changes.

Tests can be run manually by terminal or also automated with a cronjob and log its activity into a file.

To create a test run:

```
php phyrus test create <name>
```

This will create a file inside a directory named **/tests** in the root directory. This files defines a new class extending the **Test** class. Right below **creates an instance of this class** to enable the test.

```php
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
php phyrus test run
php phyrus test run <name>
```

### Display and log errors

A test will do some checks and then, if everything goes right, the terminal will display a success message:

```
TEST SUCCESSFUL
```

If, instead, there are errors, they must be printed to inform the developer. Inside the test, this can be done with the method **addError**():

```php
lass MyTest extends Test { 

    function run() {
    
        if (!checkSomething()) {
            $this->addError($message);
        }
    
    }
}
```

```php
addError($message, $detail?, $file?, $line?)
```

Then, the terminal will list the found errors like this:

```
TEST FAILED
Found errors:
    - Message: this is the message. File (line)
    - ...
    - ...
```

### Verbose

Once you found an error, sometimes it is hard to debug and find exactly what's happening. When you just run tests, you want the output to be straight and brief, so just tell me if the test succeeded or not. But when debugging, then you need more information about what's happening in the test.

For this purpose, the test has a method **addLog**:

```php
$this->addLog($msg)
```

By default these messages **won't be displayed**, but they will by using the flag **--verbose**:

```
php phyrus test run --verbose
```

### Check that routes return 200 OK

You can check that your API routes still work with a single line:

```php
$this->check200('/login');
```

This method **will automatically add an error** if fails. However, this method will just run a simple GET HTTP Request. When testing an API, you will probably need more control over the Request (method, data, headers, etc). You can do that with a second parameter:

```php
$this->check200('/api/signup', [
    'method' => 'POST',
    'data' => [...],
    'headers' => [...]
]);
```

{% hint style="info" %}
If this is not enough, you can always use the Phyrus HTTP Client to make the request yourself and log the error manually.
{% endhint %}

### Log results into a file

If you decide to automate tests to be executed by themselves, then you will need to know what happened while you were out.

Use the flag **--log** to automatically create a text file **inside the tests folder**, where the result will be logged (the same you see in the terminal).

```
php phyrus test run --log
```

### Alternative database

A common problem when running tests is that some of them require operations that write or delete data from the database. That's a problem in production, of course, you can't play with the real database 😱. It can even be a problem in development, because you don't want to mess with your playground.

To solve this problem, Phyrus gives you the option to have an additional secondary database to be used only when running tests. To configure it, set the credentials of this database in the configuration file  **database.yaml -> forTests**:

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

From now on you can freely create, update and delete data form the database when running tests, and that will be done in this second database.
