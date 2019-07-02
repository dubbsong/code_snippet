#### react-router-dom 설치

```bash
$ yarn add react-router-dom
```

<br>

#### Routes 폴더 생성

```bash
$ cd src
$ mkdir Routes
```

<br>

#### 파일 생성 (Home, TV, Search, Detail)

```bash
$ cd Routes
$ touch Home.js
$ touch TV.js
$ touch Search.js
$ touch Detail.js
```

<br>

#### 코드 추가

- Home.js

```react
export default () => 'Home';
```

- TV.js

```react
export default () => 'TV';
```

- Search.js

```react
export default () => 'Search';
```

- Detail.js

```react
export default () => 'Detail';
```

<br>

#### 파일 생성 (Router.js)

```bash
$ cd src
$ cd Components
$ touch Router.js
```

<br>

#### 코드 추가

- Router.js

```react
import React from 'react';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import Home from 'Routes/Home';
import TV from 'Routes/TV';
import Search from 'Routes/Search';

export default () => (
  <Router>
    <React.Fragment>
      <Route path="/" exact component={Home} />
      <Route path="/tv" component={TV} />
      <Route path="/tv/popular" render={() => <h4>Popular Show</h4>} />
      <Route path="/search" component={Search} />
    </React.Fragment>
  </Router>
);
```

<br>

- App.js

```react
import React, { Component } from 'react';
import Router from 'Components/Router';

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

> `localhost:3000`: Home
>
> `localhost:3000/tv`: TV
>
> `localhost:3000/tv/popular`: Popular Show
>
> `localhost:3000/search`: Search

<br>

#### 파일 생성 (Nav.js)

```bash
$ cd src
$ cd Components
$ touch Nav.js
```

<br>

#### 코드 추가

- Nav.js

```react
import React from 'react';

export default () => (
  <nav>
    <ul>
      <li>
        <a href="/">Movies</a>
      </li>
      <li>
        <a href="/tv">TV</a>
      </li>
      <li>
        <a href="/search">Search</a>
      </li>
    </ul>
  </nav>
);
```

<br>

- App.js

```react
import React, { Component } from 'react';
import Router from 'Components/Router';
import Nav from 'Components/Nav';

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <Nav />
        <Router />
      </React.Fragment>
    );
  }
}

export default App;
```

> Nav의 각 Movies, TV, Search를 클릭해서 페이지를 이동할 수 있다.

<br>

#### Redirect 설정

- Router.js

```react
import React from 'react';
import {
  BrowserRouter as Router,
  Route,
  Redirect,
  Switch
} from 'react-router-dom';
import Home from 'Routes/Home';
import TV from 'Routes/TV';
import Search from 'Routes/Search';

export default () => (
  <Router>
    <Switch>
      <Route path="/" exact component={Home} />
      <Route path="/tv" component={TV} />
      <Route path="/search" component={Search} />
      <Redirect from="*" to="/" />
    </Switch>
  </Router>
);
```

> `localhost:3000` 뒤에 `/asdfjlas;df`와 같이 무작위 입력을 하면, Home으로 Redirect 한다.

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set Router'
$ git push origin master
```

------

<br>

<br>