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

2. 더미 데이터 Console 출력

```vue
<template>
  <div>
    <ul>
      <li></li>
      <li></li>
      <li></li>
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

3. 각 값을 배열에 push

```vue
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

4. 배열의 값을 list로 출력

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
```

> 화면에 `HTML`, `CSS`, `JS`, `VueJS`가 출력된다.

5. CSS Styling (ul, li)

```vue
<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
      </li>
    </ul>
  </div>
</template>

<script>
  ...
</script>

<style scoped>
  ul {
    text-align: left;
    list-style-type: none;
    padding-left: 0;
    margin-top: 0;
  }
  
  li {
    background: #ffffff;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    padding: 0 0.9rem;
    margin: 0.5rem 0;
    border-radius: 5px;
  }
</style>
```

6. 제거 버튼 추가

```vue
<template>
  <div>
    <ul>
      <li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
        <span class="removeBtn">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>
```

7. CSS Styling (removeBtn)

```vue
<style scoped>
  ul {
  	...
  }
  
  li {
    ...
    display: flex;
  }
  
  .removeBtn {
    ...
    color: #de4343;
    margin-left: auto;
  }
</style>
```

8. 제거할 item과 index Console 출력

```vue
<template>
  <div>
    <ul>
      <li v-for="(todoItem in todoItems" v-bind:key="todoItem" class="shadow">
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
        console.log(todoItem, index);
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

> 제거 버튼을 누르면, 해당 item과 index가 Console 탭에 출력된다.

9. 제거 기능 구현

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

> 제거 버튼을 누르면, 해당 item이 제거된다.
>
> `splice()`: 배열에 item을 추가/제거한 후, 제거된 item을 반환한다.
>
> `slice()`: 문자열/배열의 일부를 추출하고, 새 문자열/배열로 반환한다.

10. check 버튼 추가

```vue
<template>
  <div>
    <ul>
      <li v-for="(todoItem in todoItems" v-bind:key="todoItem" class="shadow">
        <i class="fas fa-check checkBtn"></i>
        {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>
```

11. CSS Styling (checkBtn)

```vue
<style scoped>
  ...
  
  .checkBtn {
    color: #62acde;
    line-height: 45px;
    margin-right: 5px;
  }
</style>
```

12. click 이벤트 추가

```vue
<template>
  <div>
    <ul>
      <li v-for="(todoItem in todoItems" v-bind:key="todoItem" class="shadow">
        <i class="fas fa-check checkBtn" v-on:click="toggleComplete"></i>
        {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>
```

13. 코드 수정 (todoInput.vue)

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
        if (this.newTodoItem !== "") {
          const obj = {
            completed: false,
            item: this.newTodoItem
          };
          
          localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
          this.clearInput();
        }
      },
      clearInput: function() {
        this.newTodoItem = "";
      }
    }
  };
</script>
```

> 입력을 하고 새로고침을 해야만 화면에 출력된다.

14. 코드 수정 (todoList.vue)

```vue
<template>
  <div>
    <ul>
      <li v-for="{todoItem, index} in todoItems" v-bind:key="todoItem.item" class="shadow">
        <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
        <span v-bind:class="{textCompleted:todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
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
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            // this.todoItems.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

15. CSS Styling

```vue
<style scoped>
  ...
  
  .checkBtnCompleted {
    color: #b3adad;
  }
  
  .textCompleted {
    color: #b3adad;
    text-decoration: line-through;
  }
</style>
```

16. toggle 기능 추가

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
      },
      toggleComplete: function(togoItem, index) {
        todoItem.completed = !todoItem.completed;
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            // this.todoItems.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> check를 클릭하면, 가로줄이 나타난다.

<br>

<br>