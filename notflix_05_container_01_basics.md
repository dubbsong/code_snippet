###### 서버 실행 종료

- `control` + `C`

<br>

###### 파일 제거

```bash
src
  └─ Routes
      ├─ Movie.js
      ├─ TV.js
      ├─ Search.js
      └─ Detail.js
```

> `Routes` 디렉토리는 남기고, 4개의 컴포넌트를 제거한다.

<br>

<br>

###### `Container / Presenter` Pattern

1. `Container`
   - Write Logic
   - state를 관리하고, API 호출 등의 로직을 처리한다.
2. `Presenter`
   - Only UI
   - 데이터를 props로 받아 화면에 표시한다.
   - Stateless, 그냥 함수형 컴포넌트이다.

<br>

###### 디렉토리 생성

```bash
$ cd src
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

###### 코드 작성: `Presenter`

- MoviePresenter.js

```react
export default () => 'Movies Area';
```

- TVPresenter.js

```react
export default () => 'TV Shows Area';
```

- SearchPresenter.js

```react
export default () => 'Search Input and Results Area';
```

- DetailPresenter.js

```react
export default () => 'Each Detail Area';
```

> `import` 없이 텍스트만 `export` 한다.

<br>

###### 코드 작성: `Container`

- MovieContainer.js

```react
import React from 'react';
import MoviePresenter from './MoviePresenter';

export default class extends React.Component {
  state = {
    nowPlaying: null,
    loading: true,
    error: null
  };

  // Logic

  render() {
    const { nowPlaying, loading, error } = this.state;

    return (
      <MoviePresenter
        nowPlaying={nowPlaying}
        loading={loading}
        error={error}
      />
    );
  }
}
```

- TVContainer.js

```react
import React from 'react';
import TVPresenter from './TVPresenter';

export default class extends React.Component {
  state = {
    topRated: null,
    loading: true,
    error: null
  };

  // Logic

  render() {
    const { topRated, loading, error } = this.state;

    return (
      <TVPresenter
        topRated={topRated}
        loading={loading}
        error={error}
      />
    );
  }
}
```

- SearchContainer.js

```react
import React from 'react';
import SearchPresenter from './SearchPresenter';

export default class extends React.Component {
  state = {
    movieResults: null,
    tvResults: null,
    searchTerm: '', // 사용자의 입력을 기다린다.
    loading: false, // 처음에 아무것도 로딩하지 않는다.
    error: null
  };

  // Logic

  render() {
    const { movieResults, tvResults, searchTerm, loading, error } = this.state;

    return (
      <SearchPresenter
        movieResults={movieResults}
        tvResults={tvResults}
        searchTerm={searchTerm}
        loading={loading}
        error={error}
      />
    );
  }
}
```

- DetailContainer.js

```react
import React from 'react';
import DetailPresenter from './DetailPresenter';

export default class extends React.Component {
  state = {
    result: null, // id를 사용해서 결과를 보여준다.
    loading: true,
    error: null
  };

  // Logic

  render() {
    const { result, loading, error } = this.state;

    return (
      <DetailPresenter
        result={result}
        loading={loading}
        error={error}
      />
    );
  }
}
```

<br>

###### 서버 실행

```bash
$ yarn start
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

###### 현재 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   └─ GlobalStyle.js
  ├─ Routes
  │   ├─ Movie
  │   │   ├─ index.js
  │   │   ├─ MovieContainer.js
  │   │   └─ MoviePresenter.js
  │   ├─ TV
  │   │   ├─ index.js
  │   │   ├─ TVContainer.js
  │   │   └─ TVPresenter.js
  │   ├─ Search
  │   │   ├─ index.js
  │   │   ├─ SearchContainer.js
  │   │   └─ SearchPresenter.js
  │   └─ Detail
  │       ├─ index.js
  │       ├─ DetailContainer.js
  │       └─ DetailPresenter.js
  ├─ assets
  │   └─ img
  │       └─ logo.png
  ├─ api.js
  └─ index.js
```

<br>

<br>