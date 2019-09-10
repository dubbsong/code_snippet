###### 디렉토리 \& 파일 생성

```bash
$ cd Desktop
$ mkdir test
$ cd test
$ touch app.js
```

<br>

###### Express 설치

```bash
$ npm i express
```

<br>

###### 코드 작성

```js
// app.js

const express = require('express');
const app = express();

app.get('', (req, res) => {
  res.send('Hello Express')
});

app.get('/about', (req, res) => {
  res.send('This is About page')
});

app.listen(3000, () => {
  console.log('Server is up on http://localhost:3000');
});
```

<br>

###### 서버 실행

```bash
$ node app.js
Server is up on http://localhost:3000
```

> `http://localhost:3000`에 접속하면 `Hello Express`가 표시된다.
>
> `http://localhost:3000/about`에 접속하면 `This is About page`가 표시된다.

<br>

<br>