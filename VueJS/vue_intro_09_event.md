## Communicating Events

<br>

#### Event 01

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <div class="cart">
      <p>Cart ({{cart}})</p>
    </div>
    <product :premium="premium" @add-to-cart="updateCart"></product>
  </div>
</body>
```

- main.js

```js
Vue.component('product', {
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  template: `
  <div class="product">
    <div class="product-image">
      <img :src="image" alt="" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
      <p>Shipping: {{ shipping }}</p>

      <ul>
        <li v-for="detail in details">{{ detail }}</li>
      </ul>

      <div
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        class="color-box"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>

      <button
        @click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Add to cart
      </button>
    </div>
  </div>
  `,
  data() {
    return {
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
      brand: 'Nike'
    };
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart');
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
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return 'Free';
      }
      return 2.99;
    }
  }
});

// Vue Instance
var app = new Vue({
  el: '#app',
  data: {
    premium: true,
    cart: 0
  },
  methods: {
    updateCart() {
      this.cart += 1;
    }
  }
});
```

> JS의 `cart` div를 HTML로 이동시킨다.
>
> `data()`의 `cart: 0`을 Vue Instance의 `data`로 이동시킨다.

<br>

<br>

#### Event 02

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <div class="cart">
      <p>Cart ({{cart.length}})</p>
    </div>
    <product :premium="premium" @add-to-cart="updateCart"></product>
  </div>
</body>
```

- main.js

```js
Vue.component('product', {
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  template: `
  <div class="product">
    <div class="product-image">
      <img :src="image" alt="" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
      <p>Shipping: {{ shipping }}</p>

      <ul>
        <li v-for="detail in details">{{ detail }}</li>
      </ul>

      <div
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        class="color-box"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>

      <button
        @click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Add to cart
      </button>
    </div>
  </div>
  `,
  data() {
    return {
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
      brand: 'Nike'
    };
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart');
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
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return 'Free';
      }
      return 2.99;
    }
  }
});

// Vue Instance
var app = new Vue({
  el: '#app',
  data: {
    premium: true,
    cart: []
  },
  methods: {
    updateCart(id) {
      this.cart.push(id)
    }
  }
});
```

> JS의 `cart` div를 HTML로 이동시킨다.
>
> `data()`의 `cart: 0`을 Vue Instance의 `data`로 이동시킨다.

<br>

<br>