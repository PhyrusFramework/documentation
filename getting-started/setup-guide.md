# Start project

To start a new Phyrus project with Composer, run this command:

```
composer create-project phyrus/project MyProjectName
```

A new folder will be created with your project. Now:

* To run your website/API use a local web server (e.g Apache or Nginx) on the /public directory.
* To develop your front-end use NPM and Nuxt in the /front-end directory. Go to the /front-end directory with your terminal and run **npm install**.

#### API Only

If you're developing only an API and you're not going to need the Front-End support, run this command to clean all front-end unnecessary stuff from the project:

```
php phyrus front remove
```

#### Connect a database

Connecting a database **is not required** to use Phyrus, you can develop a project without a connected database. However, to add one, add the credentials in the configuration file **/config/database.yaml**

#### **Run your website locally**

You can either go into the /front-end directory and run:

```
npm run dev
```

Or run this command in the root directory:

```
php phyrus front run
```

Both will run your website in **http://localhost:3000**. Here you will only see your **front-end**, you will be able to develop your website pages using **Nuxt**, read Nuxt documentation if you're not familiar with it: [https://nuxtjs.org/docs/get-started/installation](https://nuxtjs.org/docs/get-started/installation)&#x20;

Your website will need an API to fetch data, you will do that with the back-end side. To develop the API, you need a local server (using Apache or Nginx, or using tools like Xampp, Mamp, etc) pointing at the **/public** directory in your project.

Once you've got this, keep reading the documentation to learn how to use the framework.
