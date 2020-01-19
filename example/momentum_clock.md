- clock.html

```html
<header>
  <h2 class="current_time"></h2>
</header>
```

<br>

- clock.js

```js
const currentTime = document.querySelector('.current_time');

function getTime() {
  const date = new Date();
  const hours = date.getHours();
  const minutes = date.getMinutes();
  const seconds = date.getSeconds();
  
  currentTime.innerHTML = `
		${hours < 10 ? `0${hours}` : hours}:
		${minutes < 10 ? `0${minutes}` : minutes}:
		${seconds < 10 ? `0${seconds}` : seconds}
	`;
}

function init() {
  getTime();
  setInterval(getTime, 1000);
}

init();
```

<br>