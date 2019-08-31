###### 디렉토리 생성

```bash
$ cd Desktop
$ mkdir test_express
```

<br>

###### VSCode 실행

```bash
$ cd test_express
$ code .
```

<br>

###### package.json 생성

```bash
$ npm init
```

> 모든 항목에서 Enter 키를 눌러 기본값을 수락한다.

<br>

###### Express 설치

```bash
$ npm install express --save
```

> package.json 내의 dependencies에 express가 추가된다.

<br>

###### 파일 생성

```bash
$ touch server.js
```

<br>

###### 코드 작성

- server.js

```js
var express = require('express');
var app = express();

var server = app.listen(3000, function() {
  console.log('Express server has started on: http://localhost:3000');
});
```

<br>

###### 서버 실행

```bash
$ node server.js
```

> `http://localhost:3000`에 `Cannot GET /`이 표시된다.
>
> 아직 Router를 설정하지 않았기 때문이다.

<br>

###### 코드 추가 후 다시 실행

- server.js

```js
var express = require('express');
var app = express();

app.get('/', function(req, res) {
  res.send('OMB');
});

var server = app.listen(3000, function() {
  console.log('Express server has started on: http://localhost:3000');
});
```

> `http://localhost:3000`에 `OMB`가 표시된다.

<br>

<br>

## 여기서부터 다시

###### 디렉토리 생성

```bash
$ mkdir router
$ mkdir views
```

<br>

###### 파일 생성

```bash
$ cd views
$ touch index.html
$ touch about.html
```

```bash
$ cd ..
$ cd router
$ touch main.js
```

<br>

###### 코드 작성

- index.html

```html
<html>
  <head>
    <title>Main</title>
    <link rel="stylesheet" href="css/style.css">
  </head>
  <body>
    <h2>Index</h2>
  </body>
</html>
```

- about.html

```html
<html>
  <head>
    <title>About</title>
    <link rel="stylesheet" href="css/style.css">
  </head>
  <body>
    <h2>About</h2>
  </body>
</html>
```

- main.js

```js
module.exports = function(app) {
  app.get('/', function(req, res) {
    res.render('index.html');
  });
  
  app.get('/about', function(req, res) {
    res.render('about.html');
  });
}
```

- server.js

```js
var express = require('express');
var app = express();
var router = require('./router/main')(app);

app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.engine('html', require('ejs').renderFile);

var server = app.listen(3000, function() {
  console.log('Express server has started on: http://localhost:3000');
});
```

<br>

###### 서버 다시 실행

```bash
$ node server.js
```

> 

<br>

<br>