# Cronjobs

The **Cron** class lets you list, create and delete automatic scheduled tasks.

{% hint style="info" %}
**Cron** will only work in a Linux or similar servers accepting the '**crontab**' command.
{% endhint %}

You can create a task in two different ways:

```
$task = new Cron( 'curl -s http://mysite.com' );
$task->create();

$task = new Cron();
$task->setInterval('0 * * * *');
$task->action('curl -m 120 -s https://mysite.com');
$task->create();
```

In the second case, we can use **helpers** to simplify the code:

```
$task = new Cron();
$task->every(1, 'hour');
$task->action('https://mysite.com', 'curl');
$task->create();
```

Helpers make it easier to configurate the interval:

```
$task->every(3, 'day');
$task->every(30, 'minute');
$task->every(1, 'month');
$task->every('monday');

$task->at(3, 'hour');
$task->at(19, 'hour');  // at 19:00
$task->at(20, 'day');  // at day 20 of each month
$task->at('monday');  // same as 'every monday'
```

You can even combine multiple helpers:

```
$task->every(2, 'month')
    ->at(20, 'day')
    ->at(13, 'hour');
// Every 2 months, on 20th at 13:00
```

The action may have a second parameter for **curl** or **php**:

```
$task->action('curl -m 120 -s https://mysite.com');
$task->action( 'https://mysite.com', 'curl' );

$task->action('php -q echo "Hello"');
$task->action( 'echo "Hello"', 'php' );
```

Finally you use **create**() to add this cronjob to the system. Each combination of **interval + command** can only be declared once in the system. You can list all created cronjobs with:

```
$list = Cron::list();  // Returns array of Cron
```

You can check if a Cron exists and then obtain it:

```
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

```
Cron::select( $command )->delete();
Cron::deleteAll();
```
