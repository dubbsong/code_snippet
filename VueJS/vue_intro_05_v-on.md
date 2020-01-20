## v-on

<br>

#### Event Handling 01

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
        
        <button>Add to cart</button>
        
        <div class="cart">
          <p>Cart ({{cart}})</p>
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
    ],
    cart: 0
  }
});
```

> 화면에 `Add to Cart` 버튼과 `Cart (0)` 박스가 표시된다.

<br>

<br>

#### Event Handling 02

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
        
        <button v-on:click="cart += 1">Add to cart</button>
        
        <div class="cart">
          <p>Cart ({{cart}})</p>
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
    ],
    cart: 0
  }
});
```

> `Add to Cart` 버튼을 클릭할 때마다, `Cart (0)` 박스의 괄호 속 숫자가 1씩 증가한다.
>
> `v-on:` 디렉티브는 `@`로 단축할 수 있다.

<br>

<br>

#### Event Handling 03

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
        
        <button @click="addToCart">Add to cart</button>
        
        <div class="cart">
          <p>Cart ({{cart}})</p>
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
    ],
    cart: 0
  },
  methods: {
    addToCart() {
      this.cart += 1;
    }
  }
});
```

> 이전과 동일하게 동작한다.

<br>

<br>

#### Event Handling 04

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
          <p @mouseover="updateProduct(variant.variantImage)">{{ variant.variantColor }}</p>
        </div>
        
        <button @click="addToCart">Add to cart</button>
        
        <div class="cart">
          <p>Cart ({{cart}})</p>
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
        variantColor: 'black',
        variantImage: './assets/shoes-01.jpg'
      },
      {
        variantId: 2235,
        variantColor: 'yellow',
        variantImage: './assets/shoes-02.jpg'
      }
    ],
    cart: 0
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    }
  }
});
```

> `black`에 마우스를 올리면 `shoes-01.jpg`가 표시된다.
>
> `yellow`에 마우스를 올리면 `shoes-02.jpg`가 표시된다.

<br>

<br>