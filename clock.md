- clock.html

```html
<div class="clock_container">
  <h4 class="current_time"></h4>
</div>
```

<br>

- clock.js

```js
const clockContainer = document.querySelector('.clock_container');
const currentTime = clockContainer.querySelector('.current_time');

function getTime() {
  const date = new Date();
  const hours = date.getHours();
  const minutes = date.getMinutes();
  const seconds = date.getSeconds();
  
  currentTime.innerHTML = `${hours < 10 ? `0${hours}` : hours} : ${minutes < 10 ? `0${minutes}` : minutes} : ${seconds < 10 ? `0${seconds}` : seconds}`;
}

function init() {
  getTime();
  setInterval(getTime, 1000);
}

init();
```

<br>