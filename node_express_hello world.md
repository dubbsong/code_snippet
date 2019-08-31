###### 디렉토리 생성

```bash
$ cd Desktop
$ mkdir express_helloworld
```

<br>

###### package.json 생성 및 작성

```bash
$ cd express_helloworld
$ npm init
```

> 대부분의 항목에서 Enter 키를 눌러 기본값을 수락한다.

<br>

###### Express 설치

```bash
$ npm install express --save
```

> package.json 내의 dependencies에 추가된다.

<br>

###### 파일 생성

```bash
$ touch app.js
```

<br>

###### 코드 작성

- app.js

```js
var express = require('express');
var app = express();

app.get('/', function(req, res) {
  res.send('Hello World');
});

app.listen(3000, function() {
  console.log('Listening on: http://localhost:3000');
});
```

<br>

###### 애플리케이션 실행

```bash
$ node app.js
```

> `http://localhost:3000`에 `Hello World`가 표시된다.

<br>

<br>