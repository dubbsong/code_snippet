#### Example App

- This app starts with three different pages.
  1. EventList.vue (Events Listing, root page)
  2. EventShow.vue (Showing event \#1)
  3. EventCreate.Vue (Create Event)

<br>

#### Delete files

- components/HelloWorld.vue
- views/Home.vue
- views/About.vue

<br>

#### Create files

- views/EventList.vue

```html
<template>
  <h1>Events Listing</h1>
</template>
```

- views/EventShow.vue

```html
<template>
  <h1>Showing event #1</h1>
</template>
```

- views/EventCreate.vue

```html
<template>
  <h1>Create Event</h1>
</template>
```

<br>

#### Write code

- router/index.js

```js
import Vue from "vue";
import VueRouter from "vue-router";
import EventList from "@/views/EventList";
import EventShow from "@/views/EventShow";
import EventCreate from "@/views/EventCreate";

Vue.use(VueRouter);

const routes = [
  {
    path: "/",
    name: "event-list",
    component: EventList
  },
  {
    path: "/event",
    name: "event-show",
    component: EventShow
  },
  {
    path: "/event/create",
    name: "event-create",
    component: EventCreate
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
      <router-link :to="{ name: 'event-list' }">List</router-link> |
      <router-link :to="{ name: 'event-show' }">Show Event #1</router-link> |
      <router-link :to="{ name: 'event-create' }">Create</router-link>
    </div>
    <router-view />
  </div>
</template>
```

- We see that everything is working.

<br>

<br>