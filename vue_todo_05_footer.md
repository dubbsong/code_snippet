## Footer

<br>

#### TodoFooter.vue

1. 버튼 추가

```vue
<template>
  <div>
    <span>Clear All</span>
  </div>
</template>
```

2. CSS Styling

```vue
<template>
  <div class="clear_all_container">
    <span class="clear_all_btn">Clear All</span>
  </div>
</template>

<style scoded>
  .clear_all_container {
    background-color: #ffffff;
    width: 120px;
    height: 50px;
    min-height: 50px;
    line-height: 50px;
    border-radius: 5px;
    margin: 0 auto;
  }
  
  .clear_all_btn {
    color: #e85a71;
    cursor: pointer;
  }
</style>
```

3. click 이벤트 추가

```vue
<template>
  <div class="clear_all_container">
    <span class="clear_all_btn" v-on:click="clearAll">Clear All</span>
  </div>
</template>
```

4. 메소드 추가

```vue
<script>
  export default {
    methods: {
      clearAll() {
        localStorage.clear();
      }
    }
  };
</script>
```

> `Clear All` 버튼을 클릭하면, localStorage의 모든 값이 제거된다.
>
> 화면의 값은 새로고침 후 제거된 것을 확인할 수 있다.

<br>

<br>