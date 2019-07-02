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
  │   ├─ Poster.js
  │   └─ Message.js
  ├─ Routes
  │   ├─ Home
  │   │   ├─ index.js
  │   │   ├─ HomeContainer.js
  │   │   └─ HomePresenter.js
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
  │   └─ noPoster.png
  ├─ api.js
  └─ index.js
```

<br>

#### create-react-app 생성

```bash
$ cd Documents
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
      <div>
        <h4>오많배</h4>
      </div>
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

<br>

#### README 작성

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## Todo
[] Home
[] TV
[] Search
[] Detail
```

<br>

#### 저장소 생성 (for commit)

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

#### Components 폴더 생성

```bash
$ cd src
$ mkdir Components
```

<br>

#### 파일 이동

- `src/App.js` —> `src/Components/App.js`

<br>

#### 파일 생성

```bash
~/Desktop/notflix $ touch .env
```

<br>

#### 코드 추가

- .env

```bash
NODE_PATH=src
```

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from 'Components/App'

ReactDOM.render(<App />, document.getElementById('root'));
```

> 다시 `$ yarn start`
>
> `.env` 내의 `NODE_PATH=src`로 인해, `import App from 'Components/App'`이 동작한다.

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set Basics'
$ git push origin master
```

------

<br>

<br>