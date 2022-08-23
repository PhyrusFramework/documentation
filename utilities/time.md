---
description: Parse and format time strings
---

# Time

The **Time** class is very helpful for parsing, formatting and operating on dates:

<pre class="language-php"><code class="lang-php"><strong>$t = new Time(); // now
</strong>// or
$t = Time::instance();

$t = new Time('2022-08-23 17:21:37');
$t = new Time('23-08-2022', 'd-m-Y');

$t = Time::fromTimestamp($number);

echo $t->format();  // By default Y-m-d H:i:s
echo $t->format('d m Y');

$t->second;
$t->minute;
$t->hour;
$t->day;
$t->month;
$t->year;
$t->timestamp;
$t->datetime; // Y-m-d H:i:s

$t->setDay($x);
$t->setMonth($x);
... second, hour, minute, year.

$dow = $t->dayOfWeek( $mondayFirst = true );
// Result ['position' => 1, 'day' => 'tuesday']</code></pre>

### Operate with time

The time object also allows you to operate on the date by adding or subtracting time:

```php
$t->add(3); // +3 days
$t->add(1, 'month');    // +1 month
$t->add(-4, 'minute');  // -4 minutes

$t->add(1, 'minute')->add(-1, 'day');
```

If you don't want to modify the original object you can make a copy:

```php
$t2 = $t1->copy()->add(3, 'day');
// $t1 and $t2 are different
```

### Time intervals

Two times can be compared with **isBefore**:

```php
if ($t1->isBefore($t2)) {
    // t1 is before t2
}

// Also with strings
if ($t->isBefore(datenow())
```

The difference between two times produces a **TimeInterval** object:

```php
$i = $t->since($t2);
$i = $t->until($t2); // inverse
$i = $t->toNow();    // until now

$i->invert();
```

Then, from the interval we can obtain each component independently or all together:

```php
// Invertval of 18 months:
// 2021-03-01 - 2022-09-01
$i->months;  // 18
$i->years;   // 1.5

// Each component separately
$i->total['years'] //  1 (2021 -> 2022)
$i->total['months'] //  6 (03 -> 09)
```
