###### Hello World 01

- App.vue

```vue
<template>
  <h2>{{ sayHello }}</h2>
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

> 화면에 `What's up?`이 표시된다.

<br>

###### Hello World 02

- App.vue

```vue
<template>
  <div>
    <h2>{{ sayHello }}</h2>
    <p>{{ name }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        sayHello: "What's up?",
        name: "Sam"
      };
    }
  };
</script>
```

> `<template>` 태그 내에는 하나의 element만 포함될 수 있다.
>
> 보통 `<div>` 태그로 감싸준다.

<br>

###### count

- App.vue

```vue
,<template>
  <div>
    <p>{{ count }}</p>
    <button @click="count++">ADD</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        count: 1
      };
    }
  };
</script>
```

> `ADD` 버튼을 클릭하면 count가 증가한다.

<br>

<br>