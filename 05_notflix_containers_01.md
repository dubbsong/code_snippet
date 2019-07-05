#### Container & Presenter Components Pattern 사용

1. `Container`
   - Logic
   - 주로 데이터를 가져오고, state를 관리하고, API 호출 등의 로직을 처리한다.
2. `Presenter`
   - Only UI
   - 데이터를 props로 받아 화면에 표시한다.
   - no state, 그냥 함수형 컴포넌트이다.

<br>

#### 폴더 생성

- src/Routes/Home
- src/Routes/TV
- src/Routes/Search
- src/Routes/Detail

<br>

#### 파일 생성 (index.js)

- src/Routes/Home/index.js
- src/Routes/TV/index.js
- src/Routes/Search/index.js
- src/Routes/Detail/index.js

<br>

#### Container 생성

- src/Routes/Home/HomeContainer.js
- src/Routes/TV/TVContainer.js
- src/Routes/Search/SearchContainer.js
- src/Routes/Detail/DetailContainer.js

<br>

#### Presenter 생성

- src/Routes/Home/HomePresenter.js
- src/Routes/TV/TVPresenter.js
- src/Routes/Search/SearchPresenter.js
- src/Routes/Detail/DetailPresenter.js

<br>

#### 코드 작성 (각 index.js)

- src/Routes/Home/index.js

```react
import HomeContainer from './HomeContainer';

export default HomeContainer;
```

<br>

- src/Routes/TV/index.js

```react
import TVContainer from './TVContainer';

export default TVContainer;
```

<br>

- src/Routes/Search/index.js

```react
import SearchContainer from './SearchContainer';

export default SearchContainer;
```

<br>

- src/Routes/Detail/index.js

```react
import DetailContainer from './DetailContainer';

export default DetailContainer;
```

<br>

#### 코드 작성 (각 Presenter.js)

- HomePresenter.js

```react
export default () => 'Home';
```

<br>

- TVPresenter.js

```react
export default () => 'TV';
```

<br>

- SearchPresenter.js

```react
export default () => 'Search';
```

<br>

- DetailPresenter.js

```react
export default () => 'Detail';
```

<br>

#### 코드 작성 (각 Container.js) (for state)

- HomeContainer.js

```react
import React from 'react';
import HomePresenter from './HomePresenter';

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
      <HomePresenter
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

<br>

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

<br>

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

<br>

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

#### 파일 제거

- src/Routes/Home.js
- src/Routes/TV.js
- src/Routes/Detail.js
- src/Routes/Search.js
- 다시 `$ yarn start` (정상 작동)

<br>

<br>