- bg.js

```js
const body = document.querySelector('body');
const IMG_NUMBER = 6;

function showImg(imgNum) {
  const img = new Image();
  
  img.src = `./img/${imgNum + 1}.png`;
  img.classList.add('bg_img');
  body.prepend(img);
}

function getRandom() {
  return Math.floor(Math.random() * IMG_NUMBER);
}

function init() {
  showImg(getRandom());
}

init();
```

<br>

- bg.css

```css
.bg_img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  animation: fadeIn 0.5s linear;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  
  to {
    opacity: 1;
  }
}
```

<br>