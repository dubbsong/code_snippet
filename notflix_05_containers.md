#### 폴더 생성

- src/Routes/Home
- src/Routes/TV
- src/Routes/Search
- src/Routes/Detail

<br>

#### 파일 생성

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
    searchTerm: '',
    loading: false,
    error: null
  };

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
    result: null,
    loading: true,
    error: null
  };

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
- 다시 `$ yarn start`

<br>

#### 코드 추가 (HomeContainer.js)

```react
...
import { movieApi } from 'api';

export default class extends React.Component {
  state = {...};

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

  render() {...}
}
```

> 콘솔에 데이터가 표시된다.

<br>

#### 코드 수정

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
        nowPlaying,
        popular,
        upcoming
      });
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const { nowPlaying, popular, upcoming, loading, error } = this.state;
    console.log(this.state);

    return (...);
  }
}
```

> 콘솔에서 state의 변화를 확인할 수 있다.

<br>

#### 에러 체크

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    try {
      ...

      const {
        data: { results: upcoming }
      } = await movieApi.upcoming();
      
      throw Error();	// 테스트 후 제거

      this.setState({
        nowPlaying,
        popular,
        upcoming
      });
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const { nowPlaying, popular, upcoming, loading, error } = this.state;
    console.log(this.state);	// 테스트 후 제거

    return (...);
  }
}
```

> 콘솔에서 `error: "Can't find movie information."`을 확인할 수 있다.
>
> 테스트 후, `throw Error();`와 `console.log(this.state)`를 제거한다.

<br>

#### 코드 추가 (TVContainer.js)

```react
...
import { tvApi } from 'api';

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
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

      this.setState({
        topRated,
        popular,
        airingToday
      });
    } catch {
      this.setState({
        error: "Can't find TV information."
      });
    } finally {
      this.setState({
        loading: false
      });
    }
  }

  render() {...}
}
```

<br>

#### 코드 추가 (SearchContainer.js)

```react
...
import { movieApi, tvApi } from 'api';

export default class extends React.Component {
  state = {
    ...
    searchTerm: 'code',	// 테스트 후 ''로 수정
    ...
  };

  // 테스트 후 제거
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

    this.setState({
      loading: true
    });

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
      this.setState({
        error: "Can't find results."
      });
    } finally {
      this.setState({
        loading: false
      });
    }
  };

  render() {
    const { movieResults, tvResults, searchTerm, loading, error } = this.state;
    console.log(this.state);	// 테스트 후 제거

    return (
      <SearchPresenter
        ...
        error={error}
        handleSubmit={this.handleSubmit}
      />
    );
  }
}
```

> 콘솔에서 `code`가 포함되어 있는 결과를 확인할 수 있다.
>
> 탭 이동 시 에러가 발생하지만, 후에 수정한다.
>
> 테스트 코드를 제거한다.

<br>

#### Route 추가 (for Detail)

- Router.js

```react
...
import Detail from 'Routes/Detail';

export default () => (
  <Router>
    <React.Fragment>
      <Nav />
      <Switch>
        ...
        <Route path="/movie/:id" component={Detail} />
        <Route path="/show/:id" component={Detail} />
        <Redirect from="*" to="/" />
      </Switch>
    </React.Fragment>
  </Router>
);
```

<br>

#### 코드 추가 (DetailContainer.js) (for Detail url)

- 콘솔 데이터를 참조한다.

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

    // url 뒤에 작성한 숫자가 콘솔에 표시된다.
    console.log(id);	// 2. 테스트 후 제거
    console.log(typeof id);	// string 3. 테스트 후 제거
    console.log(typeof parseInt(id));	// number 4. 테스트 후 제거
    // url 뒤에 /movie/test와 같이 문자열을 입력하면, Home으로 Redirect 한다.
    // url 뒤에 /movie/121과 같이 숫자를 입력하면, 해당 Detail 페이지로 이동한다.

    const parsedId = parseInt(id);

    if (isNaN(parsedId)) {
      return push('/');
    }
  }

  render() {
    console.log(this.props);	// 1. 테스트 후 제거
    const { result, loading, error } = this.state;

    return (...);
  }
}
```

> 테스트 코드를 제거한다.

<br>

#### 코드 추가 (DetailContainer.js) (Detail for path)

```react
...
import { movieApi, tvApi } from 'api';

export default class extends React.Component {
  constructor(props) {
    super(props);

    const {
      location: { pathname }
    } = props;

    this.state = {
      result: null,
      loading: true,
      error: null,
      isMovie: pathname.includes('/movie/')
    };
  }

  async componentDidMount() {
    const {...} = this.props;
    console.log(this.props);	// 1. 테스트 후 제거

    const { isMovie } = this.state;

    const parsedId = parseInt(id);

    if (isNaN(parsedId)) {...}

    let result = null;

    try {
      if (isMovie) {
        const request = await movieApi.movieDetail(parsedId);
        result = request.data;
      } else {
        const request = await tvApi.tvDetail(parsedId);
        result = request.data;
      }
    } catch {
      this.setState({
        error: "Can't find anything."
      });
    } finally {
      this.setState({
        loading: false,
        result
      });
    }
  }

  render() {
    const { result, loading, error } = this.state;
    console.log(this.state);	// 2. 테스트 후 제거

    return (...);
  }
}
```

> `localhost:3000/movie/121`을 입력해서 확인할 수 있다.
>
> 테스트 코드를 제거한다.

<br>

- Test in Chrome console

```js
const path = "/movie/8688";
path.includes("/movie/");	// true
path.includes("/show/");	// false
```

<br>

#### 코드 수정 (DetailContainer.js) (Better than before)

```react
...

export default class extends React.Component {
  constructor(props) {...}

  async componentDidMount() {
    const {...} = this.props;
    console.log(this.props);	// 1. 테스트 후 제거

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
    const { result, loading, error } = this.state;
    console.log(result);	// 2. 테스트 후 제거

    return (...);
  }
}
```

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