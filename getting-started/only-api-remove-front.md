# Only API, remove front

Phyrus has the option to remove the front-end feature and leave only the back-end side to develop an API (or anything else but views). That's useful if the front-end is being developed by someone else as an independent project, so the back-end project doesn't need all of this front-end stuff around.

Right after starting your phyrus project, run this command in the root directory:

```
php phyrus front remove
```

This will do some changes in your project, such as deleting your **/front-end** directory, removing unnecessary files from **/public** and changing the configuration **project.only\_API** to true.

If you're developing an API there's an important point about doing this. When the project supports front-end, phyrus will assume that **any unknown route is a Front route**, so will load the Nuxt project. If the page does not exist, then **Nuxt will display the visual Not Found page**, but the response is **yet a 200 OK status**.

However, when front-end is removed, the back-end can safely assume that this route definitely does not exist **and then return a 404 Not Found status error**.

