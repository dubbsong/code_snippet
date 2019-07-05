#### 디렉토리 구조

```bash
src
  ├─ index.js
  ├─ index.css
  ├─ App.js
  ├─ App.css
  ├─ MovieCard.js
  ├─ MovieCard.css
  ├─ MoviePoster.js
  └─ MoviePoster.css
```

<br>

#### create-react-app 생성

```bash
$ cd Documents
$ npx create-react-app movie_app
```

<br>

#### VSCode 열기

```bash
$ cd movie_app
$ code .
```

<br>

#### React 실행

```bash
$ cd movie_app
$ yarn start
```

> 정상적으로 작동한다.

<br>

#### 파일 제거

1. src/App.test.js
2. src/logo.svg
3. src/serviceWorker.js

<br>

#### 코드 수정

- public/index.html

```html
<title>Movie App</title>
```

<br>

- App.css

```css
/* 모든 코드 제거 */
```

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(<App />, document.getElementById('root'));
```

<br>

- App.js

```react
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div>
        <h2>What's up?</h2>
      </div>
    );
  }
}

export default App;
```

> 화면에 `What's up?`이 표시된다.

<br>

<br>

#### README 작성

- README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.

# Todo
[] test
[] test
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
$ cd movie_app
$ git init
$ git add .
$ git commit -m '1st commit'
$ git remote add origin https://github.com/dubbsong/movie_app.git
$ git push -u origin master
```

<br>

<br>

