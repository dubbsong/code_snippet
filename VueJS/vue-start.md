#### Structure

```bash
src
  ├─ assets
  │   └─ logo.png
  ├─ components
  │   ├─ Header.vue
  │   ├─ Footer.vue
  │   └─ popup
  │       ├─ CommonLoading.vue
  │       ├─ CommonAlert.vue
  │       └─ Congrats.vue
  ├─ plugins
  │   └─ vuetify.js
  ├─ router
  │   └─ index.js
  ├─ store
  │   └─ index.js
  ├─ views
  │   ├─ Home.vue
  │   ├─ About.vue
  │   ├─ Dashboard.vue
  │   ├─ Login.vue
  │   ├─ Signup.vue
  │   └─ NotFound.vue
  ├─ App.vue
  └─ main.js
```

<br>

#### Create Vue project

```bash
$ cd Desktop
$ vue create vue-start
```

> \> Select `Manually select features`
>
> \> Check `Babel`, `Router`, `Vuex`, `CSS Pre-processors`, `Linter / Formatter`
>
> \> Use history mode for router? `Y`
>
> \> Select `Sass/SCSS (with node-sass)`
>
> \> Select `ESLint + Prettier`
>
> \> Select `Lint on save`
>
> \> Select `In dedicated config files`
>
> \> Save this as a preset for future projects? `N`

<br>

#### Run server

```bash
$ cd vue-start
$ code .
$ yarn serve
```

> App running at `http://localhost:8080/`

<br>

#### Add Vuetify

```bash
$ vue add vuetify
```

> Select `Default (recommended)`

<br>

#### Set starting code

- App.vue

```html
<template>
  <!-- Home or About or NotFound -->
  <router-view />
</template>
```

- views/Home.vue

```html
<template>
  <div id="home">
    <h4>Home</h4>
  </div>
</template>
```

- views/About.vue

```html
<template>
  <div id="about">
    <h4>About</h4>
  </div>
</template>
```

- views/NotFound.vue

```html
<template>
  <div id="not-found">
    <h4>404 Not Found</h4>
  </div>
</template>
```

- router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '@/views/Home'
import About from '@/views/About'
import NotFound from '@/views/NotFound'

Vue.use(VueRouter);

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
    path: '*',
    component: NotFound
  }
];

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
});

export default router;
```

> `http://localhost:8080/`: Home
>
> `http://localhost:8080/about`: About
>
> `http://localhost:8080/anything`: 404 Not Found

<br>

#### Write README.md

```markdown
# Vue Start
<br>

### Install dependencies
​```
yarn install
​```
<br>

### Run server
​```
yarn serve
​```
<br>

### Check on browser
> http://localhost:8080
<br>
```

<br>

#### Create new repo

1. Click `New` button on Github
2. Type `vue-start` in Repository name
3. Click `Create repository`

<br>

#### Connect Vue project

```bash
$ cd vue-start
$ git init
$ git add .
$ git commit -m 'Set starting code'
$ git remote add origin git@github.com:id/project.git
$ git push -u origin master
```

> Check repo

<br>

#### Optimizing editor

- Create file

```bash
$ cd vue-start
$ touch .prettierrc.js
```

- \.prettierrc.js

```js
module.exports = {
  singleQuote: true,
  semi: false
};
```

> You don't have to use `"` and `;` in JS file.

<br>

#### Break point

```bash
$ cd vue-start
$ git add .
$ git commit -m 'Optimizing editor'
$ git push origin master
```

<br>

#### Set Header \& Footer

- Create files

```bash
$ cd src
$ cd components
$ touch Header.vue
$ touch Footer.vue
```

- App.vue

```html
<template>
  <v-app id="app">
    <!-- Header -->
    <Header />
    
    <!-- Main -->
    <div id="main" role="main">
      <router-view />
    </div>
    
    <!-- Footer -->
    <Footer />
  </v-app>
</template>

<script>
  import Header from '@/components/Header'
  import Footer from '@/components/Footer'
  
  export default {
    components: {
      Header,
      Footer
    }
  }
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Ubuntu:400,500,700&display=swap');
  $bg-white: #ffffff;
  $font-white: #ffffff;
  
  #app {
    background-color: $bg-white;
    font-family: 'Ubuntu', sans-serif;
    text-align: center;
    
    * {
      box-sizing: border-box;
      padding: 0;
      margin: 0;
    }
    
    #main {
      margin-top: 80px;
    }
    
    section {
      width: 100%;
    }
    
    .content {
      width: 1200px;
      margin: 0 auto;
    }
    
    h1 {
      font-size: 56px;
    }
    
    h2 {
      font-size: 48px;
    }
    
    h3 {
      font-size: 32px;
    }
    
    h4 {
      font-size: 24px;
    }
    
    h5 {
      font-size: 20px;
    }
    
    h6 {
      font-size: 18px;
    }
    
    p {
      font-size: 16px;
    }
    
    a {
      text-decoration: none;
      color: $font-white;
    }
    
    strong {
      font-size: 12px;
      font-weight: normal;
    }
    
    em {
      font-size: 12px;
      font-style: normal;
    }
    
    li {
      list-style: none;
    }
  }
</style>
```

- Header.vue

```html
<template>
  <div id="header">
    <!-- left -->
    <ul>
      <li>
        <router-link to="/">
          <img src="@/assets/logo.png" alt="logo" />
        </router-link>
      </li>
      <li>
        <router-link to="/">Home</router-link>
      </li>
      <li>
        <router-link to="/about">About</router-link>
      </li>
      <li>
        <router-link to="/dashboard">Dashboard</router-link>
      </li>
    </ul>
    
    <!-- right -->
    <ul>
      <li>
        <router-link to="/login">Login</router-link>
      </li>
      <li>
        <router-link to="/signup">Signup</router-link>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
  $bg-blue: #26324d;
  $font-white: #ffffff;
  $font-active: #4fc08d;
  
  #header {
    background-color: $bg-blue;
    color: $font-white;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 4%;
    box-shadow: 4px 0 16px rgba(0, 0, 0, 0.04);
    z-index: 10;
    
    ul {
      display: flex;
      align-items: center;
      
      li {
        margin-right: 16px;
        
        a {
          display: flex;
          align-items: center;
          
          &.router-link-exact-active {
            color: $font-active;
          }
          
          img {
            width: 160px;
          }
        }
      }
    }
  }
</style>
```

- Footer.vue

```html
<template>
  <div id="footer">
    <p>© OMB</p>
  </div>
</template>

<style lang="scss" scoped>
  $bg-blue: #26324d;
  $font-white: #ffffff;
  
  #footer {
    background-color: $bg-blue;
    color: $font-white;
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 80px;
    display: flex;
    align-items: center;
    padding: 0 4%;
  }
</style>
```

<br>

#### Break point

```bash
$ cd vue-start
$ git add .
$ git commit -m 'Set Header and Footer'
$ git push origin master
```

<br>

#### Set pages

- Create files

```bash
$ cd src
$ cd views
$ touch Dashboard.vue
$ touch Login.vue
$ touch Signup.vue
```

- Home.vue

```html
<template>
  <div id="home">
    <div class="content">
      <h4>Home</h4>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  #home {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
  }
</style>
```

- About.vue

```html
<template>
  <div id="about">
    <div class="content">
      <h4>About</h4>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  #about {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
  }
</style>
```

- Dashboard.vue

```html
<template>
  <div id="dashboard">
    <div class="content">
      <h4>Dashboard</h4>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  #dashboard {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
  }
</style>
```

- Login.vue

```html
<template>
  <div id="login">
    <div class="content">
      <h4>Log in</h4>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  #login {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
  }
</style>
```

- Signup.vue

```html
<template>
  <div id="signup">
    <div class="content">
      <h4>Sign up</h4>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  #signup {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
  }
</style>
```

- router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '@/views/Home'
import About from '@/views/About'
import Dashboard from '@/views/Dashboard'
import Login from '@/views/Login'
import Signup from '@/views/Signup'
import NotFound from '@/views/NotFound'

Vue.use(VueRouter);

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
    path: '/dashboard',
    name: 'dashboard',
    component: Dashboard
  },
  {
    path: '/login',
    name: 'login',
    component: Login
  },
  {
    path: '/signup',
    name: 'signup',
    component: Signup
  },
  {
    path: '*',
    component: NotFound
  }
];

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
});

export default router;
```

<br>

#### Break point

```bash
$ cd vue-start
$ git add .
$ git commit -m 'Set pages'
$ git push origin master
```

<br>

<br>