---
description: Folders and files you will find in the project
---

# Project Structure

Phyrus places all the framework stuff that you don't need to see or touch in the **framework composer package** directory (located in **/vendor/phyrus/framework**), so the project directory is cleaner, lighter and free of unnecessary files for you.

Phyrus is a full-stack framework composed of two halfs: **back-end** and **front-end**. **Back-End** works with PHP and with it you can develop an API, manage file uploads, the database, models, business logic and all of that. Front-End uses **Nuxt**, which is a **Vue** framework: [https://nuxtjs.org](https://nuxtjs.org/).

As you can see, there are these two directories inside the project folder: **front-end**, and **back-end**.

Finally, the **/public** folder must be configured as the **root** of your web server, and will be the one who handles the browser request to either take the browser to a PHP endpoint or a Vue page.

Keep reading the documentation to understand it all.
