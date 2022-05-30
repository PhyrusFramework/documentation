# Back-End & Front-End routing

This is a **full-stack** framework, which means that the same web server, the same hosting and the same domain **can host actually two different projects**, a back-end project written in **PHP** and a front-end project written in **Javascript** (Vue).

So how does it work? Easy. Your Back-End (PHP) will declare routes (API Endpoints). When a user accesses the website, that triggers the **index.php** file in the **/public** directory. This will call the framework, which will decide whether the route being accessed **is an endpoint of the API or not**. If it is, it will execute the endpoint in PHP and display its output (JSON, XML, etc). If it's not, it will just output the content of the **index.html** file located also in **/public**, which belongs to Nuxt, so the front-end application will be triggered.

So, basically, anything that is not an API endpoint, is a web HTML page.

From here, routing is managed differently in back-end and Front-End. For front-end, read Nuxt's documentation, for Back-End keep reading here.
