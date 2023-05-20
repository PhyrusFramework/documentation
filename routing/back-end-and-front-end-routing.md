# Back-End & Front-End routing

This is a **full-stack** framework, which means that the same web server, the same hosting and the same domain **can host actually two different projects**, a back-end project written in **PHP** and a front-end project written in **Javascript** (**Typescript**).

So, how does it work? Your Back-End (PHP) will define routes (API Endpoints). Requests will trigger the **index.php** file in **/public**. This will call the framework to detect whether the route being accessed **is a Back-End route or not**. If it is, it will execute the endpoint in PHP and display its output (JSON, XML, whatever). If it's not, it will just output the content of the **index.html** file located in **/public**, which belongs to Nuxt, so the front-end application will be loaded.

So, basically, anything that is not an back-end route, loads the Nuxt project. The Front-End framework will handle displaying a 404 Not Found page when the route does not exist.

From this point on, routing is managed differently in Back-End and Front-End. For Front, read Nuxt's documentation, for Back-End keep reading here.
