## v-for

<br>

#### List Rendering 01

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
        
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
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
    inStock: true,
    details: ['80% cotton', '20% polyester', 'Gender-neutral']
  }
});
```

> 화면에 `details` list가 뿌려진다.

<br>

<br>

#### List Rendering 02

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
        
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        
        <div v-for="variant in variants" :key="variant.variantId">
          <p>{{ variant.variantColor }}</p>
        </div>
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
    inStock: true,
    details: ['80% cotton', '20% polyester', 'Gender-neutral'],
    variants: [
      {
        variantId: 2234,
        variantColor: 'black'
      },
      {
        variantId: 2235,
        variantColor: 'yellow'
      }
    ]
  }
});
```

> 화면에 `red`와 `black`이 표시된다.

<br>

<br>