## Computed

<br>

#### Computed Properties 01

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
        <h1>{{ brand }} {{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        
        <div
             v-for="variant in variants"
             :key="variant.variantId"
             class="color-box"
             :style="{ backgroundColor: variant.variantColor }"
             @mouseover="updateProduct(variant.variantImage)">
        </div>
        
        <button
                @click="addToCart"
                :disabled="!inStock"
                :class="{ disabledButton: !inStock }">
          Add to cart
        </button>
        
        <div class="cart">
          <p>Cart ({{cart}})</p>
        </div>
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
    cart: 0,
    brand: 'Nike'
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

> `Shoes`가 `Nike Shoes`로 변경된다.

<br>

<br>

#### Computed Properties 02

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
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        
        <div
             v-for="variant in variants"
             :key="variant.variantId"
             class="color-box"
             :style="{ backgroundColor: variant.variantColor }"
             @mouseover="updateProduct(variant.variantImage)">
        </div>
        
        <button
                @click="addToCart"
                :disabled="!inStock"
                :class="{ disabledButton: !inStock }">
          Add to cart
        </button>
        
        <div class="cart">
          <p>Cart ({{cart}})</p>
        </div>
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
    cart: 0,
    brand: 'Nike'
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product;
    }
  }
});
```

> 이전과 동일하게 동작한다.

<br>

<br>

<br>

<br>

#### Refactor code

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
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        
        <div
             v-for="(variant, index) in variants"
             :key="variant.variantId"
             class="color-box"
             :style="{ backgroundColor: variant.variantColor }"
             @mouseover="updateProduct(index)">
        </div>
        
        <button
                @click="addToCart"
                :disabled="!inStock"
                :class="{ disabledButton: !inStock }">
          Add to cart
        </button>
        
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
    selectedVariant: 0,
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
    cart: 0,
    brand: 'Nike'
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(index) {
      this.selectedVariant = index;
      console.log(index);
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    }
  }
});
```

> `data`의 `image`를 `computed`로 이동시킨다.
>
> 이전과 동일하게 동작한다.

<br>

<br>

#### Computed Properties 03

- main.js

```js
var app = new Vue({
  el: '#app',
  data: {
    product: 'Shoes',
    selectedVariant: 0,
    details: ['80% cotton', '20% polyester', 'Gender-neutral'],
    variants: [
      {
        variantId: 2234,
        variantColor: 'black',
        variantImage: './assets/shoes-01.jpg',
        variantQuantity: 10
      },
      {
        variantId: 2235,
        variantColor: 'yellow',
        variantImage: './assets/shoes-02.jpg',
        variantQuantity: 0
      }
    ],
    cart: 0,
    brand: 'Nike'
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(index) {
      this.selectedVariant = index;
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    }
  }
});
```

> `data`의 `inStock`을 `computed`로 이동시킨다.
>
> 두 번째 상품은 개수가 0이므로 mouseover를 하면 `Out of Stock`과 `disabled`가 적용된다.

<br>

<br>