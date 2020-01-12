#### Vue Router Basics

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

- router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '@/views/Home'
import About from '@/views/About'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: Home
  },
  {
    path: '/about',
    name: 'about',
    component: About
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
```

- Home.vue

```html
<template>
  <div class="home">
    <h1>This is an home page</h1>
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

<br>

<br>

#### Using Named Routes

- App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'home' }">Home</router-link>
      <router-link :to="{ name: 'about' }">About</router-link>
    </div>
    <router-view />
  </div>
</template>
```

<br>

<br>

#### Redirect

- router/index.js

```js
const routes = [
  {
    path: '/',
    name: 'home',
    component: Home
  },
  {
    path: '/about',
    name: 'about',
    component: About
  },
  {
    path: '/about-us',
    redirect: { name: 'about' }
  }
]
```

<br>

<br>

#### Alias

- router/index.js

```js
const routes = [
  {
    path: '/',
    name: 'home',
    component: Home
  },
  {
    path: '/about',
    name: 'about',
    component: About
  },
  {
    path: '/about-us',
    name: 'about',
    component: About,
    alias: '/about'
  }
]
```

<br>

<br>