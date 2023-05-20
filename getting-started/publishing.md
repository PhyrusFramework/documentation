# Publishing

In order to upload your website to a server and get it working you'll only need a standard Web Server supporting Apache or Nginx to run PHP. That's it. You **don't need** a Node server, or special extensions or anything. Just a classic web server capable of running PHP >= 7.4, which is most of them.

Then, right before publishing, you must make sure that your **/public** directory contains the last version of your development done in **/front-end**. To do it, run this command in the root directory:

```
php phyrus front sync
```

This command will compile your front-end project and move the output to /public. Now just upload your directory to your server. **You can avoid the /front-end directory**, it's only necessary during development, **the server will just ignore it**.

{% hint style="danger" %}
If you changed your front-end framework to React or Angular, this command won't work for you. Instead, you'll have to manually run the build command, and copy-paste the output files to the /public directory.
{% endhint %}

That's it! Your website should be ready to go!

### Continuous integration with GIT

If you configure your server to automatically download changes from your repository, the website should work without any additional configuration.

Front-end pages should already be compiled in the **/public** directory, which **must be included in the repository**. The **/front-end** directory will be downloaded into the server but ignored, because it's not needed to run the webiste on production, so just leave it there or configure a process to delete that folder.
