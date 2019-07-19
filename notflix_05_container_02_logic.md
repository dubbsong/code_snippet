#### try/catch/finally 문

###### [w3schools](https://www.w3schools.com/jsref/jsref_try_catch.asp) 참조

- try/catch/finally 문은, 코드를 실행하는 동안 코드 블록에서 발생할 수 있는 일부 또는 모든 에러를 처리한다.

```js
try {
  // 시도할 코드 블록
} catch {
  // 에러 처리를 위한 코드 블록
} finally {
  // try/catch 결과에 상관없이 실행될 코드 블록
}
```

<br>

<br>

#### 로직 작성: `MovieContainer`

- 데이터 확인

```react
...
import { movieApi } from 'api';

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    try {
      const nowPlaying = await movieApi.nowPlaying();
      const popular = await movieApi.popular();
      const upcoming = await movieApi.upcoming();

      console.log(nowPlaying, popular, upcoming);
    } catch {
      this.setState({ error: "Can't find movie information." });
    } finally {
      this.setState({ loading: false });
    }
  };

  render() {
    ...
  }
}
```

> `Movies`를 클릭하면, Console 탭에서 `nowPlaying`, `popular`, `upcoming`의 데이터를 확인할 수 있다.
>
> `data`의 `results`에서 필요한 데이터를 확인할 수 있다.

<br>

- 구조 분해 할당 (Destructuring Assignment)

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
        nowPlaying: nowPlaying, // 단축 가능 (TVContainer에서 확인)
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

> Console 탭에서 state의 3가지 변화를 확인할 수 있다.
>

<br>

- Error test

```react
...

export default class extends React.Component {
  state = {...};

  async componentDidMount() {
    try {
      ...

      throw Error();	// 테스트 후 제거

      this.setState({...});
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const {...} = this.state;
    console.log(this.state);	// 테스트 후 제거

    return (...);
  }
}
```

> Console 탭에서 state의 3가지 변화를 확인할 수 있다.
>
> `throw Error();`와 `console.log(this.state);`를 제거한다.

<br>

#### 로직 작성: `TVContainer`

- 데이터 확인

```react
...
import { tvApi } from 'api';

export default class extends React.Component {
  state = {...};

  // MovieContainer의 async cdm와 동일한 문법
  componentDidMount = async () => {
    try {
      const topRated = await tvApi.topRated();
      const popular = await tvApi.popular();
      const airingToday = await tvApi.airingToday();

      console.log(topRated, popular, airingToday);
    } catch {
      this.setState({ error: "Can't find tv information." });
    } finally {
      this.setState({ loading: false });
    }
  };

  render() {
    ...
  }
}
```

> `TV Shows`를 클릭하면, Console 탭에서 `topRated`, `popular`, `airingToday`의 데이터를 확인할 수 있다.

<br>

- 구조 분해 할당 (Destructuring Assignment)

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

      // MovieContainer와 동일한 문법
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
    console.log(this.state); // 테스트 후 제거

    return (
      ...
    );
  }
}
```

> Console 탭에서 state의 3가지 변화를 확인할 수 있다.
>
> `console.log(this.state);`를 제거한다.

<br>

#### 로직 작성: `SearchContainer`

- 데이터 확인

```react
...
import { movieApi, tvApi } from 'api';

export default class extends React.Component {
  state = {
    movieResults: null,
    tvResults: null,
    searchTerm: 'code', // 테스트를 위해 'code'를 입력
    loading: false,
    error: null
  };

  // 테스트를 위해 cdm 작성
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
    } catch {
      this.setState({ error: "Can't find results." });
    } finally {
      this.setState({ loading: false });
    }
  };

  render() {
    ...
  }
}
```

> `🔍`를 클릭하면, Console 탭에서 `"code"`가 포함된 `movieResults`, `tvResults`의 데이터를 확인할 수 있다.

<br>

- 구조 분해 할당 (Destructuring Assignment)

```react
...

export default class extends React.Component {
  state = {
    ...
    searchTerm: 'code', // 테스트 후 ''로 변경
    ...
  };

  // 테스트 후 cdm 제거
  componentDidMount() {
    ...
  }

  handleSubmit = () => {
    ...
  };

  searchByTerm = async () => {
    const { searchTerm } = this.state;

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
    const {...} = this.state;
    console.log(this.state); // 확인 후 제거

    return (
      ...
    );
  }
}
```

> Console 탭에서 state의 3가지 변화를 확인할 수 있다.

> `'code'`를 `''`로 변경한다.
>
> `cdm`를 제거한다.
>
> `console.log(this.state);`를 제거한다.

<br>

- `handleSubmit`을 `SearchPresenter`에 전달

```react
...

export default class extends React.Component {
  ...

  render() {
    ...

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

> `searchTerm`을 업데이트하는 함수는 나중에 작성한다.
>
> 탭 이동 시 에러가 발생하지만, 나중에 수정한다.

<br>

<br>

#### 로직 작성: `DetailContainer`

- 데이터 확인

```react
...

export default class extends React.Component {
  state = {...};

  // Logic

  render() {
    console.log(this.props);	// for checking id
    ...
  }
}
```

> `localhost:3000/movie/121`로 이동하면, `match`의 `params`에서 `id`를 확인할 수 있다.

<br>

- 데이터 타입 확인

```react
...

export default class extends React.Component {
  state = {...};

  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      }
    } = this.props;

    // localhost:3000/movie/121 입력
    console.log(id); // 121
    console.log(typeof id); // string
    console.log(typeof parseInt(id)); // number
    console.log(parseInt(id)); // 121

    // localhost:3000/movie/abc 입력
    console.log(parseInt(id)); // NaN
  };

  render() {
    console.log(this.props);
    ...
  }
}
```

> cdm의 `console.log(…);`들을 제거한다.
>
> render()의 `console.log(this.props);`는 아직 제거하지 않는다.

<br>

- Redirect 설정

```react
...

export default class extends React.Component {
  state = {...};

  componentDidMount = async () => {
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
  };

  render() {
    ...
  }
}
```

> `/movie/abc` 또는 `/show/abc`의 경우, `/`를 push해서 Home으로 Redirect 한다.

<br>

- pathname 확인

```react
...

export default class extends React.Component {
  state = {...};

  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      },
      history: { push },
      location: { pathname }
    } = this.props;

    // pathname 확인
    this.isMovie = pathname.includes('/movie/');
    console.log(this.isMovie); // true

    ...
  };

  render() {
    console.log(this.props); // 확인 후 제거
    ...
  }
}
```

> `localhost:3000/movie/121`을 입력하면, `location`에서 `pathname`을 확인할 수 있다.
>
> `localhost:3000/movie/121`의 경우, true를 반환한다.
>
> `localhost:3000/show/121`의 경우, false를 반환한다.

> `console.log(this.isMovie);`를 제거한다.
>
> `console.log(this.props);`를 제거한다.

<br>

- For example:

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

  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      },
      history: { push }
    } = this.props;

    const parsedId = parseInt(id);

    if (isNaN(parsedId)) {
      return push('/');
    }

    const { isMovie } = this.state;
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
  };

  render() {
    const {...} = this.state;
    console.log(this.state);

    ...
  }
}
```

> `localhost:3000/movie/121`을 입력하면, `result`에서 `data`를 확인할 수 있다.

<br>

- `/movie/`인지 아닌지 확인한 후, result 덮어쓰기

```react
...

export default class extends React.Component {
  constructor(props) {
    ...
  }

  componentDidMount = async () => {
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
  };

  render() {
    const {...} = this.state;
    console.log(this.state); // 확인 후 제거

    ...
  }
}
```

> 해당 id의 정보를 확인할 수 있다.
>
> `console.log(this.state);`를 제거한다.

<br>

- better than before

```react
...

export default class extends React.Component {
  constructor(props) {
    ...
  }

  componentDidMount = async () => {
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
  };

  render() {
    const {...} = this.state;
    console.log(result); // 확인 후 제거

    ...
  }
}
```

> 해당 데이터를 확인할 수 있다.
>
> `console.log(result);`를 제거한다.

<br>

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

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set Containers'
$ git push origin master
```

<br>

<br>