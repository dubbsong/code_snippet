#### create-react-app 생성

```bash
$ cd Desktop
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
Learning React and ES6 by building a Movie Discovery App.

## Screens
- [] Home
- [] TV
- [] Search
- [] Detail
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
```

> 다시 `$ yarn start`
>
> `.env` 내의 `NODE_PATH=src`로 인해, `import App from 'Components/App'`이 동작한다.

------

<br>

<br>