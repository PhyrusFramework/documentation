# Cronjobs

The **Cron** class lets you list, create and delete automatic scheduled tasks from the code.

{% hint style="info" %}
**Cron** will only work in a Linux or similar servers accepting the '**crontab**' command.
{% endhint %}

A task can be created in two different ways:

```php
// Use the full command in the constructor
$task = new Cron( '0 2 * * * curl -s http://mysite.com' );
$task->create();

// Or build the command step by step
$task = new Cron();
$task->setInterval('0 * * * *');
$task->action('curl -m 120 -s https://mysite.com');
$task->create();
```

If you are not sure about how to set intervals using the **cron interval format**, use this alternative:

```php
$task->every(1, 'hour');
$task->every(3, 'day');
$task->every(30, 'minute');
$task->every(1, 'month');
$task->every('monday');

$task->at(3, 'hour');    // at 03:00
$task->at(19, 'hour');   // at 19:00
$task->at(20, 'day');    // at day 20 of each month
$task->at('monday');     // same as 'every monday'
```

You can even combine multiple helpers:

```php
$task->every(2, 'month')
    ->at(20, 'day')
    ->at(13, 'hour');
// Every 2 months, on 20th at 13:00
```

The action may have a second parameter for **curl** or **php**:

```php
$task->action('curl -m 120 -s https://mysite.com');
// is equal to:
$task->action( 'https://mysite.com', 'curl' );

$task->action('php -q echo "Hello"');
// is equal to:
$task->action( 'echo "Hello"', 'php' );
```

Finally you use **create**() to add this cronjob to the system. Each combination of **interval + command** can only be declared **once** in the system. You can check first all created cronjobs with:

```php
$list = Cron::list();  // Returns array of Cron objects
```

You can check if a Cron exists and then obtain it:

```php
$command = '0 * * * * curl https://site.com';

if ( Cron::exists( $command ) ) {
    $cron = Cron::select( $command );
    $cron->delete();
} else {
    $cron = new Cron($command);
    $cron->create();
}
```

You can delete one specific cron using the object or delete them all with a static method:

```php
Cron::select( $command )->delete();
Cron::deleteAll();
```
