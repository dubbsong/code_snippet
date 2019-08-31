###### 바탕화면으로 이동

```bash
$ cd Desktop
```

<br>

###### express generator 전역 설치

```bash
$ sudo npm install express-generator -g
```

<br>

###### 명령 옵션 표시

```bash
$ express -h
```

<br>

###### express 애플리케이션 생성

```bash
$ express --view=pug test_generator
```

<br>

###### VSCode 실행

```bash
$ cd test_generator
$ code .
```

<br>

###### 종속 항목 설치

```bash
$ cd test_generator
$ npm install
```

<br>

###### 애플리케이션 실행

```bash
$ DEBUG=test_generator:* npm start
```

> `http:localhost:3000`에 `Express Welcome to Express`가 표시된다.

<br>

###### 구조

```bash
.
├── app.js
├── bin
│   └── www
├── package.json
├── package-lock.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug
```

<br>

<br>