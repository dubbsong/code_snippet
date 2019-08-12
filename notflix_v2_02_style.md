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

###### 컴포넌트 생성: `GlobalStyle`

```bash
$ cd src
$ cd Components
$ touch GlobalStyle.js
```

<br>

###### Basic CSS 설정

- GlobalStyle.js

```react
import { createGlobalStyle } from 'styled-components';
import reset from 'styled-reset';

const globalStyle = createGlobalStyle`
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

export default globalStyle;
```

> `${reset}`: 모든 CSS 속성을 초기화한다.
>
> `etc`: 필요한 기본 속성을 설정한다.

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