- todo.html

```html
<form class="todo_form">
  <input type="text" placeholder="+ todo">
</form>
<ul class="todo_list"></ul>
```

<br>

- todo.js

```js
const todoForm = document.querySelector('.todo_form');
const todoInput = todoForm.querySelector('input');
const todoList = document.querySelector('.todo_list');

let todos = [];

function saveTodos() {
  localStorage.setItem('todos', JSON.stringify(todos));
}

function showTodo(text) {
  const li = document.createElement('li');
  const span = document.createElement('span');
  const delBtn = document.createElement('button');
  const newId = todos.length + 1;
  
  todoList.appendChild(li);
  li.id = newId;
  li.appendChild(span);
  li.appendChild(delBtn);
  
  span.innerText = text;
  delBtn.innerHTML = '&times;';
  delBtn.addEventListener('click', deleteTodo);
  
  const todoObj = {
    id: newId,
    text: text
  };
  
  todos.push(todoObj);
  saveTodos();
}

function deleteTodo(event) {
  const btn = event.target;
  const li = btn.parentNode;
  
  todoList.removeChild(li);
  
  const cleanTodos = todos.filter(todo => {
    return todo.id !== parseInt(li.id);
  })
  
  todo = cleanTodos;
  saveTodos();
}

function handleSubmit(event) {
  event.preventDefault();
  const currentValue = todoInput.value;
  showTodo(currentValue);
  todoInput.value = '';
}

function loadTodos() {
  const loadedTodos = localStorage.getItem('todos');
  
  if (loadedTodos !== null) {
    const parsedTodos = JSON.parse(loadedTodos);
    
    parsedTodos.forEach(todo => {
      showTodo(todo.text);
    })
  }
}

function init() {
  loadTodos();
  todoForm.addEventListener('submit', handleSubmit);
}

init();
```

------

<br>

- `JSON.stringify()`
  - JS 객체를 문자열로 변환한다.

```js
const obj = {
  name: "Sam",
  age: 28,
  city: "Dubbo"
};

console.log(JSON.stringify(obj));	// {"name":"Sam","age":28,"city":"Dubbo"}
```

<br>

- `JSON.parse()`
  - 데이터를 JS 객체로 변환한다.

```js
console.log(JSON.parse('{"name":"Sam","age":28,"city":"Dubbo"}'));
// {name: "Sam", age: 28, city: "Dubbo"}
```

<br>