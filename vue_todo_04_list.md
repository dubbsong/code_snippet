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
      todoItems: []
    }),
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

> `개발자 도구/Vue/<TodoList>`에서 `todoItems: Array[4]` 를 확인할 수 있다.

4. 배열의 값을 list에 뿌려주기

```vue
<template>
  <div>
    <ul>
      <li
        v-for="todoItem in todoItems"
        v-bind:key="todoItem"
      >
        {{ todoItem }}
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
        v-for="todoItem in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
        {{ todoItem }}
        <span class="removeBtn">
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
    background: #ffffff;
    height: 50px;
    min-height: 50px;
    line-height: 50px;
    padding: 0 1rem;
    margin: 0.5rem 0;
    border-radius: 5px;
    display: flex;
  }
  
  .removeBtn {
    color: #de4343;
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
        v-for="todoItem in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
        {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo">
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
      removeTodo: function() {
        console.log("Remove Item");
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

> 제거 버튼을 클릭하면, Console 탭에 `Remove Item`이 출력된다.

7. index 부여

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
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
    data: () => ({
      todoItems: []
    }),
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

> 제거 버튼을 클릭하면, 해당 todoItem과 index가 Console 탭에 출력된다.

8. localStorage의 해당 값 제거

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
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
    data: () => ({
      todoItems: []
    }),
    methods: {
      removeTodo: function(todoItem, index) {
        console.log(todoItem, index);
        localStorage.removeItem(todoItem);
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

> localStorage의 값은 바로 제거되지만, list의 값은 새로고침 후에 제거된다.

9. 새로고침 없이 함께 제거

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
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
    data: () => ({
      todoItems: []
    }),
    methods: {
      removeTodo: function(todoItem, index) {
        console.log(todoItem, index);
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

> 제거 버튼을 클릭하면, 화면의 값과 localStorage의 값이 함께 제거된다.

10. CSS Styling for checkBtn

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
        <i class="fas fa-check checkBtn"></i>
        {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
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
  
  .checkBtn {
    color: #62acde;
    line-height: 45px;
    margin-right: 5px;
  }
</style>
```

11. click 이벤트 추가

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem"
        class="shadow"
      >
        <i class="fas fa-check checkBtn" v-on:click="toggleComplete"></i>
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
    data: () => ({
      todoItems: []
    }),
    methods: {
      removeTodo: function(todoItem, index) {
        console.log(todoItem, index);
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      },
      toggleComplete: function() {
        console.log("Check Item");
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

> 체크 버튼을 클릭하면, Check Item이 Console 탭이 출력된다.

<br>

<br>

#### todoInput.vue

1. obj 객체 생성

```vue
<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        const obj = {
          completed: false,
          item: this.newTodoItem
        };
        
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

2. JSON.stringify

```vue
<script>
  export default {
    data: () => ({
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        const obj = {
          completed: false,
          item: this.newTodoItem
        };
        
        localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
        this.clearInput();
      },
      clearInput() {
        this.newTodoItem = "";
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
      newTodoItem: ""
    }),
    methods: {
      addTodo() {
        if (this.newTodoItem !== '') {
          const obj = {
            completed: false,
            item: this.newTodoItem
          };
          
          localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
          this.clearInput();
        }
      },
      clearInput() {
        this.newTodoItem = "";
      }
    }
  };
</script>
```

<br>

<br>

#### todoList.vue

1. 데이터 가져오기 (parsing)

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
      toggleComplete: function() {
        console.log("Check Item");
      }
    },
    created: function() {
      if (localStorage.length > 0) {
        for (let i = 0; i < localStorage.length; i++) {
          if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
            console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
            
            // this.todoItems.push(localStorage.key(i));
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
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem.item"
        class="shadow"
      >
        <i class="fas fa-check checkBtn" v-on:click="toggleComplete"></i>
        {{ todoItem.item }}
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
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
        console.log(todoItem, index);
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      },
      toggleComplete: function() {
        console.log("Check Item");
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

> `{{todoItem.item}}`으로 인해 객체의 모양이 아닌 `HTML`, `CSS`, `JS`, `VueJS`만 출력된다.

3. CSS Styling

```vue
<template>
  <div>
    <ul>
      <li
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem.item"
        class="shadow"
      >
        <i class="fas fa-check checkBtn" v-on:click="toggleComplete"></i>
        <span class="textCompleted">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
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
  
  .textCompleted {
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
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem.item"
        class="shadow"
      >
        <i class="fas fa-check checkBtn" v-on:click="toggleComplete"></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
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
        v-for="(todoItem, index) in todoItems"
        v-bind:key="todoItem.item"
        class="shadow"
      >
        <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
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
        console.log(todoItem, index);
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
  .checkBtnCompleted {
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
        console.log(todoItem, index);
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

