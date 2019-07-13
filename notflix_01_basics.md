#### 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   ├─ GlobalStyle.js
  │   ├─ Section.js
  │   ├─ Loader.js
  │   ├─ Message.js
  │   └─ Poster.js
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
  ├─ assets
  │   └─ img
  │       ├─ logo.png
  │       └─ noPoster.png
  ├─ api.js
  └─ index.js
```

<br>

#### 프로젝트 생성

```bash
$ cd Documents
$ cd deploying
$ npx create-react-app notflix
```

<br>

#### VSCode 열기

```bash
$ cd notflix
$ code .
```

<br>

#### 파일 제거

1. src/App.css
2. src/App.test.js
3. src/index.css
4. src/logo.svg
5. src/serviceWorker.js

<br>

#### 코드 수정

- public/index.html

```html
<link href="https://fonts.googleapis.com/css?family=Ubuntu&display=swap" rel="stylesheet">
<title>NOTFLIX</title>
```

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

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
        <h4>NOTFLIX</h4>
      </React.Fragment>
    );
  }
}

export default App;
```

<br>

#### React 실행

```bash
$ yarn start
```

> 화면에 `NOTFLIX`가 표시된다.

<br>

#### README 작성

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## TODO
- [] Movie
- [] TV
- [] Search
- [] Detail
```

<br>

#### Repository 생성

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

#### 파일 생성

```bash
~/Documents/deploying/notflix $ touch .env
```

<br>

#### 코드 작성

- .env

```bash
NODE_PATH=src
```

> 경로를 작성할 때, `src/`를 생략할 수 있다.

<br>

#### 디렉토리 생성

```bash
$ cd src
$ mkdir Components
```

<br>

#### 파일 이동

- `src/App.js` => `src/Components/App.js`

```bash
src
  ├─ index.js
  └─ Components
      └─ App.js
```

<br>

#### 경로 수정

- index.js

```react
...
import App from 'Components/App';

...
```

> 다시 `$ yarn start`
>

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set Basics'
$ git push origin master
```

<br>

<br>