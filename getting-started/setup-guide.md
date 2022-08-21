---
description: Start a new project with Phyrus
---

# Setup guide

To start a new Phyrus project with Composer, just run this line in your terminal:

```
composer create-project phyrus/project MyProjectName
```

A new folder will be created with your project. Now:

* To run your website/API use a local web server (e.g Apache or Nginx) on the /public directory.
* To develop your front-end use NPM and Nuxt in the /front-end directory. Go to the /front-end directory with your terminal and run **npm install**.

#### Connect a database

Connecting a database **is not required** to use Phyrus, you can develop a website without a connected database. However, to configure it, add the credentials in the configuration file **/config/database.yaml**

#### **Run your website locally**

You can either go into the /front-end directory and run:

```
npm run dev
```

Or run this command in the root directory:

```
php phyrus front run
```

Both will run your website in http://localhost:3000. Here you will only see your **front-end**, you will be able to develop your website pages using **Nuxt**, read Nuxt documentation if you're not familiar with it: [https://nuxtjs.org/docs/get-started/installation](https://nuxtjs.org/docs/get-started/installation)&#x20;

Your website will need an API to fetch data, you will do that with the back-end side. To develop the API, you need a local server (using Apache or Nginx, or using tools like Xampp, Mamp, etc) pointing at the **/public** directory in your project.

Once you've got this, keep reading the documentation to learn how to use the framework.
