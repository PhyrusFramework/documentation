---
description: List, create or delete cronjobs from the terminal
---

# CLI Cron

The cron command allows you to list, create and delete crons from the terminal.

{% hint style="info" %}
Beware that cronjobs only work on linux servers, not windows
{% endhint %}

```
php phyrus cron list

php phyrus cron delete --all
php phyrus cron delete --index=2  // From the list
php phyrus cron delete --command="0 2 * * * /bin/sh backup.sh"

php phyrus cron create "0 2 * * * /bin/sh backup.sh"
php phyrus cron create "/bin/sh backup.sh" --interval="0 2 * * *"
```
