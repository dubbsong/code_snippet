## List

<br>

#### TodoList.vue

1. 더미 데이터 저장

| key   | Value |
| ----- | ----- |
| HTML  | HTML  |
| CSS   | CSS   |
| JS    | JS    |
| VueJS | VueJS |

> `개발자 도구/Application/Local Storage/http://localhost:8080`에 4쌍의 값을 저장한다.

2. 더미 데이터 출력

```vue
<template>
  <div>
    <ul>
      <li></li>
    </ul>
  </div>
</template>

<script>
  export default {
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

3. 빈 배열에 값 push

```vue
<script>
  export default {
    data: () => ({
      todos: []
    }),
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todos.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> `개발자 도구/Vue/<TodoList>`에서 `todos: Array[4]` 를 확인할 수 있다.

4. 배열의 값을 list에 뿌려주기

```vue
<template>
  <div>
    <ul>
      <li
        v-for="todo in todos"
        v-bind:key="todo"
      >
        {{ todo }}
      </li>
    </ul>
  </div>
</template>
```

> list에 `HTML`, `CSS`, `JS`, `VueJS`가 각각 뿌려진다.

5. CSS Styling

```vue
<template>
  <div>
    <ul>
      <li
        v-for="todo in todo"
        v-bind:key="todo"
        class="shadow"
      >
        {{ todo }}
        <span class="remove-btn">
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
    text-align: left;
    padding-left: 0;
    margin-top: 0;
  }
  
  li {
    background-color: #ffffff;
    height: 50px;
    min-height: 50px;
    line-height: 50px;
    padding: 0 16px;
    margin: 8px 0;
    border-radius: 5px;
    display: flex;
  }
  
  .remove-btn {
    color: #e85a71;
    margin-left: auto;
  }
</style>
```

6. click 이벤트 추가

```vue
<template>
  <div>
    <ul>
      <li
        v-for="todo in todos"
        v-bind:key="todo"
        class="shadow"
      >
        {{ todo }}
        <span class="remove-btn" v-on:click="removeTodo">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: () => ({
      todos: []
    }),
    methods: {
      removeTodo() {
        console.log("Remove Todo");
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todos.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> 제거 버튼을 클릭하면, Console 탭에 `Remove Todo`가 출력된다.

7. index 부여

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo"
        class="shadow"
      >
        {{ todo }}
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: () => ({
      todos: []
    }),
    methods: {
      removeTodo(todo, index) {
        console.log(todo, index);
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todos.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> 제거 버튼을 클릭하면, 해당 todo와 index가 Console 탭에 출력된다.

8. localStorage의 해당 값 제거

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo"
        class="shadow"
      >
        {{ todo }}
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: () => ({
      todos: []
    }),
    methods: {
      removeTodo(todo, index) {
        localStorage.removeItem(todo);
        this.todos.splice(index, 1);
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todos.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

<br>

<br>

9. check_btn 추가 및 styling

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo"
        class="shadow"
      >
        <i class="fas fa-check check-btn"></i>
        {{ todo }}
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
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
  ...
  
  .check-btn {
    color: #4ea1d3;
    line-height: 45px;
    margin-right: 5px;
  }
</style>
```

10. click 이벤트 추가

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo"
        class="shadow"
      >
        <i class="fas fa-check check-btn" v-on:click="toggleComplete"></i>
        {{ todo }}
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: () => ({
      todos: []
    }),
    methods: {
      removeTodo(todo, index) {
        localStorage.removeItem(todo);
        this.todos.splice(index, 1);
      },
      toggleComplete() {
        console.log("Check Todo");
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todos.push(localStorage.key(i));
          }
        }
      }
    }
  };
</script>
```

> 체크 버튼을 클릭하면, Check Todo가 Console 탭에 출력된다.

<br>

<br>

#### todoInput.vue

1. obj 객체 생성

```vue
<script>
  export default {
    data: () => ({
      newTodo: ""
    }),
    methods: {
      addTodo() {
        const obj = {
          completed: false,
          item: this.newTodo
        };
        
        localStorage.setItem(this.newTodo, this.newTodo);
        this.clearInput();
      },
      clearInput() {
        this.newTodo = "";
      }
    }
  };
</script>
```

2. JSON.stringify

```vue
<script>
  export default {
    data: () => ({
      newTodo: ""
    }),
    methods: {
      addTodo() {
        const obj = {
          completed: false,
          item: this.newTodoItem
        };
        
        localStorage.setItem(this.newTodo, JSON.stringify(obj));
        this.clearInput();
      },
      clearInput() {
        this.newTodo = "";
      }
    }
  };
</script>
```

3. 조건식 작성

```vue
<script>
  export default {
    data: () => ({
      newTodo: ""
    }),
    methods: {
      addTodo() {
        if (this.newTodo !== "") {
          const obj = {
            completed: false,
            item: this.newTodo
          };
          
          localStorage.setItem(this.newTodo, JSON.stringify(obj));
          this.clearInput();
        }
      },
      clearInput() {
        this.newTodo = "";
      }
    }
  };
</script>
```

<br>

<br>

#### todoList.vue

1. 데이터 가져오기 (parsing)
   - **기존의 localStorage 데이터를 모두 제거하고, 새로 입력한다.**

```vue
<script>
  export default {
    data: () => ({
      todos: []
    }),
    methods: {
      removeTodo(todo, index) {
        localStorage.removeItem(todo);
        this.todos.splice(index, 1);
      },
      toggleComplete() {
        console.log("Check Todo");
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
           console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
          }
        }
      }
    }
  };
</script>
```

> `{completed: false, item: "HTML"}`과 같이, localStorage의 값이  Console 탭에 출력된다.

2. 가져온 값을 배열에 push

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo.item"
        class="shadow"
      >
        <i class="fas fa-check check-btn" v-on:click="toggleComplete"></i>
        {{ todo.item }}
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: () => ({
      todos: []
    }),
    methods: {
      removeTodo(todo, index) {
        localStorage.removeItem(todo);
        this.todos.splice(index, 1);
      },
      toggleComplete() {
        console.log("Check Todo");
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todos.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          }
        }
      }
    }
  };
</script>
```

> `{{todo.item}}`으로 인해 객체의 모양이 아닌 `HTML`, `CSS`, `JS`, `VueJS`만 출력된다.

3. CSS Styling

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo.item"
        class="shadow"
      >
        <i class="fas fa-check check-btn" v-on:click="toggleComplete"></i>
        <span class="text-completed">{{ todo.item }}</span>
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
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
  ...
  
  .text-completed {
    color: #b3adad;
    text-decoration: line-through;
  }
</style>
```

> 각 list에 stripe line이 적용된다.

4. class 바인딩

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo.item"
        class="shadow"
      >
        <i class="fas fa-check check-btn" v-on:click="toggleComplete"></i>
        <span v-bind:class="{text-completed: todo.completed}">{{ todo.item }}</span>
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>
```

> `completed`가 true라면, stripe line이 보여진다.

5. class 바인딩

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        v-bind:key="todo.item"
        class="shadow"
      >
        <i class="fas fa-check check-btn" v-on:click="toggleComplete(todo, index)" v-bind:class="{check-btn-completed: todo.completed}"></i>
        <span v-bind:class="{text_completed: todo.completed}">{{ todo.item }}</span>
        <span class="remove-btn" v-on:click="removeTodo(todo, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data: () => ({
      todoItems: []
    }),
    methods: {
      removeTodo: function(todoItem, index) {
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      },
      toggleComplete: function(todoItem, index) {
        console.log(todoItem);
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          }
        }
      }
    }
  };
</script>
```

6. CSS Styling

```vue
<style scoped>
  .check_btn_completed {
    color: #b3adad;
  }
</style>
```

7. toggle 구현

```vue
<script>
  export default {
    data: () => ({
      todoItems: []
    }),
    methods: {
      removeTodo: function(todoItem, index) {
        console.log(todoItem, index);
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      },
      toggleComplete: function(todoItem, index) {
        todoItem.completed = !todoItem.completed;
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
          }
        }
      }
    }
  };
</script>
```

8. localStorage 업데이트

```vue
<script>
  export default {
    data: () => ({
      todoItems: []
    }),
    methods: {
      removeTodo: function(todoItem, index) {
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      },
      toggleComplete: function(todoItem, index) {
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
          }
        }
      }
    }
  };
</script>
```

> 토글 기능이 정상 작동하고, 새로고침 후에도 변하지 않는다.

<br>

<br>

