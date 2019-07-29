###### react-router-dom 설치

```bash
$ yarn add react-router-dom
```

<br>

###### 디렉토리 생성: `Routes`

```bash
$ cd src
$ mkdir Routes
```

<br>

###### 컴포넌트 생성: `Movie` / `TV` / `Search` / `Detail`

```bash
$ cd Routes
$ touch Movie.js
$ touch TV.js
$ touch Search.js
$ touch Detail.js
```

<br>

###### 코드 작성

- Movie.js

```react
export default () => 'Movies Area';
```

- TV.js

```react
export default () => 'TV Shows Area';
```

- Search.js

```react
export default () => 'Search Input and Results Area';
```

- Detail.js

```react
export default () => 'Each Detail Area';
```

> `import` 없이 텍스트만 `export` 한다.

<br>

###### 컴포넌트 생성: `Router`

```bash
$ cd src
$ cd Components
$ touch Router.js
```

<br>

###### Route 설정

- Router.js

```react
import React from 'react';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import Movie from '../Routes/Movie';
import TV from '../Routes/TV';
import Search from '../Routes/Search';
import Detail from '../Routes/Detail';

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
...
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

...
```

> `localhost:3000`: __Movies Area__
>
> `localhost:3000/tv`: __TV Shows Area__
>
> `localhost:3000/search`: __Search Input and Results Area__
>
> `localhost:3000/movie/272`: __Each Detail Area__
>
> `localhost:3000/show/272`: __Each Detail Area__

<br>

<br>

###### Redirect 설정

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
        <Redirect from="*" to="/" />
      </Switch>
    </React.Fragment>
  </Router>
);
```

> localhost:3000`/anything`과 같이, 설정하지 않은 경로를 입력하면 `/`로 Redirect 한다.

<br>

<br>

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

> 각 `<a> 태그`를 클릭해서 페이지 이동이 가능하다.
>
> 하지만 클릭할 때마다 `refresh` 된다.

<br>

<br>

###### 현재 디렉토리 구조

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

<br>