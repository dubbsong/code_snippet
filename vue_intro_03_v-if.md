## v-if / v-else

<br>

#### Conditional Rendering 01

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <div class="product">
      <div class="product-image">
        <img :src="image" alt="" />
      </div>
      
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
      </div>
    </div>
  </div>
  
  ...
</body>
```

<br>

- main.js

```js
var app = new Vue({
  el: '#app',
  data: {
    product: 'Shoes',
    image: './assets/shoes-01.jpg',
    inStock: true
  }
});
```

> `inStock: true`라면 `In Stock`이 화면에 표시된다.
>
> `inStock: false`라면 `Out of Stock`이 화면에 표시된다.

<br>

<br>

#### Conditional Rendering 02

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <div class="product">
      <div class="product-image">
        <img :src="image" alt="" />
      </div>
      
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out</p>
        <p v-else>Out of Stock</p>
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
    image: './assets/shoes-01.jpg',
    inventory: 100
  }
});
```

> `inventory: 100`이면 `In Stock`이 표시된다.
>
> `inventory: 10`이면 `Almost sold out`이 표시된다.
>
> `inventory: 1`이면 `Almost sold out`이 표시된다.
>
> `inventory: 0`이면 `Out of Stock`이 표시된다.

<br>

<br>