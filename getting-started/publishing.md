# Publishing

In order to upload your website to a server and get it working you'll only need a standard Web Server supporting Apache or Nginx to run PHP.

Then, make sure that the /public directory contains the last version of your compiled front-end project (run **php cli nuxt sync** if necessary).

Upload your directory to your server. You can **avoid** the /front-end directory, since it's only necessary during development, the server will just ignore it.

That's it! Your website should be ready to go!

### Continuous integration with GIT

If you configure your server to automatically download changes from your repository, the website should work without any additional configuration.

Front-end pages should already be compiled in the **/public** directory, which must be included in the repository. The **/front-end** directory will be downloaded into the server but ignored, because it's not needed to run the webiste on production, so just leave it there.
