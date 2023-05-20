# Scripts

You can create php scripts and run them in the terminal. The difference with running a simple php file, is that scripts have previously loaded the framework and your project, so all those functions and classes will be available.

To create scripts, just use the following command:

```
php phyrus script create <name>
```

This will just create a folder named "scripts" in your root directory, and inside a file named \<name>.php. That's something you could also do manually.

Then, write there your code, and run this line to execute your script:

```
php phyrus script <name>
```

{% hint style="info" %}
You don't need to include the extension (.php) when using the commands.
{% endhint %}
