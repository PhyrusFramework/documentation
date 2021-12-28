---
description: Combine PHP and Vue
---

# VueJS

Phyrus integrates VueJS to offer a powerful front-end solution.

### What is Vue?

Perhaps you don't know yet what Vue is. Vue is a Javascript framework for front-end web development. It's an alternative to other famous frameworks like **Angular** or **React**.

The important difference with these is that Angular or React require their own project structure, making harder to combine with other tools or frameworks.

Instead, Vue is more flexible and adaptable, allowing Phyrus to integrate it in a more comfortable way for the developer.

This framework, like the others, manages these features:

* Data-binding
* Reusable components
* Client-side rendering

Everything explained next belongs to Vue, and you can read it in its official documentation:

[https://vuejs.org/](https://vuejs.org)

### Data binding

Of all these features, **data-binding** is the most important. Data-binding is when the view automatically display and modify the value of variables, so we don't have to manage, for example, gathering the value of forms. An example:

```
// Javascript:
data: {
    username: ''
}

// HTML
<input v-model="username">
```

The input will automatically update the value of "username".

We can even use conditions and loops:

```
<div v-for="user of users">
    <div v-if="user.ID == myId">It's me!</div>
    <div v-else>{{ user.username }}</div>
</div>
```

### Components

A page with vue is made of **components**. A component can refer to a simple widget or the whole page. In any case, a component usually uses an object like this:

```
{
    // component variables
    data: {
        return {
            username: '',
            password: ''
        }
    },
    
    // component variables
    methods: {
        doLogin() {
            http.login(this.username, this.password);
        }
    },
    
    // When page starts
    created() {
    
    }
}

// HTML
<input v-model="username">
<input v-model="password">
<button @click="doLogin()">LOGIN</button>
```

This is only a small example, there are many other properties we can use.

Please, to learn more about Vue, read its documentation:

[https://vuejs.org/v2/guide/](https://vuejs.org/v2/guide/)
