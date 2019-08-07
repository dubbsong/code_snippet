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
- Container & Presenter Pattern
- Styled Components

## Todo
- [] Movies
- [] TV Shows
- [] Search
- [] Detail
```

<br>

###### favicon 추가

```bash
public
  └─ favicon.ico
```

<br>

###### 코드 추가

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

###### 코드 수정 및 작성

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

###### 서버 실행

```bash
$ yarn start
```

> 화면에 `오많배`가 표시된다.

<br>

<br>