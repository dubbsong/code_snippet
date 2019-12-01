

#### Vue Instance

- index.html

```html
<body>
  <!-- App -->
  <div id="app">
    <!-- Expression -->
    <h1>{{ product }}</h1>
  </div>
  
  ...
</body>
```

- main.js

```js
// Vue Instance
var app = new Vue({
  el: '#app',
  data: {
    product: 'Shoes'
  }
});
```

> 화면에 `Shoes`가 표시된다.

<br>

#### Reactivity (반응성)

- Chrome Console

```js
app.product = 'AirPods';
```

> 화면의 `Shoes`가 `AirPods`로 변경된다.

<br>

<br>