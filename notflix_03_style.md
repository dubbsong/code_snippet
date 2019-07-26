###### styled-components 설치

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

###### 기본 CSS 설정

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
    padding-top: 80px;
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

<br>

###### styled-components 적용: `Nav`

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

> `{ Link }`로 인해, 페이지 이동 시에도 `refresh` 되지 않는다.

<br>

<br>

###### 디렉토리 생성: `assets` / `img`

```bash
$ cd src
$ mkdir assets
$ cd assets
$ mkdir img
```

<br>

###### 이미지 파일 추가: `logo.png`

```bash
assets
  └─ img
      └─ logo.png
```

<br>

###### logo 설정

- Nav.js

```react
...
import logo from '../assets/img/logo.png';

const Nav = styled.nav`
  ...
  display: flex;
  align-items: center;
  padding: 0 20px;

	@media (max-width: 768px) {
		padding: 0 5px;
		justify-content: space-between;
	}
`;

const Logo = styled.img`
  width: 120px;
  height: 45px;
`;

...

export default () => (
  <Nav>
    <SLink to="/">
      <Logo src={logo} alt="" />
    </SLink>
    <List>
      ...
    </List>
  </Nav>
);
```

<br>

<br>

###### react-fontawesome 설치

```bash
$ yarn add @fortawesome/fontawesome-svg-core
$ yarn add @fortawesome/react-fontawesome
$ yarn add @fortawesome/free-solid-svg-icons
```

<br>

###### faSearch 아이콘 설정

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

export default () => (
  <Nav>
    ...
    <List>
      ...
      <Item>
        <SLink to="/search">
          <FontAwesomeIcon icon={faSearch} />
        </SLink>
      </Item>
    </List>
  </Nav>
);
```

<br>

<br>

###### underbar 설정: `Nav`

1. props 확인

```react
...
import { Link, withRouter } from 'react-router-dom';
...

...

export default withRouter(props => (
  <Nav>
    {console.log(props)}
    <SLink to="/">
      ...
    </SLink>
    <List>
      ...
    </List>
  </Nav>
));
```

> `location`에서 `pathname`을 확인할 수 있다.

<br>

2. props 전달

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
    ...
    <List>
      <Item current={pathname === '/'}>
        ...
      </Item>
      <Item current={pathname === '/tv'}>
        ...
      </Item>
      <Item current={pathname === '/search'}>
        ...
      </Item>
    </List>
  </Nav>
));
```

<br>

<br>

###### 현재 디렉토리 구조

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

<br>