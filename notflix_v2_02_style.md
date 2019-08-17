## Set GlobalStyle

1. 모든 속성 초기화
2. 기본 style 설정

<br>

<br>

###### styled-component 설치

```bash
$ yarn add styled-components
```

<br>

###### styled-reset 설치

```bash
$ yarn add styled-reset
```

<br>

###### 컴포넌트 생성

```bash
$ cd src
$ cd components
$ touch GlobalStyle.js
```

<br>

###### Style 설정

- GlobalStyle.js

```react
import { createGlobalStyle } from 'styled-components';
import reset from 'styled-reset';

const GlobalStyle = createGlobalStyle`
  ${reset}

  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Blinker', sans-serif;
    font-size: 14px;
    background-color: #141414;
    color: #ffffff;
  }

  a {
    text-decoration: none;
    color: inherit;
  }
`;

export default GlobalStyle;
```

- App.js

```react
...
import GlobalStyle from './GlobalStyle';

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <h2>오많배</h2>
        <GlobalStyle />
      </React.Fragment>
    );
  }
}

...
```

<br>

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set GlobalStyle'
$ git push origin master
```

<br>

<br>