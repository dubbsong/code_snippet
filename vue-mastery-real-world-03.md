#### Dynamic Routes

- views/User.vue

```html
<template>
  <div class="user">
    <h1>This is a page for {{ $route.params.username }}</h1>
  </div>
</template>
```

- router/index.js

```js
...
import User from "@/views/User";

Vue.use(VueRouter);

const routes = [
  ...
  {
    path: "/user/:username",
    name: "user",
    component: User
  }
];

...
```

- App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      ...
      <router-link :to="{ name: 'user', params: { username: 'omb' } }">OMB</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
  ...
</style>
```

> Now when you visit `localhost:8080/#/user/omb`, you see `This is a page for omb`.
>
> But using `$route.params` in your component limits its flexibility.

<br>

<br>

#### Using Props for Routes

- router/index.js

```js
...
import User from "@/views/User";

Vue.use(VueRouter);

const routes = [
  ...
  {
    path: "/user/:username",
    name: "user",
    component: User,
    props: true
  }
];

...
```

- views/User.vue

```html
<template>
  <div class="user">
    <h1>{{ username }}</h1>
  </div>
</template>

<script>
  export default {
    props: ["username"]
  };
</script>
```

> Everything will now work the same.

<br>

<br>

#### History mode (remove \#)

- router/index.js

```js
...

const router = new VueRouter({
  mode: "history",
  routes
});

...
```

<br>

<br>

#### Handling 404s

- views/NotFound.vue

```html
<template>
  <div class="not-found">
    <h1>Not Found</h1>
  </div>
</template>
```

- router/index.js

```js
...
import NotFound from "@/views/NotFound";

...

const routes = [
  ...
  {
    path: "*",
    component: NotFound
  }
];

...
```

> Now when you visit `localhost:8080/abcd`, you see `Not Found`.

<br>

<br>

#### Example Application

- router/index.js

```js
import Vue from "vue";
import VueRouter from "vue-router";
import EventList from "@/views/EventList";
import EventShow from "@/views/EventShow";
import EventCreate from "@/views/EventCreate";
import NotFound from "@/views/NotFound";

Vue.use(VueRouter);

const routes = [
  {
    path: "/",
    name: "event-list",
    component: EventList
  },
  {
    path: "/event/create",
    name: "event-create",
    component: EventCreate
  },
  {
    path: "/event/:id",
    name: "event-show",
    component: EventShow,
    props: true
  },
  {
    path: "*",
    component: NotFound
  }
];

const router = new VueRouter({
  mode: "history",
  routes
});

export default router;
```

- EventList.vue

```html
<template>
  <div>
    <h1>Events Listing</h1>
    <p>
      <router-link :to="{ name: 'event-show', params: { id: '1' } }">Show Event #1</router-link>
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
    props: ["id"]
  };
</script>
```

- EventCreate.vue

```html
<template>
  <h1>Create Event</h1>
</template>
```

- App.vue

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'event-list' }">List</router-link>
      <router-link :to="{ name: 'event-create' }">Create</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
  ...
</style>
```

> This is all we need for now, and we're ready to jump into the next lesson.

<br>

<br>