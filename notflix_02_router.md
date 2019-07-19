#### react-router-dom 설치

```bash
$ yarn add react-router-dom
```

<br>

#### 디렉토리 생성: `Routes`

```bash
$ cd src
$ mkdir Routes
```

<br>

#### 컴포넌트 생성: `Movie`, `TV`, `Search`, `Detail`

```bash
$ cd Routes
$ touch Movie.js
$ touch TV.js
$ touch Search.js
$ touch Detail.js
```

<br>

#### 코드 추가: `only export`

- Movie.js

```react
export default () => 'You will see movies';
```

- TV.js

```react
export default () => 'You will see tv shows';
```

- Search.js

```react
export default () => 'You will see search input';
```

- Detail.js

```react
export default () => 'You will see detail page';
```

<br>

<br>

#### 컴포넌트 생성: `Router`

```bash
$ cd src
$ cd Components
$ touch Router.js
```

<br>

#### Route 설정

- Router.js

```react
import React from 'react';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import Movie from 'Routes/Movie';
import TV from 'Routes/TV';
import Search from 'Routes/Search';
import Detail from 'Routes/Detail';

export default () => (
  <Router>
    <React.Fragment>
      <Route path="/" exact component={Movie} />
      <Route path="/tv" component={TV} />
      <Route path="/search" component={Search} />
      <Route path="/movie/:id" component={Detail} />
      <Route path="/show/:id" component={Detail} />
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

> `localhost:3000`: You will see movies
>
> `localhost:3000/tv`: You will see tv shows
>
> `localhost:3000/search`: You will see search input
>
> `localhost:3000/movie/121`: You will see detail page
>
> `localhost:3000/show/121`: You will see detail page
>
> `localhost:3000/show/abc`: You will see detail page

<br>

#### Redirect 설정

- Router.js

```react
...
import {
  BrowserRouter as Router,
  Route,
  Switch,
  Redirect
} from 'react-router-dom';
...

export default () => (
  <Router>
    <React.Fragment>
      <Switch>
        ...
        <Route path="/show/:id" component={Detail} />
        <Redirect from="*" to="/" />
      </Switch>
    </React.Fragment>
  </Router>
);
```

> `localhost:3000` 뒤에 `/asdfjlas;df`와 같이 무작위 입력을 하면, Movies로 Redirect 한다.

<br>

<br>

#### 컴포넌트 생성: `Nav`

```bash
$ cd src
$ cd Components
$ touch Nav.js
```

<br>

#### Route 연결

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
        <a href="/tv">TV Shows</a>
      </li>
      <li>
        <a href="/search">Search</a>
      </li>
    </ul>
  </nav>
);
```

<br>

- Router.js

```react
...
import Nav from './Nav';
...

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

> 클릭으로 페이지를 이동할 수 있게 된다.
>
> 하지만 클릭할 때마다 새로고침된다.

<br>

<br>

#### 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   └─ Nav.js
  ├─ Routes
  │   ├─ Movie.js
  │   ├─ TV.js
  │   ├─ Search.js
  │   └─ Detail.js
  └─ index.js
```

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set Router'
$ git push origin master
```

<br>

<br>