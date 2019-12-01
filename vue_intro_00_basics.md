#### 구조

```bash
vue-intro
  ├─ index.html
  ├─ style.css
  ├─ main.js
  ├─ favicon.ico
  └─ assets
       ├─ shoes-01.jpg
       └─ shoes-02.jpg
```

<br>

#### 프로젝트 생성

```bash
$ cd Desktop
$ mkdir vue-intro
$ cd vue-intro
$ touch index.html
$ touch style.css
$ touch main.js
$ mkdir assets
```

<br>

#### 코드 작성

- index.html

```html
<html>
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vue Intro</title>
    
    <!-- Favicon -->
    <link rel="shortcut icon" type="image/x-icon" sizes="16x16 32x32" href="./favicon.ico" />
    
    <!-- Fonts -->
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Ubuntu&display=swamp" />
    
    <!-- CSS -->
    <link rel="stylesheet" href="./style.css" />
  </head>
  
  <body>
    <!-- App -->
    <div id="app">
      <h1>What's up?</h1>
    </div>
    
    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    <script src="./main.js"></script>
  </body>
</html>
```

<br>

#### 서버 실행

```bash
$ cd vue-intro
$ live-server .
```

> 화면에 `What's up?`이 표시된다.

<br>

<br>

#### 집중을 위해 미리 CSS 작성

- style.css

```css
body {
  font-family: 'Ubuntu', sans-serif;
  color: #282828;
  margin: 0;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  width: 70%;
  border: 1px solid #d8d8d8;
  margin: 40px;
  box-shadow: 0 .5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  width: 50%;
  margin-top: 10px;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
  margin-right: 25px;
}

button {
  background-color: #1e95ea;
  color: #ffffff;
  font-size: 14px;
  width: 100px;
  height: 40px;
  border: none;
  margin-top: 30px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 400px;
  border: 1px solid #d8d8d8;
  padding: 20px;
  margin: 40px;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}

.tab {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
```

<br>

<br>