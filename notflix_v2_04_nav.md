###### 컴포넌트 생성: `Nav`

```bash
$ cd src
$ cd Components
$ touch Nav.js
```

<br>

###### Nav 설정

- Nav.js

```react
import React from 'react';
import styled from 'styled-components';
import { Link } from 'react-router-dom';

const Nav = styled.nav``;

const List = styled.ul``;

const Item = styled.li``;

const StyledLink = styled(Link)``;

export default () => (
  <Nav>
    <List>
      <Item>
        <StyledLink to="/">Movies</StyledLink>
      </Item>
      <Item>
        <StyledLink to="/tv">TV Shows</StyledLink>
      </Item>
      <Item>
        <StyledLink to="/search">Search</StyledLink>
      </Item>
    </List>
  </Nav>
);
```

- Router.js

```react
...
import Nav from './Nav';

export default () => (
  <Router>
    <React.Fragment>
      <Nav />
      <Switch>
        ...
      </Switch>
    </React.Fragment>
  </Router>
);
```

<br>

###### CSS 설정

- Nav.js

```react
...

const Nav = styled.nav`
  position: fixed;
  top: 0;
  left: 0;
  background-color: #20a19c;
  width: 100%;
  height: 68px;
`;

const List = styled.ul`
  display: flex;
`;

const Item = styled.li`
  width: 68px;
  height: 68px;
  text-align: center;
`;

const SLink = styled(Link)`
  display: flex;
  justify-content: center;
  align-items: center;
  height: 68px;
`;

...
```

- GlobalStyle.js

```react
...

const globalStyle = createGlobalStyle`
  ...

  body {
    ...
    padding-top: 70px;
  }

  ...
`;

...
```

<br>

<br>

###### 디렉토리 생성: `assets`

```bash
$ cd src
$ mkdir assets
```

<br>

###### 이미지 추가: `logo.png`

```bash
assets
  └─ logo.png
```

<br>

###### logo 설정

- Nav.js

```react
...
import logo from 'assets/logo.png';

const Nav = styled.nav`
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 68px;
  display: flex;
  align-items: center;
  padding: 0 4%;
  z-index: 10;

  @media (max-width: 768px) {
    justify-content: space-between;
  }
`;

const Logo = styled.img`
  width: 90px;
`;

const List = styled.ul`
  ...
  margin-left: 10px;
`;

const Item = styled.li`
  ...
  margin-left: 8px;

  @media (max-width: 576px) {
    margin: 0;
  }
`;

const StyledLink = styled(Link)`
  ...
`;

export default () => (
  <Nav>
    <StyledLink to="/">
      <Logo src={logo} alt="" />
    </StyledLink>
    <List>
      ...
    </List>
  </Nav>
);
```

> `background-color: #20a19c;` 제거

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

  &:last-child {
    width: 50px;
  }

  @media (max-width: 576px) {...}
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

###### withRouter 확인

- Nav.js

```react
...
import { Link, withRouter } from 'react-router-dom';
...

...

export default withRouter(props => (
  <Nav>
    {console.log(props)}
    ...
  </Nav>
));
```

> 1. 개발자 도구 `Console` 탭으로 이동
> 2. `location`의 `pathname` 확인

<br>

###### active 설정

- Nav.js

```react
...
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faSearch } from '@fortawesome/free-solid-svg-icons';

...

const Item = styled.li`
  ...

  color: ${props => (props.current ? '#ffffff' : '#b3b3b3')};

  @media (max-width: 576px) {...}
`;

const StyledLink = styled(Link)`
  ...
  transition: color 0.2s ease-in-out;

  &:hover {
    color: #ffffff;
  }
`;

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