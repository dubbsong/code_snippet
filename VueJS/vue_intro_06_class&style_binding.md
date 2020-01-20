## :class \& :style

<br>

#### class \& style Binding 01

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
        
        <div
             v-for="variant in variants"
             :key="variant.variantId"
             class="color-box"
             :style="{ backgroundColor: variant.variantColor }"
             @mouseover="updateProduct(variant.variantImage)">
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

> `black`과 `yellow` 텍스트 대신, 각 색상을 가진 `color-box`가 표시된다.
>
> 이전과 동일하게 동작한다.

<br>

<br>

#### class \& style Binding 02

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

- Chrome Console

```js
app.inStock = false;
```

> `inStock: false`의 경우, `Add to Cart` 버튼이 `disabled`로 표시된다.

<br>

<br>