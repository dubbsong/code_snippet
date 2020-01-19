- index.html

```html
<form class="greeting_form hiding">
  <input type="text" placeholder="What's your name?">
</form>
<h4 class="greeting_name hiding"></h4>
```

<br>

- index.css

```css
.hiding {
  display: none;
}

.showing {
  display: block;
}
```

<br>

- greeting.js

```js
const greetingForm = document.querySelector('.greeting_form');
const greetingInput = greetingForm.querySelector('input');
const greetingName = document.querySelector('.greeting_name');

function saveName(value) {
  localStorage.setItem('user', value);
}

function handleSubmit(event) {
  event.preventDefault();
  const currentValue = greetingInput.value;
  sayHello(currentValue);
  saveName(currentValue);
}

function askForName() {
  greetingForm.classList.add('showing');
  greetingForm.addEventListener('submit', handleSubmit);
}

function sayHello(name) {
  greetingForm.classList.remove('showing');
  greetingName.classList.add('showing');
  greetingName.innerText = `Hello, ${name}`;
}

function loadName() {
  const name = localStorage.getItem('user');
  
  if (name === null) {
    askForName();
  } else {
    sayHello(name);
  }
}

function init() {
  loadName();
}

init();
```

<br>