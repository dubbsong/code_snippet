#### styled-components 설치

```bash
$ yarn add styled-components
```

<br>

#### styled-reset 설치

```bash
$ yarn add styled-reset
```

<br>

#### vscode-styled-components 설치

- VSCode 마켓에서 `vscode-styled-components`를 설치하면, 백틱 내에서 CSS 자동완성 기능이 동작한다.

<br>

#### 코드 수정

- Nav.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';

const Nav = styled.nav``;

const List = styled.ul``;

const Item = styled.li``;

const SLink = styled(Link)``;

export default () => (
  <Nav>
    <List>
      <Item>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item>
        <SLink to="/tv">TV</SLink>
      </Item>
      <Item>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
);
```

<br>

#### 구조 변경

- Router.js

```react
...
import {...} from 'react-router-dom';
import Nav from './Nav';
...

export default () => (
  <Router>
    <React.Fragment>
      <Nav />
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/tv" exact component={TV} />
        <Route path="/search" exact component={Search} />
        <Redirect from="*" to="/" />
      </Switch>
    </React.Fragment>
  </Router>
);
```

<br>

- App.js

```react
import React, { Component } from 'react';
import Router from './Router';

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <Router />
      </React.Fragment>
    );
  }
}

export default App;
```

<br>

#### 파일 생성 (GlobalStyle.js)

```bash
$ cd src
$ cd Components
$ touch GlobalStyle.js
```

<br>

#### 코드 추가

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
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    font-size: 16px;
    background-color: #1e2022;
    color: #f0f5f9;
    padding-top: 50px;
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

- Nav.js

```react
...

const Nav = styled.nav`
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 50px;
  background-color: #1e2022;
  box-shadow: 0 1px 5px 2px rgba(0, 0, 0, 0.8);
  z-index: 10;
`;

const List = styled.ul`
  display: flex;
`;

const Item = styled.li`
  text-align: center;
  width: 80px;
  height: 50px;
`;

const SLink = styled(Link)`
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
`;

...
```

<br>

#### Underbar 설정 (Nav.js)

- underbar 확인 (on TV)

```react
...

const Item = styled.li`
  text-align: center;
  width: 80px;
  height: 50px;
  border-bottom: 5px solid
    ${props => (props.current ? '#c9d6de' : 'transparent')};
`;

...

export default () => (
  <Nav>
    <List>
      <Item current={false}>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item current={true}>
        <SLink to="/tv">TV</SLink>
      </Item>
      <Item current={false}>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
);
```

<br>

- pathname 확인

```react
...
import { Link, withRouter } from 'react-router-dom';
import styled from 'styled-components';

...

const Item = styled.li`
  text-align: center;
  width: 80px;
  height: 50px;
  border-bottom: 5px solid
    ${props => (props.current ? '#c9d6de' : 'transparent')};
`;

...

export default withRouter(props => (
  <Nav>
    {console.log(props)}
    <List>
      <Item current={true}>
        <SLink to="/">Movies</SLink>
      </Item>
      <Item current={true}>
        <SLink to="/tv">TV</SLink>
      </Item>
      <Item current={false}>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
));
```

> `location`에서 `pathname`을 확인할 수 있다.

<br>

- props 전달

```react
...

const Item = styled.li`
  text-align: center;
  width: 80px;
  height: 50px;
  border-bottom: 5px solid
    ${props => (props.current ? '#c9d6de' : 'transparent')};
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
        <SLink to="/tv">TV</SLink>
      </Item>
      <Item current={pathname === '/search'}>
        <SLink to="/search">Search</SLink>
      </Item>
    </List>
  </Nav>
));
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

------

<br>

<br>