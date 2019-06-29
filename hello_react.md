#### npx 설치

```bash
$ yarn global add npx
$ npm i npx -g
```

<br>

#### create-react-app 생성

```bash
$ cd Desktop
$ npx create-react-app hello_react
```

<br>

#### VSCode 열기

```bash
$ cd hello_react
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
<title>HELLO REACT</title>
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
        <h4>Hello React</h4>
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

<br>