###### 라우트 정의 구조

```js
app.METHOD(PATH, HANDLER)
```

> `app`: express의 인스턴스
>
> `METHOD`: HTTP 요청 메소드
>
> `PATH`: 서버에서의 경로
>
> `HANDLER`: 라우트가 일치할 때 실행되는 함수

<br>

<br>

###### 디렉토리 생성

```bash
$ cd Desktop
$ mkdir test_routing
```

<br>

###### VSCode 실행

```bash
$ cd test_routing
$ code .
```

<br>

###### package.json 생성 및 작성

```bash
$ npm init
```

> 모든 항목에서 Enter를 눌러 기본값을 수락한다.

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
  res.send('Test Routing');
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

> `http://localhost:3000`에 `Test Routing`이 표시된다.

<br>

<br>

###### 라우트 정의 설명

1. `get`

```js
app.get('/', function(req, res) {
  res.send('Hello World');
});
```

> 홈에서 Hello World로 응답

<br>

2. `post`

```js
app.post('/', function(req, res) {
  res.send('Got a POST request');
});
```

> 루트 라우트(/)에서 POST 요청에 응답

<br>

3. `put`

```js
app.put('/user', function(req, res) {
  res.send('Got a PUT request at /user');
});
```

> /user 라우트에 대한 PUT 요청에 응답

<br>

4. `delete`

```js
app.delete('/user', function(req, res) {
  res.send('Got a DELETE request at /user');
});
```

> /user 라우트에 대한 DELETE 요청에 응답

<br>

<br>