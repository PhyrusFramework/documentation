# React or Angular

The framework brings Nuxt as its Front-End framework by default. But Phyrus is perfectly capable of working with any Front-End framework, such as React or Angular, and now you will learn how to change your front-end framework if you desire to.

However, for now Phyrus will only officially support Nuxt because the project brings a npm package (**phyrus-nuxt**) which helps the developer with front-end stuff, such as UI Components, making API calls, uploading files, etc, so this package would need to be replicated for every other supported framework. Nevertheless, if you don't mind losing this feature, feel free to switch to React or Angular, or any other.

#### Switch framework

Just delete everything inside the /front-end directory, and place there your front-end project with your desired framework. Now, develop your website just like you would normally do, and then build your project.

The project will be built into a directory named **/dist, /www, /build**, whatever depending on the framework. Now just copy all of those files, and paste them into the **/public** directory. That's it! Now you can publish your project, read the [publishing](publishing.md) chapter for more information.

The Phyrus CLI has a command to automatize this process of copying and pasting the built project into the /public directory, with Nuxt. You should override this CLI or built your own to copy this feature with your framework, read the chapter about [CLI ](broken-reference)for more information.

