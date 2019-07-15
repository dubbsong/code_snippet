#### styled-components 설치

```bash
$ yarn add styled-components
```

> VSCode 마켓에서 `vscode-styled-components`를 설치하면, 백틱 내에서 CSS 자동완성 기능이 동작한다.

<br>

#### styled-reset 설치

```bash
$ yarn add styled-reset
```

<br>

#### 컴포넌트 생성: `GlobalStyle`

```bash
$ cd src
$ cd Components
$ touch GlobalStyle.js
```

<br>

#### CSS 초기화 & Global CSS 설정

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
    font-family: 'Ubuntu', sans-serif;
    font-size: 0.8rem;
    background-color: #141414;
    color: #ffffff;
    padding: 80px 5%;
  }

  a {
    text-decoration: none;
    color: inherit;
  }
`;

export default globalStyle;
```

<br>

- App.js

```react
...
import GlobalStyle from './GlobalStyle';

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <Router />
        <GlobalStyle />
      </React.Fragment>
    );
  }
}

...
```

<br>

#### 사용자 정의 컴포넌트로 변경

- Nav.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';

const Nav = styled.nav`
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 70px;
  background-color: #141414;
  box-shadow: 0 1px 10px 2px rgba(0, 0, 0, 0.8);
  z-index: 10;
`;

const List = styled.ul`
  display: flex;
`;

const Item = styled.li`
  width: 70px;
  height: 70px;
  text-align: center;
`;

const SLink = styled(Link)`
  display: flex;
  justify-content: center;
  align-items: center;
  height: 70px;
`;

export default () => (
  <Nav>
    <List>
      <Item>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item>
        <SLink to="/tv">TV Shows</SLink>
      </Item>
      <Item>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
);
```

<br>

<br>

#### Underbar CSS 설정: `Nav`

- pathname 확인

```react
...
import { Link, withRouter } from 'react-router-dom';
...

...

export default withRouter(props => (
  <Nav>
    {console.log(props)}
    <List>
      <Item current={true}>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item current={true}>
        <SLink to="/tv">TV Shows</SLink>
      </Item>
      <Item current={false}>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
));
```

> Console 탭의 `location`에서 `pathname`을 확인할 수 있다.

<br>

- props 전달

```react
...

const Item = styled.li`
  ...
  border-bottom: 2px solid
    ${props => (props.current ? '#e5e5e5' : 'transparent')};
  transition: border-bottom 0.2s ease-in-out;
`;

...

export default withRouter(({ location: { pathname } }) => (
  <Nav>
    <List>
      <Item current={pathname === '/'}>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item current={pathname === '/tv'}>
        <SLink to="/tv">TV Shows</SLink>
      </Item>
      <Item current={pathname === '/search'}>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
));
```

<br>

<br>

#### 디렉토리 생성: `assets`, `img`

```bash
$ cd src
$ mkdir assets
$ cd assets
$ mkdir img
```

<br>

#### 이미지 추가: `logo.png`

```bash
assets
  └─ img
      └─ logo.png
```

<br>

#### logo 설정

- Nav.js

```react
...
import logo from 'assets/img/logo.png';

const Nav = styled.nav`
  display: flex;
  align-items: center;
  ...
  padding: 0 4%;
`;

const Logo = styled.img`
  width: 120px;
  height: 45px;
`;

...

export default withRouter(({ location: { pathname } }) => (
  <Nav>
    <SLink to="/">
      <Logo src={logo} alt="" />
    </SLink>
    <List>
      ...
    </List>
  </Nav>
));
```

<br>

<br>

#### react-fontawesome 설치

```bash
$ yarn add @fortawesome/fontawesome-svg-core
$ yarn add @fortawesome/free-solid-svg-icons
$ yarn add @fortawesome/react-fontawesome
```

<br>

#### `Search`를 `🔍`로 변경

- Nav.js

```react
...
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faSearch } from '@fortawesome/free-solid-svg-icons';

...

const Item = styled.li`
  ...
  :last-child {
    width: 50px;
  }
`;

...

export default withRouter(({ location: { pathname } }) => (
  <Nav>
    ...
    <List>
      ...
      <Item current={pathname === '/search'}>
        <SLink to="/search">
          <FontAwesomeIcon icon={faSearch} />
        </SLink>
      </Item>
    </List>
  </Nav>
));
```

> `Search` 탭이 `🔍` 아이콘으로 변경된다.

<br>

<br>

#### 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   └─ GlobalStyle.js
  ├─ Routes
  │   ├─ Movie.js
  │   ├─ TV.js
  │   ├─ Search.js
  │   └─ Detail.js
  ├─ assets
  │   └─ img
  │       └─ logo.png
  └─ index.js
```

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set CSS'
$ git push origin master
```

<br>

<br>