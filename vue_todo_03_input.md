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
    data: function() {
      return {
        newTodoItem: ""
      };
    },
    methods: {
      addTodo: function() {
        console.log(this.newTodoItem);
      }
    }
  };
</script>
```

> input에 입력을 하면, `개발자 도구/Vue`에서 입력에 따라 변화하는 것을 확인할 수 있다.
>
> input에 입력을 하고 `add` 버튼을 누르면, `개발자 도구/Console`에 입력 값이 표시된다.

3. 입력 값 저장

```vue
<script>
  export default {
    data: function() {
      return {
        newTodoItem: ""
      };
    },
    methods: {
      addTodo: function() {
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
      }
    }
  };
</script>
```

> input에 입력을 하고 `add` 버튼을 누르면, `개발자 도구/Application/Local Storage/http://localhost:8080`에 값이 저장되는 것을 확인할 수 있다.
>
> `localStorage.setItem('key', 'value');`: 값을 `key:value`의 형식으로 localStorage에 저장한다.

4. input 초기화

```vue
<script>
  export default {
    data: function() {
      return {
        newTodoItem: ""
      };
    },
    methods: {
      addTodo: function() {
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
        this.newTodoItem = "";
      }
    }
  };
</script>
```

> input에 입력을 하고 `add` 버튼을 누르면, 값이 저장되고 input이 초기화된다.

5. 코드 분할

```vue
<script>
  export default {
    data: function() {
      return {
        newTodoItem: ""
      };
    },
    methods: {
      addTodo: function() {
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
        this.clearInput();
      },
      clearInput: function() {
        this.newTodoItem = "";
      }
    }
  };
</script>
```

> 위와 동일하게 동작한다.
>
> `this`를 사용해서 `data`와 `methods`에 접근할 수 있다.

6. keyup 추가

```vue
<template>
  <div>
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <button v-on:click="addTodo">add</button>
  </div>
</template>
```

> input에 입력을 하고 `Enter`를 누르면, 값이 저장되고 input이 초기화된다.

7. CSS Styling

```vue
<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
  ...
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  
  .inputBox {
    background: #ffffff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  
  .inputBox input {
    font-size: 0.9rem;
    border-style: none;
  }
  
  .addContainer {
    background: linear-gradient(to right, #6478fb, #8763fb);
    float: right;
    width: 3rem;
    border-radius: 0 5px 5px 0;
    display: block;
    cursor: pointer;
  }
  
  .addBtn {
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
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        newTodoItem: ""
      };
    },
    methods: {
      addTodo: function() {
        localStorage.setItem(this.newTodoItem, this.newTodoItem);
        this.clearInput();
      },
      clearInput: function() {
        this.newTodoItem = "";
      }
    }
  };
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  
  .inputBox {
    background: #ffffff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  
  .inputBox input {
    font-size: 0.9rem;
    border-style: none;
  }
  
  .addContainer {
    background: linear-gradient(to right, #6478fb, #8763fb);
    float: right;
    width: 3rem;
    border-radius: 0 5px 5px 0;
    display: block;
    cursor: pointer;
  }
  
  .addBtn {
    color: #ffffff;
    vertical-align: middle;
  }
</style>
```

<br>

<br>