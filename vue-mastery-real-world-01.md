#### Creating Vue project

```bash
$ cd Desktop
$ vue create vue-real-world
```

<br>

#### Serving Vue project

```bash
$ cd vue-real-world
$ npm run serve
```

<br>

#### How the App is Loaded

- main.js

```js
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";

Vue.config.productionTip = false;

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount("#app");
```

<br>

#### package.json

- All of our application's dependencies are tracked inside our `package.json` file.

```json
"dependencies": {
  "vue": "^2.6.10",
  "vue-router": "^3.1.3",
  "vuex": "^3.1.2"
}
```

<br>

#### Router

- Home.vue

```html
<template>
  <div class="home">
    <h1>This is a home page</h1>
  </div>
</template>
```

- About.vue

```html
<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>
```

- router/index.js

```js
import Vue from "vue";
import VueRouter from "vue-router";
import Home from "../views/Home.vue";

Vue.use(VueRouter);

const routes = [
  {
    path: "/",
    name: "home",
    component: Home
  },
  {
    path: "/about",
    name: "about",
    component: () => import("../views/About.vue")
  }
];

const router = new VueRouter({
  routes
});

export default router;
```

- App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
  }
  
  #nav {
    padding: 30px;
  }
  
  #nav a {
    font-weight: bold;
    color: #2c3e50;
  }
  
  #nav a.router-link-exact-active {
    color: #42b983;
  }
</style>
```

- We can see that we can navigate between these two different routes.

<br>

<br>