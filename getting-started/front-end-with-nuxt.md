# Front-End with Nuxt

During development you will work with **Nuxt** ([https://nuxtjs.org](https://nuxtjs.org/)), a framework of **Vue**. To learn about it you should read its documentation, but basically this is how it works:

The Nuxt project is located in the **/front-end** directory. Go there, run **npm install** to install dependencies, and then run **npm run dev** to start your website at [http://localhost:3000](http://localhost:3000).

Nuxt is a **front-end framework**, which means that, unlike using other PHP frameworks like Laravel or Symfony, you can't directly query the database and render the view. You **have to develop an API** in the Back-End, and use it in your Front-End.

This is done intentionally, since working with SSR (Server-Side rendering, which means that the Back-End renders the view directly) has been proved to be a bad practice and awfully scalable. This framework forces you to work with an API, which in addition to being a better practice, makes it easier to develop another app using the same API in the future if you need it.

### Development and production

While in development, if you access just **http://localhost**, you won't see your changes, you'll need to use **http://localhost:3000**.

Once you're finished (or if you want to update your production status) run this command in your **root folder**:

```
php cli nuxt sync
```

This will compile your nuxt project (**npm run generate**) and move the produced static files to **/public**, so you see it when accessing your website.
