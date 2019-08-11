###### `Container / Presenter` 패턴 사용

> 1. `Container`
>    - Write Logic
>    - state 관리, API 호출 등의 로직 처리
> 2. `Presenter`
>    - Only UI
>    - stateless, prop-types 설정

<br>

<br>

###### 디렉토리 생성: `Routes`

```bash
$ cd src
$ mkdir Routes
```

<br>

###### 디렉토리 생성: `Movie` / `TV` / `Search` / `Detail`

```bash
$ cd Routes
$ mkdir Movie
$ mkdir TV
$ mkdir Search
$ mkdir Detail
```

<br>

###### 컴포넌트 생성: `index` / `Container` / `Presenter`

- Movie

```bash
$ cd Movie
$ touch index.js
$ touch MovieContainer.js
$ touch MoviePresenter.js
```

- TV

```bash
$ cd ..
$ cd TV
$ touch index.js
$ touch TVContainer.js
$ touch TVPresenter.js
```

- Search

```bash
$ cd ..
$ cd Search
$ touch index.js
$ touch SearchContainer.js
$ touch SearchPresenter.js
```

- Detail

```bash
$ cd ..
$ cd Detail
$ touch index.js
$ touch DetailContainer.js
$ touch DetailPresenter.js
```

<br>

###### 코드 작성: `Presenter`

- MoviePresenter.js

```react
import React from 'react';

const MoviePresenter = () => 'Movies Area';

export default MoviePresenter;
```

- TVPresenter.js

```react
import React from 'react';

const TVPresenter = () => 'TV Shows Area';

export default TVPresenter;
```

- SearchPresenter.js

```react
import React from 'react';

const SearchPresenter = () => 'Search Input & Results Area';

export default SearchPresenter;
```

- DetailPresenter.js

```react
import React from 'react';

const DetailPresenter = () => 'Each Detail Area';

export default DetailPresenter;
```

<br>

###### 코드 작성: `Container`

- MovieContainer.js

```react
import React from 'react';
import MoviePresenter from './MoviePresenter';

export default class extends React.Component {
  render() {
    return <MoviePresenter />;
  }
}
```

- TVContainer.js

```react
import React from 'react';
import TVPresenter from './TVPresenter';

export default class extends React.Component {
  render() {
    return <TVPresenter />;
  }
}
```

- SearchContainer.js

```react
import React from 'react';
import SearchPresenter from './SearchPresenter';

export default class extends React.Component {
  render() {
    return <SearchPresenter />;
  }
}
```

<br>

- DetailContainer.js

```react
import React from 'react';
import DetailPresenter from './DetailPresenter';

export default class extends React.Component {
  render() {
    return <DetailPresenter />;
  }
}
```

<br>

###### 코드 작성: `index`

- Movie/index.js

```react
import MovieContainer from './MovieContainer';

export default MovieContainer;
```

- TV/index.js

```react
import TVContainer from './TVContainer';

export default TVContainer;
```

- Search/index.js

```react
import SearchContainer from './SearchContainer';

export default SearchContainer;
```

- Detail/index.js

```react
import DetailContainer from './DetailContainer';

export default DetailContainer;
```

<br>

###### react-router-dom 설치

```bash
$ yarn add react-router-dom
```

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
import {
  BrowserRouter as Router,
  Route,
  Switch,
  Redirect
} from 'react-router-dom';
import Movie from 'Routes/Movie';
import TV from 'Routes/TV';
import Search from 'Routes/Search';
import Detail from 'Routes/Detail';

export default () => (
  <Router>
    <React.Fragment>
      <Switch>
        <Route path="/" exact component={Movie} />
        <Route path="/tv" component={TV} />
        <Route path="/search" component={Search} />
        <Route path="/movie/:id" component={Detail} />
        <Route path="/show/:id" component={Detail} />
        <Redirect from="*" to="/" />
      </Switch>
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
        <GlobalStyle />
      </React.Fragment>
    );
  }
}

...
```

> `localhost:3000`: Movies Area
>
> `localhost:3000/tv`: TV Shows Area
>
> `localhost:3000/search`: Search Input & Results Area
>
> `localhost:3000/movie/272`: Each Detail Area
>
> `localhost:3000/show272`: Each Detail Area
>
> `localhost:3000/abc`: `/`로 Redirect

<br>

<br>
