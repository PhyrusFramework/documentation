---
description: Parse and format time strings
---

# Time

The time class allows you to parse datetimes and format them:

```
new Time(); // now
new Time($datetime, $format? = 'Y-m-d H:i:s');
$t = Time::instance($datetime);
$t = Time::fromTimestamp($number);

echo $t->format($format);

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

$t->dayOfWeek( $mondayFirst = true );
// Result ['position' => 1, 'day' => 'tuesday']
```

### Operate with time

The time object also allows you to operate on the date by adding or subtracting time:

```
$t->add(3); // +3 days
$t->add(1, 'month');    // +1 month
$t->add(-4, 'minute');  // -4 minutes

$t->add(1, 'minute')->add(-1, 'day');
```

If you don't want to modify the original object you can make a copy:

```
$t2 = $t->copy()->add(3, 'day');
// $t and $t2 are different
```

### Time intervals

Two times can be compared with **isBefore**:

```
if ($t1->isBefore($t2))

// Also with strings
if ($t->isBefore(datenow())
```

The difference between two times produces a **TimeInterval** object:

```
$i = $t->since($t2);
$i = $t->until($t2); // inverse
$i = $t->toNow();    // until now

$i->invert();
```

Then, from the interval we can obtain each component independently or all together:

```
// Invertval of 18 months:
// 2021-03-01 - 2022-09-01
$i->months;  // 18
$i->years;   // 1.5

$total = $i->total;
$total['years'] => 1  (2021 -> 2022)
$total['months'] => 6  (03 -> 09)
```
