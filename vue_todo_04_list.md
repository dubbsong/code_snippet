## List

<br>

#### TodoList.vue

1. 더미 데이터 저장 (Local Storage)

| Key   | Value |
| ----- | ----- |
| HTML  | HTML  |
| CSS   | CSS   |
| JS    | JS    |
| VueJS | VueJS |

2. 더미 데이터 출력

```vue

```





<br>

#### localStorage 값 출력 확인

- TodoList.vue

```vue
<template>
  <div>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        todoItems: []
      };
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          console.log(localStorage.key(i));
        }
      }
    }
  };
</script>
```

> Console 탭에 `HTML`, `CSS`, `JS`, `VueJS`가 출력된다.
>
> `created`: 인스턴스가 생성되자마자 호출되는 라이프사이클 훅

<br>

#### todoItems 배열에 값 넣기

- TodoList.vue

```vue
<template>
  <div>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        todoItems: []
      };
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> `개발자 도구/Vue/<TodoList>`에서 `todoItems: Array[4]`를 확인할 수 있다.

<br>

#### list에 값 넣기

- TodoList.vue

```vue
<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems" v-bind:key="todoItem">
        {{ todoItem }}
      </li>
    </ul>
  </div>
</template>

<script>
  ...
</script>
```

> 화면에 `HTML`, `CSS`, `JS`, `VueJS`가 출력된다.

<br>

#### CSS 작성

- TodoInput.vue

```vue
<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  ...
</script>

<style scoped>
  ul {
    list-style-type: none;
    padding-left: 0;
    margin-top: 0;
    text-align: left;
  }
  
  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    background: white;
    padding: 0 0.9rem;
    margin: 0.5rem 0;
    border-radius: 5px;
  }
  
  .removeBtn {
    color: #de4343;
    margin-left: auto;
  }
  
  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
  }
  
  .checkBtnCompleted {
    color: #b3adad;
  }
  
  .textCompleted {
    text-decoration: line-through;
    color: #b3adad;
  }
</style>
```

<br>

#### 제거 기능 구현

- 01

```vue
<script>
  export default {
    data: function() {
      return {
        todoItems: []
      };
    },
    methods: {
      removeTodo: function() {
        console.log("remove item");
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> `trash` 버튼을 누르면, Console 탭에 `remove item`이 표시된다.

- 02

```vue
<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        todoItems: []
      };
    },
    methods: {
      removeTodo: function(todoItem, index) {
        console.log(todoITem, index);
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> `trash` 버튼을 누르면, Console 탭에 해당 값과 index가 표시된다.

- 03

```vue
<script>
  export default {
    data: function() {
      return {
        todoItems: []
      };
    },
    methods: {
      removeTodo: function(todoItem, index) {
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> `trash` 버튼을 누르면, localStorage의 해당 값이 제거되고, 화면에서도 해당 값이 제거된다.
>
> `splice()`: 배열에  item을 추가/제거한 후, 제거된 item을 반환한다.
>
> `slice()`: 문자열/배열의 일부를 추출하고, 새 문자열/배열로 반환한다.

<br>

####  check 기능 구현

- 

























