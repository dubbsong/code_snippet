## Example App

###### EventList.vue

- A home page where we list all events.
- This is also the root page.

###### EventShow.vue

- A page that shows the details of a single event, and allows us to say we're attending an event.

###### EventCreate.vue

- A page where we can create an event.

<br>

<br>

#### Starting Code

- structure

```bash
src
  ├─ components
  ├─ router
  │   └─ index.js
  ├─ store
  │   └─ index.js
  ├─ views
  │   ├─ EventList.vue
  │   ├─ EventCreate.vue
  │   └─ EventShow.vue
  ├─ App.vue
  └─ main.js
```

- views/EventList.vue

```html
<template>
  <h1>Events Listing</h1>
</template>
```

- views/EventCreate.vue

```html
<template>
  <h1>Create Event</h1>
</template>
```

- views/EventShow.vue

```html
<template>
  <h1>Showing event #1</h1>
</template>
```

- components/NotFound.vue

```html
<template>
  <h1>Not Found</h1>
</template>
```

- router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import EventList from '@/views/EventList'
import EventCreate from '@/views/EventCreate'
import EventShow from '@/views/EventShow'
import NotFound from '@/components/NotFound'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'event-list',
    component: EventList
  },
  {
    path: '/event/create',
    name: 'event-create',
    component: EventCreate
  },
  {
    path: '/event/show',
    name: 'event-show',
    component: EventShow
  },
  {
    path: '*',
    component: NotFound
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
```

- App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'event-list' }">List</router-link> |
      <router-link :to="{ name: 'event-create' }">Create</router-link> |
      <router-link :to="{ name: 'event-show' }">Show Event #1</router-link>
    </div>
  </div>
</template><br>
```

<br>

<br>

#### Next

- views/EventList.vue

```html
<template>
  <div>
    <h1>Events Listing</h1>
    <p>
      <router-link :to="{ name: 'event-show', params: { id: '1' } }">First Event</router-link>
    </p>
  </div>
</template>
```

- EventShow.vue

```html
<template>
  <h1>Showing event #{{ id }}</h1>
</template>

<script>
  export default {
    props: ['id']
  }
</script>
```

- router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import EventList from '@/views/EventList'
import EventCreate from '@/views/EventCreate'
import EventShow from '@/views/EventShow'
import NotFound from '@/components/NotFound'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'event-list',
    component: EventList
  },
  {
    path: '/event/create',
    name: 'event-create',
    component: EventCreate
  },
  {
    path: '/event/:id',
    name: 'event-show',
    component: EventShow,
    props: true
  },
  {
    path: '*',
    component: NotFound
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
```

- App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'event-list' }">List</router-link> |
      <router-link :to="{ name: 'event-create' }">Create</router-link>
    </div>
    <router-view />
  </div>
</template>
```

<br>

<br>

#### 



















