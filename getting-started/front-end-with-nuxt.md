# Front-End with Nuxt

During development you will work with **Nuxt** ([https://nuxtjs.org](https://nuxtjs.org/)), a framework of **Vue**. To learn about Nuxt, you should read its documentation, but basically this is how it works:

The Nuxt project is located in the **/front-end** directory. Go there, run **npm install** to install dependencies, and then run **npm run dev** to start your website at [http://localhost:3000](http://localhost:3000).

Nuxt is a **front-end framework**, which means that, unlike using other PHP frameworks like Laravel or Symfony, you can't directly query the database and use the result to render HTML. Instead, you **must develop an API** in the Back-End to pass data to Front-End.

This is done on purpose. Working with **SSR** (Server-Side rendering, which means that the Back-End renders the view directly as it happens with Laravel) has been proved to be a bad practice and awfully scalable. Phyrus forces you to work with an API, which in addition to being a better practice, will make it easier in the future to build another application using the same API, or renew the aspect of your website without modifying the business logic.

### Phyrus-Nuxt NPM Package

The phyrus front-end project comes with a NPM package named **phyrus-nuxt**, which is a library to help developers with the front-end part, same as Phyrus PHP helps you with the back-end.

The documentation for this package is currently still in development. Soon will be added here.

### Development and production

While in development, if you access **http://localhost**, you won't see your changes, you'll need to run the Nuxt local server (as explained before) and use **http://localhost:3000**.

Once you're finished (or if you want to update your production files) run this command in your **root folder** to compile your front-end proejct and update the content in the /public directory:

```
php cli nuxt sync
```

This will compile your nuxt project (**npm run generate**) and move the produced static files to **/public**, so it displays when accessing the website.
