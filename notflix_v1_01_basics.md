###### 프로젝트 생성: `notflix`

```bash
$ cd Documents
$ cd laboratory
$ npx create-react-app notflix
```

<br>

###### VSCode 실행

```bash
$ cd notflix
$ code .
```

<br>

###### 파일 제거

```bash
src
  ├─ App.css
  ├─ App.test.js
  ├─ index.css
  ├─ logo.svg
  └─ serviceWorker.js
```

<br>

###### 코드 작성

- index.html

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
        <h4>NOTFLIX Movie App</h4>
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

> 화면에 `NOTFLIX Movie App`이 표시된다.

<br>

###### README 작성

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

###### 디렉토리 생성: `Components`

```bash
$ cd src
$ mkdir Components
```

<br>

###### 파일 이동

```bash
src
  ├─ Components
  │   └─ App.js
  └─ index.js
```

<br>

###### 경로 수정

- index.js

```react
...
import App from './Components/App';

...
```

> 화면에 `NOTFLIX Movie App`이 표시된다.

<br>

<br>

###### 현재 디렉토리 구조

```bash
src
  ├─ Components
  │   └─ App.js
  └─ index.js
```

<br>

<br>