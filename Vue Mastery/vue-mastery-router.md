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

#### Dynamic Routes

- router/index.js

```js
const routes = [
  ...
  {
    path: '/user/:username',
    name: 'user',
    component: User
  }
]
```

> `:username`을 동적 세그먼트(dynamic segment)라고 한다.

- views/User.vue

```html
<template>
  <div class="user">
    <h1>This is a page for {{ $route.params.username }}</h1>
  </div>
</template>
```

> `localhost:8080/user/song`에 `This is a page for song`이 표시된다.

<br>

<br>

#### Using Props for Routes

- router/index.js

```js
const routes = [
  ...
  {
    path: '/user/:username',
    name: 'user',
    component: User,
    props: true
  }
]
```

<br>

- views/User.vue

```html
<template>
  <div class="user">
    <h1>{{ username }}</h1>
  </div>
</template>

<script>
  export default {
    props: ['username']
  }
</script>
```

> `localhost:8080/user/song`에 `song`이 표시된다.

<br>

<br>

#### History mode

- router/index.js

```js
...

const router = new VueRouter({
  mode: 'history',  // <----
  base: process.env.BASE_URL,
  routes
})

export default router
```

<br>

<br>

#### Handling 404s

- components/NotFound.vue

```html
<template>
  <h1>Not Found</h1>
</template>
```

- router/index.js

```js
...
import NotFound from '@/components/NotFound';

const routes = [
  ...
  {
    path: '*',
    component: NotFound
  }
]
```

> router 설정이 되어 있지 않은 주소로 이동하면 `Not Found`가 표시된다.

<br>

<br>