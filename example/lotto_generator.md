- HTML

```html
<div class="container">
  <h2>LOTTO GENERATOR</h2>
  <p></p>
  <button>Generate</button>
</div>
```

<br>

- Pure JS

```js
const container = document.querySelector('.container');
const output = container.querySelector('p');
const button = container.querySelector('button');

function handleClick() {
  let arr = [];
  
  for (let i = 0; i < 6; i++) {
    let randomNum = Math.floor(Math.random() * 45) + 1;
    
    if (randomNum < 10) {
      randomNum = `0${randomNum}`;
    }
    
    if (arr.includes(randomNum) === false) {
      arr.push(randomNum);
    } else {
      i--;
    }
  }
  
  output.innerText = arr.sort((a, b) => a - b).join(' ');
}

function init() {
  button.addEventListener('click', handleClick);
}

init();
```

<br>

<br>

- jQuery

```js
$(function() {
  $('button').on('click', function() {
    let arr = [];
    
    for (let i = 0; i < 6; i++) {
      let randomNum = Math.floor(Math.random() * 45) + 1;
      
      if (randomNum < 10) {
        randomNum = `0${randomNum}`;
      }
      
      if (arr.includes(randomNum) === false) {
        arr.push(randomNum);
      } else {
        i--;
      }
    }
    
    $('p').text(arr.sort((a, b) => a - b).join(' '));
  });
});
```

<br>

<br>

- CSS

```css
body {
  background-color: #141414;
  color: #ffffff;
  font-family: 'Ubuntu', sans-serif;
  text-align: center;
  height: 100vh;
  margin: 0;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

h2 {
  font-size: 1.8rem;
}

p {
  font-size: 20px;
  line-height: 40px;
  word-spacing: 10px;
  width: 260px;
  height: 40px;
  border-bottom: 2px solid #e5e5e5;
  margin: 0;
}

button {
  font-size: 14px;
  width: 85px;
  height: 35px;
  color: #141414;
  border-radius: 0.25rem;
  margin-top: 25px;
  cursor: pointer;
}
```

<br>

<br>