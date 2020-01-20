## Component

- Components are reusable blocks of code that are used to create a more modular and maintainable code base.
  - 컴포넌트는 재사용이 가능한 코드 블록이다.
  - 컴포넌트는 모듈식이며, 유지보수가 용이한 코드 베이스를 작성하는 데 사용된다.
- How can a component access outside data?
  - 컴포넌트는 어떻게 외부 데이터에 액세스할 수 있을까?
- A prop is a custom attribute for passing data in components.
  - prop은 컴포넌트에 데이터를 전달하기 위한 사용자 정의 속성이다.

<br>

#### Component 01 (기존의 코드를 변경)

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <product></product>
    <product></product>
  </div>
</body>
```

> `App`의 모든 내용을 JS의 `template`으로 이동시키고, `<product></product>` 컴포넌트를 작성한다.

- main.js

```js
Vue.component('product', {
  template: `
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
        @mouseover="updateProduct(index)"
      ></div>

      <button
        @click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Add to cart
      </button>

      <div class="cart">
        <p>Cart ({{cart}})</p>
      </div>
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
      cart: 0,
      brand: 'Nike'
    };
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
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    }
  }
});

// Vue Instance
var app = new Vue({
  el: '#app'
});
```

> `data:`를 `data()`로 변경한다.
>
> 이전과 동일하게 동작한다.

<br>

<br>

#### Component 02 (prop 설정)

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <product :premium="premium"></product>
    <product></product>
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
      <p>User is premium: {{ premium }}</p>

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

      <div class="cart">
        <p>Cart ({{cart}})</p>
      </div>
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
      cart: 0,
      brand: 'Nike'
    };
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
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    }
  }
});

// Vue Instance
var app = new Vue({
  el: '#app',
  data: {
    premium: true
  }
});
```

> `User is premium: true`가 표시된다.

<br>

<br>

#### Component 03

- index.html

```html
<body>
  <!-- Nav -->
  <div class="nav-bar"></div>
  
  <!-- App -->
  <div id="app">
    <product :premium="premium"></product>
    <product></product>
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

      <div class="cart">
        <p>Cart ({{cart}})</p>
      </div>
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
      cart: 0,
      brand: 'Nike'
    };
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
    premium: true
  }
});
```

> `premium: true`인 경우  `Shipping: Free`로 표시된다.
>
> `premium: false`인 경우  `Shipping: 2.99`로 표시된다.

<br>

<br>

