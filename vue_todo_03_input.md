## Input

<br>

#### TodoInput.vue

1. HTML 작성

```vue
<template>
  <div>
    <input type="text" />
    <button>add</button>
  </div>
</template>
```

2. 데이터 바인딩

```vue
<template>
  <div>
    <input type="text" v-model="newTodoItem" />
    <button v-on:click="addTodo">add</button>
  </div>
</template>

<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        console.log(this.newTodoItem);
      }
    }
  };
</script>
```

> input에 입력을 하면, `개발자 도구/Vue`에서 입력에 따라 변화하는 것을 확인할 수 있다.
>
> input에 입력을 하고 `add` 버튼을 누르면, `개발자 도구/Console`에 입력 값이 표시된다.

3. keyup\.enter 이벤트 추가

```vue
<template>
  <div>
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <button v-on:click="addTodo">add</button>
  </div>
</template>
```

> input에 입력을 하고 `Enter`를 누르면, `개발자 도구/Console`에 입력 값이 표시된다.

4. 입력 값 저장

```vue
<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        // console.log(this.newTodoItem);
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
      }
    }
  };
</script>
```

> input에 입력을 하고 `add` 버튼을 누르면, `개발자 도구/Application/Local Storage/http://localhost:8080`에 값이 저장되는 것을 확인할 수 있다.
>
> `localStorage.setItem('key', 'value');`: 값을 `key:value`의 형식으로 localStorage에 저장한다.

5. input 초기화

```vue
<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
        this.newTodoItem = "";
      }
    }
  };
</script>
```

> input에 입력을 하고 `add` 버튼을 누르면, 값이 저장되고 input이 초기화된다.

6. 코드 분할

```vue
<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
        this.clearInput();
      },
      clearInput() {
        this.newTodoItem = "";
      }
    }
  };
</script>
```

> 위와 동일하게 동작한다.
>
> `this`를 사용해서 `data`와 `methods`에 접근할 수 있다.

7. CSS Styling

```vue
<template>
  <div class="input_box shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="add_container" v-on:click="addTodo">
      <i class="fas fa-plus add_btn"></i>
    </span>
  </div>
</template>

<script>
  ...
</script>

<style scoped>
  .input_box {
    background-color: #ffffff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  
  .input_box input {
    font-size: 16px;
    border-style: none;
  }
  
  .add_container {
    background-color: #4ea1d3;
    float: right;
    width: 48px;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
  }
  
  .add_btn {
    color: #ffffff;
    vertical-align: middle;
  }
</style>
```

<br>

<br>

#### Result

```vue
<template>
  <div class="input_box shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="add_container" v-on:click="addTodo">
      <i class="fas fa-plus add_btn"></i>
    </span>
  </div>
</template>

<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        // console.log(this.newTodoItem);
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
        this.clearInput();
      },
      clearInput() {
        this.newTodoItem = "";
      }
    }
  };
</script>

<style scoped>
  .input_box {
    background-color: #ffffff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  
  .input_box input {
    font-size: 16px;
  }
  
  .add_container {
    background-color: #4ea1d3;
    float: right;
    width: 48px;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
  }
  
  .add_btn {
    color: #ffffff;
    vertical-align: middle;
  }
</style>
```

<br>

<br>