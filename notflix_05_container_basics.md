#### Container & Presenter Pattern

1. `Container`
   - Logic
   - 주로 데이터를 가져오고, state를 관리하고, API 호출 등의 로직을 처리한다.
2. `Presenter`
   - Only UI
   - 데이터를 props로 받아 화면에 표시한다.
   - no state, 그냥 함수형 컴포넌트이다.

<br>

<br>

#### React 실행 종료

- `control` \+ `C`

<br>

#### 파일 제거

- src/Routes/Movie.js
- src/Routes/TV.js
- src/Routes/Detail.js
- src/Routes/Search.js

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

#### 디렉토리 생성

- src/Routes/Movie
- src/Routes/TV
- src/Routes/Search
- src/Routes/Detail

<br>

#### index.js 생성

- src/Routes/Movie/index.js
- src/Routes/TV/index.js
- src/Routes/Search/index.js
- src/Routes/Detail/index.js

<br>

#### Container 생성

- src/Routes/Movie/MovieContainer.js
- src/Routes/TV/TVContainer.js
- src/Routes/Search/SearchContainer.js
- src/Routes/Detail/DetailContainer.js

<br>

#### Presenter 생성

- src/Routes/Movie/MoviePresenter.js
- src/Routes/TV/TVPresenter.js
- src/Routes/Search/SearchPresenter.js
- src/Routes/Detail/DetailPresenter.js

<br>

#### 코드 작성: 각 `index.js`

- src/Routes/Movie/index.js

```react
import MovieContainer from './MovieContainer';

export default MovieContainer;
```

- src/Routes/TV/index.js

```react
import TVContainer from './TVContainer';

export default TVContainer;
```

- src/Routes/Search/index.js

```react
import SearchContainer from './SearchContainer';

export default SearchContainer;
```

- src/Routes/Detail/index.js

```react
import DetailContainer from './DetailContainer';

export default DetailContainer;
```

<br>

#### 코드 작성: 각 `Presenter`

- MoviePresenter.js

```react
export default () => 'Movie Presenter';
```

- TVPresenter.js

```react
export default () => 'TV Presenter';
```

- SearchPresenter.js

```react
export default () => 'Search Presenter';
```

- DetailPresenter.js

```react
export default () => 'Detail Presenter';
```

<br>

#### 코드 작성: 각 `Container`

- MovieContainer.js

```react
import React from 'react';
import MoviePresenter from './MoviePresenter';

export default class extends React.Component {
  state = {
    nowPlaying: null,
    popular: null,
    upcoming: null,
    loading: true,
    error: null
  };

  // 여기에 로직을 작성한다.

  render() {
    const { nowPlaying, popular, upcoming, loading, error } = this.state;

    return (
      <MoviePresenter
        nowPlaying={nowPlaying}
        popular={popular}
        upcoming={upcoming}
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
    popular: null,
    airingToday: null,
    loading: true,
    error: null
  };

  // 여기에 로직을 작성한다.

  render() {
    const { topRated, popular, airingToday, loading, error } = this.state;

    return (
      <TVPresenter
        topRated={topRated}
        popular={popular}
        airingToday={airingToday}
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

  // 여기에 로직을 작성한다.

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
    result: null,	// id를 가져와서 결과를 보여준다.
    loading: true,
    error: null
  };

  // 여기에 로직을 작성한다.

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

#### 다시 실행

```bash
$ yarn start
```

> `localhost:3000`: Movie Presenter
>
> `localhost:3000/tv`: TV Presenter
>
> `localhost:3000/search`: Search Presenter

<br>

<br>