## v-bind

<br>

#### Attribute Binding

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <div class="product">
      <div class="product-image">
        <img v-bind:src="image" alt="" />
      </div>
      
      <div class="product-info">
        <h1>{{ product }}</h1>
      </div>
    </div>
  </div>
  
  ...
</body>
```

- main.js

```js
var app = new Vue({
  el: '#app',
  data: {
    product: 'Shoes',
    image: './assets/shoes-01.jpg'
  }
});
```

> 화면에 `shoes-01.jpg`와 `Shoes`가 표시된다.
>
> `v-bind:` 디렉티브는 `:`로 단축할 수 있다.

<br>

<br>