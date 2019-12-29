#### Anatomy of a Single File Component

- Vue components combine markup(HTML), logic(JS), and style(CSS) into one, single file.

```html
<template>
  <div>
    <!-- Here is where we lay out the structure of our component -->
  </div>
</template>

<script>
  export default {
    // Here is where we give our component the ability to behave and perform logic
  }
</script>

<style scoped>
  /* Here is where we design the appearance of our component */
</style>
```

- Part of what makes Vue so powerful is how it’s flexible and allows you to use alternatives to the traditional HTML, JS and CSS setup.

```html
<template lang="pug"></template>

<script lang="ts"></script>

<style lang="scss" scoped></style>
```

<br>

<br>

#### Use SCSS

```bash
$ npm install --save-dev sass-loader node-sass
```

<br>

<br>

#### Create Component

- components/EventCard.vue

```html
<template>
  <div>
    <h4>{{ title }}</h4>
  </div>
</template>

<script>
  export default {
    data() {
      return (
        title: 'Sam Azor'
      )
    }
  }
</script>

<style scoped>
  h4 {
    color: #20a19c;
  }
</style>
```

<br>

#### Nesting Components

- 