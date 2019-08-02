###### `try / catch / finally` Statement

###### [w3schools](https://www.w3schools.com/jsref/jsref_try_catch.asp) 참조

- 코드를 실행하는 동안, 코드 블록에서 발생할 수 있는 일부 또는 모든 에러를 처리한다.

```js
try {
  // 시도할 코드 블록
} catch {
  // 에러 처리를 위한 코드 블록
} finally {
  // try / catch 결과에 상관없이 실행될 코드 블록
}
```

<br>

<br>

###### 로직 작성: `MovieContainer`

- 데이터 확인

```react
...
import { movieApi } from '../../api';

export default class extends React.Component {
  ...

  // Logic
  async componentDidMount() {
    try {
      const nowPlaying = await movieApi.nowPlaying();
      console.log(nowPlaying);
    } catch {
      this.setState({ error: "Can't find movie information." });
    } finally {
      this.setState({ loading: false });
    }
  }

  ...
}
```

> 1. Nav `Movies` 클릭
> 2. 개발자 도구 `Console` 탭 클릭
> 3. `data`의 `results` 확인 (20개)

> `id`, `poster_path`, `vote_average`, `original_title`, `release_date`, `backdrop_path`, `genre_ids`, `overview`가 필요하다.

<br>

- 구조 분해 할당 (Destructuring Assignment)

```react
...

export default class extends React.Component {
  ...

  // Logic
  async componentDidMount() {
    try {
      const {
        data: { results: nowPlaying }
      } = await movieApi.nowPlaying();

      this.setState({
        nowPlaying: nowPlaying // ES6 구문으로 단축 가능
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

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화를 확인할 수 있다.

<br>

- Error 확인

```react
...

export default class extends React.Component {
  ...

  // Logic
  async componentDidMount() {
    try {
      const {
        data: { results: nowPlaying }
      } = await movieApi.nowPlaying();

      throw Error(); // 테스트 후 제거

      this.setState({
        ...
      });
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    const {...} = this.state;
    console.log(this.state); // 테스트 후 제거

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화를 확인할 수 있다.
>
> `throw Error();`를 제거한다.
>
> `console.log(this.state);`를 제거한다.

<br>

###### 로직 작성: `TVContainer`

- 데이터 확인

```react
...
import { tvApi } from '../../api';

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    try {
      const topRated = await tvApi.topRated();
      console.log(topRated);
    } catch {
      this.setState({ error: "Can't find tv information." });
    } finally {
      this.setState({ loading: false });
    }
  };

  ...
}
```

> 1. Nav `TV Shows` 클릭
> 2. 개발자 도구 `Console` 탭 클릭
> 3. `data`의 `results` 확인 (20개)

> `id`, `poster_path`, `vote_average`, `original_name`, `first_air_date`, `backdrop_path`, `genre_ids`, `overview`가 필요하다.

<br>

- 구조 분해 할당 (Destructuring Assignment)

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    try {
      const {
        data: { results: topRated }
      } = await tvApi.topRated();

      this.setState({
        topRated // ES6 구문으로 단축
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {
    const {...} = this.state;
    console.log(this.state);

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화를 확인할 수 있다.

<br>

- Error 확인

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    try {
      const {
        data: { results: topRated }
      } = await tvApi.topRated();

      throw Error(); // 테스트 후 제거

      this.setState({
        ...
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

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화를 확인할 수 있다.
>
> `throw Error();`, `console.log(this.state);`를 제거한다.

<br>

###### 로직 작성: `SearchContainer`

- 데이터 확인

```react
...
import { movieApi, tvApi } from '../../api';

export default class extends React.Component {
  state = {
    ...
    searchWord: 'batman', // For test
    ...
  };

  // Logic
  handleSubmit = () => {
    const { searchWord } = this.state;

    if (searchWord !== '') {
      this.searchByWord();
    }
  };

  searchByWord = async () => {
    const { searchWord } = this.state;

    try {
      const movieResults = await movieApi.search(searchWord);
      const tvResults = await tvApi.search(searchWord);
      console.log(movieResults, tvResults);
    } catch {
      this.setState({ error: "Can't find results." });
    } finally {
      this.setState({ loading: false });
    }
  };

  // For test
  componentDidMount() {
    this.handleSubmit();
  }

  ...
}
```

> 1. Nav `🔍` 클릭
> 2. 개발자 도구 `Console` 탭 클릭
> 3. `movieResults`, `tvResults` 데이터 확인

<br>

- 구조 분해 할당 (Destructuring Assignment)

```react
...

export default class extends React.Component {
  state = {
    ...
    searchWord: 'batman', // 테스트 후 ''로 변경
    ...
  };

  // Logic
  ...

  searchByWord = async () => {
    ...

    try {
      const {
        data: { results: movieResults }
      } = await movieApi.search(searchWord);

      const {
        data: { results: tvResults }
      } = await tvApi.search(searchWord);

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

  // 테스트 후 제거
  componentDidMount() {
    this.handleSubmit();
  }

  render() {
    const {...} = this.state;
    console.log(this.state); // 테스트 후 제거

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화를 확인할 수 있다.
>
> `'batman'`을 `''`로 변경한다.
>
> `cdm`를 제거한다.
>
> `console.log(this.state);`를 제거한다.

<br>

- `handleSubmit` props 전달

```react
...

export default class extends React.Component {
  ...

  render() {
    const {...} = this.state;

    return (
      <SearchPresenter
        ...
        handleSubmit={this.handleSubmit}
      />
    );
  }
}
```

> `searchWord`를 업데이트하는 함수는 나중에 작성한다.
>
> 탭 이동 시 에러가 발생하지만, 나중에 수정한다.

<br>

###### 로직 작성: `DetailContainer`

- 데이터 확인

```react
...

export default class extends React.Component {
  ...

  render() {
    console.log(this.props);
    ...
  }
}
```

> 1. `localhost:3000/movie/272`로 이동
> 2. `match`의 `params`에서 `id` 확인

<br>

- 데이터 타입 확인

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      }
    } = this.props;

    // localhost:3000/movie/272 입력
    console.log(id); // 272
    console.log(typeof id); // string
    console.log(typeof parseInt(id)); // number
    console.log(parseInt(id)); // 272

    // localhost:3000/movie/abc 입력
    console.log(parseInt(id)); // NaN
  };

  render() {
    console.log(this.props);
    ...
  }
}
```

> `cdm`의 `console.log(…);`들을 제거한다.
>
> `render()`의 `console.log(this.props);`는 남겨 둔다.

<br>

- Redirect 설정

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      },
      history: { push }
    } = this.props;

    // For Redirect
    const parsedId = parseInt(id);

    if (isNaN(parsedId)) {
      return push('/'); // return을 추가해서 함수를 종료시킨다.
    }
  };

  ...
}
```

> `/movie/abc`, `/show/abc`의 경우, `/`를 push해서 Redirect 한다.

<br>

- pathname 확인

```js
// For example

const path = '/movie/8688';
path.includes('/movie/');	// true
path.includes('/show/');	// false
```

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      },
      history: { push },
      location: { pathname }
    } = this.props;
    
    // For Redirect
    ...

    // Check movie or show
    this.isMovie = pathname.includes('/movie/');
    console.log(this.isMovie); // 확인 후 제거
  };

  render() {
    console.log(this.props); // 확인 후 제거
    ...
}
```

> `localhost:3000/movie/272`의 경우, `true`를 반환한다.
>
> `localhost:3000/show/272`의 경우, `false`를 반환한다.
>
> `console.log(this.isMovie);`를 제거한다.
>
> `console.log(this.props);`를 제거한다.

<br>

- constructor 사용

```react
...
import { movieApi, tvApi } from '../../api';

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

  // Logic (location 제거)
  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      },
      history: { push }
    } = this.props;

    // For Redirect
    ...

    // Check movie or show
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

> `this.isMovie = pathname.includes('/movie/');`를 제거한다.

> 1. `localhost:3000/movie/272`로 이동
> 2. `Console` 탭 확인

<br>

- result 덮어쓰기

```react
...

export default class extends React.Component {
  ...

  // Logic
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

  ...
}
```

<br>

- Better than before

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
  };

  render() {
    const {...} = this.state;
    console.log(result); // 확인 후 제거

    ...
  }
}
```

> `console.log(result);`를 제거한다.

<br>

<br>

###### 현재 디렉토리 구조 (변화 없음)

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