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
  localStorage.setItem('key', value);
}

function handleSubmit(event) {
  event.preventDefault();
  const currentValue = greetingInput.value;
  greetingForm.classList.remove('showing');
  greetingName.classList.add('showing');
  greetingName.innerText = `What's up? ${currentValue}`;
  saveName(currentValue);
}

function init() {
  const getName = localStorage.getItem('key');
  
  if (getName === null) {
    greetingForm.classList.add('showing');
    greetingForm.addEventListener('submit', handleSubmit);
  } else {
    greetingForm.classList.remove('showing');
    greetingName.classList.add('showing');
    greetingName.innerText = `What's up? ${getName}`;
  }
}

init();
```

<br>