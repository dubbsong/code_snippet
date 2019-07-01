#### 구조

```bash
src
	├─ Components
	│		├─ App.js
	│		├─ Header.js
	│		├─ Router.js
	│		└─ GlobalStyles.js
	├─ Routes
	│		├─ Home.js
	│		├─ TV.js
	│		├─ Search.js
	│		└─ Detail.js
	└─ index.js
```

<br>

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

#### VSCode styled-components 설치

- `vscode-styled-components` 설치
  - 설치 후 백틱 내에서 CSS 자동완성

<br>

#### 코드 수정 (구조 변경)

- App.js

```react
import React, { Component } from 'react';
import Router from 'Components/Router';

class App extends Components {
  render() {
    return (
      <>
        <Router />
      </>
    );
  }
}

export default App;
```

<br>

- Header.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';

const Header = styled.header``;

const List = styled.ul``;

const Item = styled.li``;

const SLink = styled(Link)``;

export default () => (
  <Header>
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
  </Header>
);
```

<br>

- Router.js

```react
import React from 'react';
import { BrowserRouter as Router, Route, Redirect, Switch } from 'react-router-dom';
import Home from 'Routes/Home';
import TV from 'Routes/TV';
import Search from 'Routes/Search';
import Header from 'Components/Header';

export default () => (
  <Router>
    <>
      <Header />
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/tv" component={TV} />
        <Route path="/search" component={Search} />
        <Redirect from="*" to="/" />
      </Switch>
    </>
  </Router>
);
```

<br>

#### 파일 생성

```bash
$ cd src
$ cd Components
$ touch GlobalStyles.js
```

<br>

#### 코드 추가

- GlobalStyles.js

```react
import { createGlobalStyle } from 'styled-components';
import reset from 'styled-reset';

const globalStyles = createGlobalStyle`
	${reset}

	* {
		box-sizing: border-box;
	}

	body {
		font-family: -apple-system, ..., sans-serif;
		font-size: 16px;
		background-color: rgba(20, 20, 20, 1);
		color: #ffffff;
		padding-top: 50px;
	}

	a {
		text-decoration: none;
		color: inherit;
	}
`;

export default globalStyles;
```

<br>

- App.js

```react
import React, { Component } from 'react';
import Router from 'Components/Router';
import GlobalStyles from 'Components/GlobalStyles';

class App extends Component {
  render() {
    return (
      <>
        <Router />
        <GlobalStyles />
      </>
    );
  }
}

export default App;
```

<br>

- Header.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';

const Header = styled.header`
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 50px;
	background-color: rgba(20, 20, 20, 0.8);
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
	align-items: center;
	justify-content: center;
	height: 50px;
`;

export default () => (
  <Header>
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
  </Header>
);
```

<br>

#### Underbar 설정

- Header.js

```react
import React from 'react';
import { Link, withRouter } from 'react-router-dom';
import styled from 'styled-components';

const Header = styled.header`
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 50px;
	background-color: rgba(20, 20, 20, 0.8);
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
	border-bottom: 5px solid ${props => (props.current ? '#c9d6de' : 'transparent')};
	transition: border-bottom 0.2s ease-in-out;
`;

const SLink = styled(Link)`
	display: flex;
	align-items: center;
	justify-content: center;
	height: 50px;
`;

export default withRouter(({ location: { pathname } }) => (
  <Header>
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
  </Header>
));
```

------

<br>

<br>