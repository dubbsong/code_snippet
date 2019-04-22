- index.html

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
  });
  
  todos = cleanTodos;
  saveTodos();
}

function loadTodos() {
  const loadedTodos = localStorage.getItem('todos');
  
  if (loadedTodos !== null) {
    const parsedTodos = JSON.parse(loadedTodos);
    
    parsedTodos.forEach(todo => {
      showTodo(todo.text);
    });
  }
}

function handleSubmit(event) {
  event.preventDefault();
  const currentValue = todoInput.value;
  showTodo(currentValue);
  todoInput.value = '';
}

function init() {
  loadTodos();
  todoForm.addEventListener('submit', handleSubmit);
}

init();
```

------

> `forEach()` 메소드
>
> 배열의 각 element에 대해, 제공된 함수를 차례로 한 번씩 호출한다.

> `filter()` 메소드
>
> 테스트를 통과한 배열의 각 값을 모아, 새 배열로 반환한다.

------

<br>

> **JSON의 일반적인 사용은, 웹 서버와 데이터를 교환하는 것이다.**

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
  - 문자열 데이터를 JS 객체로 변환한다.

```js
console.log(JSON.parse('{"name":"Sam","age":28,"city":"Dubbo"}'));
// {name: "Sam", age: 28, city: "Dubbo"}
```

------

<br>