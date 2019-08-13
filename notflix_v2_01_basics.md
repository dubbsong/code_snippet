## Get Started

1. 프로젝트 생성
2. 기본 설정
3. 프로젝트 실행

<br>

<br>

###### 프로젝트 생성: `notflix`

```bash
$ cd Desktop
$ npx create-react-app notflix
```

<br>

###### VSCode 실행

```bash
$ cd notflix
$ code .
```

<br>

###### README 작성

```markdown
# NOTFLIX
- Learning React and ES6 by building a Movie App.

## Used
- ReactJS
- Styled Components
- Container & Presenter Pattern
- TMDB API

## Todo
- [] Movies
- [] TV Shows
- [] Search
- [] Each Detail

## Structure
src
  ├─ Components
  │   ├─ App.js
  │   ├─ GlobalStyle.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   ├─ Header
  │   ├─ Section.js
  │   ├─ Poster.js
  │   ├─ Loader.js
  │   ├─ Message.js
  │   └─ Footer.js
  ├─ Routes
  │   ├─ Movie
  │   │   ├─ index.js
  │   │   ├─ MovieContainer.js
  │   │   └─ MoviePresenter.js
  │   ├─ TV
  │   │   ├─ index.js
  │   │   ├─ TVContainer.js
  │   │   └─ TVPresenter.js
  │   ├─ Search
  │   │   ├─ index.js
  │   │   ├─ SearchContainer.js
  │   │   └─ SearchPresenter.js
  │   └─ Detail
  │       ├─ index.js
  │       ├─ DetailContainer.js
  │       └─ DetailPresenter.js
  ├─ api.js
  └─ index.js
```
<br>

###### favicon 추가

```bash
public
  └─ favicon.ico
```

<br>

###### 코드 추가 및 수정

- index.html

```html
...
<link href="https://fonts.googleapis.com/css?family=Blinker&display=swap" rel="stylesheet">
<title>Notflix</title>
...
```

<br>

###### 파일 제거

- src/App.css
- src/App.test.js
- src/index.css
- src/logo.svg
- src/serviceWorker.js

<br>

###### 환경 변수(environment variable) 생성: `.env`

```bash
~/Desktop/notflix $ touch .env
```

<br>

###### 환경 변수 설정

- \.env

```bash
NODE_PATH=src
```

<br>

###### 디렉토리 생성: `Components`

```bash
$ cd src
$ mkdir Components
```

<br>

###### 파일 이동

```bash
src
  └─ Components
      └─ App.js
```

<br>

###### 코드 수정

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from 'Components/App';

ReactDOM.render(<App />, document.getElementById('root'));
```

<br>

- App.js

```react
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <h2>오많배</h2>
      </React.Fragment>
    );
  }
}

export default App;
```

<br>

###### 프로젝트 실행

```bash
$ yarn start
```

> 화면에 `오많배`가 표시된다.

<br>

<br>

###### Repository 생성

1. https://github.com 이동
2. `Repositories` 탭 클릭
3. `New` 버튼 클릭
4. `Repository name` 기입
5. `Create repository` 버튼 클릭
6. `Terminal` 작성

```bash
$ cd notflix
$ git init
$ git add .
$ git commit -m '1st commit'
$ git remote add origin https://github.com/dubbsong/notflix.git
$ git push -u origin master
```

<br>

<br>