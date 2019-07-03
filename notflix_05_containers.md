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

#### 로직 작성 (HomeContainer.js)

- 콘솔에서 데이터 확인 (for setting state value)

```react
...
import { movieApi } from 'api';

export default class extends React.Component {
  state = {...};

  // 로직
  async componentDidMount() {
    try {
      const nowPlaying = await movieApi.nowPlaying();
      console.log(nowPlaying);
    } catch {
      this.setState({
        error: "Can't find movie information."
      });
    } finally {
      this.setState({
        loading: false
      });
    }
  }
  // try: 실행한다.
  // catch: 주로 error를 처리한다.
  // finally: 어떤 결과라도 보여준다. (movie or error)
  // async & await: cdm를 실행한 후, JS는 API response를 기다리지 않는다. 그래서 작업을 끝낼 때까지 '나 좀 기다려줘'라고 JS에게 말하는 것과 같다.

  render() {...}
}
```

> 콘솔에서 `nowPlaying` 데이터를 확인할 수 있다.
>
> 우리에게 필요한 것은 `data`의 `results`이다.

<br>

- Object Destructuring Assignment (변수 이름 변경)

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    try {
      const {
        data: { results: nowPlaying }
      } = await movieApi.nowPlaying();

      const {
        data: { results: popular }
      } = await movieApi.popular();

      const {
        data: { results: upcoming }
      } = await movieApi.upcoming();

      this.setState({
        nowPlaying: nowPlaying, // 단축이 가능하다.
        popular: popular,
        upcoming: upcoming
      });
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const {...} = this.state;
    console.log(this.state);

    return (...);
  }
}
```

> 콘솔에서 state의 3가지 변화를 확인할 수 있다.

<br>

- Error test

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    try {
      ...

      throw Error();	// 테스트 후 제거한다.

      this.setState({...});
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const {...} = this.state;
    console.log(this.state);	// 테스트 후 제거한다.

    return (...);
  }
}
```

> 콘솔에서 state의 3가지 변화를 확인할 수 있다.
>
> 테스트 후, `throw Error();`와 `console.log(this.state);`를 제거한다.

<br>



#### 로직 작성 (TVContainer.js)

- 콘솔에서 데이터 확인 (for setting state value)

```react
...
import { tvApi } from 'api';

export default class extends React.Component {
  state = {...};

  // HomeContainer 부분과 동일한 문법이다.
  componentDidMount = async () => {
    try {
      const topRated = await tvApi.topRated();
      const popular = await tvApi.popular();
      const airingToday = await tvApi.airingToday();
      console.log(topRated, popular, airingToday);
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {...}
}
```

> 콘솔에서 `topRated, popular, airingToday` 데이터를 확인할 수 있다.
>
> 우리에게 필요한 것은 `data`의 `results`이다.

<br>

- Object Destructuring Assignment (변수 이름 변경)

```react
...

export default class extends React.Component {
  state = {...};

  componentDidMount = async () => {
    try {
      const {
        data: { results: topRated }
      } = await tvApi.topRated();

      const {
        data: { results: popular }
      } = await tvApi.popular();

      const {
        data: { results: airingToday }
      } = await tvApi.airingToday();

      // HomeContainer 부분과 동일한 문법이다. (단축형)
      this.setState({
        topRated,
        popular,
        airingToday
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {
    const {...} = this.state;
    console.log(this.state);	// 테스트 후 제거한다.

    return (...);
  }
}
```

> 콘솔에서 state의 3가지 변화를 확인할 수 있다.
>
> 테스트 후, `console.log(this.state);`를 제거한다.

<br>

#### 로직 작성 (SearchContainer.js)

- 콘솔에서 데이터 확인 (for setting state value)

```react
...
import { movieApi, tvApi } from 'api';

export default class extends React.Component {
  state = {
    movieResults: null,
    tvResults: null,
    searchTerm: 'code', // Type 'code' for test
    loading: false,
    error: null
  };

  // for test
  componentDidMount() {
    this.handleSubmit();
  }

  handleSubmit = () => {
    const { searchTerm } = this.state;

    if (searchTerm !== '') {
      this.searchByTerm();
    }
  };

  searchByTerm = async () => {
    const { searchTerm } = this.state;

    try {
      const movieResults = await movieApi.search(searchTerm);
      const tvResults = await tvApi.search(searchTerm);
      console.log(movieResults, tvResults);

      // 검색을 했을 때, loading을 true로 변경한다.
      this.setState({ loading: true });
    } catch {
      this.setState({ error: "Can't find results." });
    } finally {
      this.setState({ loading: false });
    }
  };

  render() {...}
}
```

> `data`의 `results`에서 `code`가 포함된 데이터를 확인할 수 있다.
>
> 테스트 후, `this.setState({ loading: true });`의 위치를 `const { searchTerm } = this.state;` 아래로 이동시킨다.

<br>

- Object Destructuring Assignment (변수 이름 변경) & 데이터 확인

```react
...

export default class extends React.Component {
  state = {
    movieResults: null,
    tvResults: null,
    searchTerm: 'code', // Type 'code' for test
    loading: false,
    error: null
  };

  // for test
  componentDidMount() {
    this.handleSubmit();
  }

  handleSubmit = () => {
    const { searchTerm } = this.state;

    if (searchTerm !== '') {
      this.searchByTerm();
    }
  };

  searchByTerm = async () => {
    const { searchTerm } = this.state;
    this.setState({ loading: true });

    try {
      const {
        data: { results: movieResults }
      } = await movieApi.search(searchTerm);

      const {
        data: { results: tvResults }
      } = await tvApi.search(searchTerm);

      this.setState({
        movieResults,
        tvResults
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {
    const { movieResults, tvResults, searchTerm, loading, error } = this.state;
    console.log(this.state);	// 테스트 후 제거한다.

    return (...);
  }
}
```

> 테스트 후, `'code'`를 `''`로 변경한다.
>
> 테스트 후, `cdm`를 제거한다.
>
> 테스트 후, `console.log(this.state);`를 제거한다.

<br>

- `handleSubmit`을 `SearchPresenter`에 보낸다.

```react
...

export default class extends React.Component {
  ...

  render() {
    ...

    return (
      <SearchPresenter
        ...
        handleSubmit={this.handleSubmit}
      />
    );
  }
}
```

> `searchTerm`을 업데이트하는 함수는 나중에 작성할 것이다.
>
> 탭 이동 시 에러가 발생하지만, 나중에 수정할 것이다.

<br>

#### Detail Route 추가

- Router.js
  - `/movie/121`로 이동
  - `/show/121`로 이동

```react
...
import Detail from 'Routes/Detail';

export default () => (
  <Router>
    <React.Fragment>
      <Nav />
      <Switch>
        ...
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

#### 로직 작성 (DetailContainer.js)

- 콘솔에서 데이터 확인 (for props)

```react
...

export default class extends React.Component {
  state = {...};

  render() {
    console.log(this.props);
    ...
  }
}
```

> `localhost:3000/movie/121`을 입력하면, `match`의 `params`에서 `id`가 포함된 데이터를 확인할 수 있다.

<br>

- 데이터 타입 확인 (for getting `id`)

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    const {
      match: {
        params: { id }
      }
    } = this.props;

    // localhost:3000/movie/121 입력
    console.log(id); // 121
    console.log(typeof id); // string
    console.log(typeof parseInt(id)); // number

    // localhost:3000/movie/abc 입력
    console.log(parseInt(id)); // NaN
  }

  render() {...}
}
```

> 테스트 후, 모든 `console.log(…);`를 제거한다.

<br>

- Redirect 설정

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    const {
      match: {
        params: { id }
      },
      history: { push }
    } = this.props;

    const parsedId = parseInt(id);

    if (isNaN(parsedId)) {
      return push('/'); // return을 추가해서 함수를 종료시킨다.
    }
  }

  ...
}
```

> `/movie/abc` 또는 `/show/abc`의 경우, `/`를 push해서 Home으로 Redirect 한다.

<br>

- pathname 확인

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    const {
      ...,
      history: { push },
      location: { pathname }
    } = this.props;

    ...

    if (isNaN(parsedId)) {
      return push('/');
    }

    // pathname 확인
    this.isMovie = pathname.includes('/movie/');
    console.log(this.isMovie);	// 테스트 후 제거한다.
  }

  render() {...}
}
```

> `localhost:3000/movie/121`을 입력하면, `location`에서 `pathname`을 확인할 수 있다.
>
> `localhost:3000/movie/121`의 경우, true를 반환한다.
>
> `localhost:3000/show/121`의 경우, false를 반환한다.
>
> `console.log(this.isMovie);`를 제거한다.
>
> `console.log(this.props);`를 제거한다.

<br>

- 참조

```js
const path = "/movie/8688";
path.includes("/movie/");	// true
path.includes("/show/");	// false
```

<br>

- constructor 사용

```react
...
import { movieApi, tvApi } from 'api';

export default class extends React.Component {
  constructor(props) {
    const {
      location: { pathname }
    } = props;

    super(props);
    this.state = {
      result: null,
      loading: true,
      error: null,
      isMovie: pathname.includes('/movie/')
    };
  }

  async componentDidMount() {
    const {
      match: {
        params: { id }
      },
      history: { push }
    } = this.props;

    const { isMovie } = this.state;

    const parsedId = parseInt(id);

    if (isNaN(parsedId)) {
      return push('/');
    }

    let result = null;

    try {
      if (isMovie) {
        result = await movieApi.movieDetail(parsedId);
      } else {
        result = await tvApi.tvDetail(parsedId);
      }
    } catch {
      this.setState({ error: "Can't find anything." });
    } finally {
      this.setState({ loading: false, result });
    }
  }

  render() {
    const { result, loading, error } = this.state;
    console.log(this.state);

    return (...);
  }
}
```

> `localhost:3000/movie/121`을 입력하면, `result`에서 `data`를 확인할 수 있다.

<br>

- `/movie/`인지 아닌지 확인한 후, result 덮어쓰기

```react
...

export default class extends React.Component {
  ...

    try {
      if (isMovie) {
        const request = await movieApi.movieDetail(parsedId);
        result = request.data;
      } else {
        const request = await tvApi.tvDetail(parsedId);
        result = request.data;
      }
    } catch {
      ...
    } finally {
      ...
    }
  }

  ...
}
```

> 해당 id의 정보를 확인할 수 있다.

<br>

- better than before

```react
...

export default class extends React.Component {
  ...

    try {
      if (isMovie) {
        ({ data: result } = await movieApi.movieDetail(parsedId));
      } else {
        ({ data: result } = await tvApi.tvDetail(parsedId));
      }
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const {...} = this.state;
    console.log(result); // 테스트 후 제거한다.

    ...
  }
}
```

> 해당 데이터를 확인할 수 있다.
>
> `console.log(result);`를 제거한다.

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set Containers'
$ git push origin master
```

------

<br>

<br>