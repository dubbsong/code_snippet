#### 지역 컴포넌트

###### 컴포넌트 생성

```bash
$ cd src
$ touch Home.vue
```

<br>

###### 코드 작성

- Home.vue

```vue
<template>
  <div>
    <p>{{ homeTitle }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        homeTitle: "This is Home"
      };
    }
  };
</script>
```

- App.vue

```vue
<template>
  <div>
    <h1>{{ sayHello }}</h1>
    <Home></Home>
  </div>
</template>

<script>
  import Home from './Home';
  
  export default {
    data() {
      return {
        sayHello: "What's up?"
      };
    },
    components: {
      Home
    }
  };
</script>
```

> `What's up?`과 `This is Home`이 표시된다.

<br>

#### 전역 컴포넌트

###### 컴포넌트 생성

```bash
$ cd src
$ touch Status.vue
```

<br>

###### 코드 작성

- Status.vue

```vue
<template>
  <h2>{{ text }}</h2>
</template>

<script>
  export default {
    data() {
      return {
        text: "Status is good."
      };
    }
  };
</script>
```

- Main.js

```js
...
import Status from './Status';

Vue.component('AppStatus', Status);

...
```

- App.vue

```vue
<template>
  <div>
    <h1>{{ sayHello }}</h1>
    <AppStatus></AppStatus>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        sayHello: "What's up?"
      };
    }
  };
</script>
```

> `What's up?`과 `Status is good`이 표시된다.

<br>

<br>