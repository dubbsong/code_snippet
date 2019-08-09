###### 코드 작성: `MovieContainer`

1. 데이터 설정

```react
...
import { movieApi } from 'api';

export default class extends React.Component {
  ...

  // Logic
  async componentDidMount() {
    try {
      const nowPlaying = await movieApi.nowPlaying();
      const topRated = await movieApi.topRated();
      console.log(nowPlaying, topRated);
    } catch {
      this.setState({ error: "Can't find movie information." });
    } finally {
      this.setState({ loading: false });
    }
  }

  ...
}
```

> 1. `Movies` 클릭
> 2. 개발자 도구 `Console` 탭 클릭
> 3. `nowPlaying`, `topRated` 확인

2. state 설정
   - [구조 분해 할당](https://github.com/dubbsong/code_snippet/blob/master/es6_02_destructuring%20assignment.md) 사용

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
      const {
        data: { results: topRated }
      } = await movieApi.topRated();

      this.setState({
        nowPlaying: nowPlaying,
        topRated: topRated
      });
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    console.log(this.state);

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화 확인

3. Error 확인

```react
...

export default class extends React.Component {
  ...

  // Logic
  async componentDidMount() {
    try {
      ...

      throw Error(); // 확인 후 제거

      ...
    } catch {
      ...
    } finally {
      ...
    }
  }

  render() {
    console.log(this.state); // 확인 후 제거

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화 확인
>
> `throw Error();` 제거
>
> `console.log(this.state);` 제거

<br>

###### 코드 작성: `TVContainer`

1. 데이터 설정

```react
...
import { tvApi } from 'api';

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    try {
      const topRated = await tvApi.topRated();
      const popular = await tvApi.popular();
      console.log(topRated, popular);
    } catch {
      this.setState({ error: "Can't find tv information." });
    } finally {
      this.setState({ loading: false });
    }
  };

  ...
}
```

> 1. `TV Shows` 클릭
> 2. 개발자 도구 `Console` 탭 클릭
> 3. `topRated`, `popular` 확인

2. state 설정

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
      const {
        data: { results: popular }
      } = await tvApi.popular();

      this.setState({
        topRated: topRated,
        popular: popular
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {
    console.log(this.state);

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화 확인

3. Error 확인

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    try {
      ...

      throw Error(); // 확인 후 제거

      ...
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {
    console.log(this.state); // 확인 후 제거

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화 확인
>
> `throw Error();` 제거
>
> `console.log(this.state);` 제거

<br>

###### 코드 작성: `SearchContainer`

1. 데이터 확인

```react
...
import { movieApi, tvApi } from 'api';

export default class extends React.Component {
  state = {
    ...
    searchWord: 'begins', // For test
    ...
  };

  // Logic
  searchByWord = async () => {
    try {
      const movieResults = await movieApi.search(this.state.searchWord);
      const tvResults = await tvApi.search(this.state.searchWord);
      console.log(movieResults, tvResults);
    } catch {
      this.setState({ error: "Can't find results." });
    } finally {
      this.setState({ loading: false });
    }
  };

  handleSubmit = () => {
    if (this.state.searchWord !== '') {
      this.searchByWord();
    }
  };

  // For test
  componentDidMount() {
    this.handleSubmit();
  }

  ...
}
```

> 1. `🔍` 클릭
> 2. 개발자 도구 `Console` 탭 클릭
> 3. `movieResults`, `tvResults` 확인

2. 구조 분해 할당

```react
...

export default class extends React.Component {
  state = {
    ...
    searchWord: 'begins', // 확인 후 ''로 변경
    ...
  };

  // Logic
  searchByWord = async () => {
    try {
      const {
        data: { results: movieResults }
      } = await movieApi.search(this.state.searchWord);
      const {
        data: { results: tvResults }
      } = await tvApi.search(this.state.searchWord);

      this.setState({
        movieResults: movieResults,
        tvResults: tvResults
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  handleSubmit = () => {
    if (this.state.searchWord !== '') {
      this.searchByWord();
    }
  };

  // 확인 후 제거
  componentDidMount() {...}

  render() {
    console.log(this.state); // 확인 후 제거

    ...
  }
}
```

> `Console` 탭에서 state의 3가지 변화 확인
>
> `'begins'`를 `''`로 변경
>
> `componentDidMount() {...}` 제거
>
> `console.log(this.state);` 제거

3. props 전달: `handleSubmit`

```react
...

export default class extends React.Component {
  ...

  render() {
    return (
      <SearchPresenter
        ...
        handleSubmit={this.handleSubmit}
      />
    );
  }
}
```

> `searchWord` 업데이트 함수는 나중에 작성한다.

<br>

###### 코드 작성: `DetailContainer`

1. props 확인

```react
...

export default class extends React.Component {
  ...

  // Logic

  render() {
    console.log(this.props);

    ...
  }
}
```

> 1. `localhost:3000/movie/272`로 이동
> 2. `match` / `params` / `id: "272"` 확인
> 3. `location` / `pathname: "/movie/272"` 확인

2. `id` 데이터 타입 확인 \& `id` 설정

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

    // For test
    console.log(id);                  // 272
    console.log(typeof id);           // string
    console.log(typeof parseInt(id)); // number
    console.log(parseInt(id));        // 272

    // Set id
    const parsedId = parseInt(id);
  };

  ...
}
```

> 1. `localhost:3000/movie/272` 이동
> 2. `Console` 탭에서 각 출력 확인
>
> `For test` 제거

3. `Movie` or `show` 확인

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
      location: { pathname }
    } = this.props;

    // Set id
    ...

    // Check movie or show
    this.isMovie = pathname.includes('/movie/');
    console.log(this.isMovie); // 확인 후 제거
  };

  render() {
    console.log(this.props); // 확인 후 제거

    ...
  }
}
```

> `localhost:3000/movie/272`: true
>
> `localhost:3000/show/272`: false
>
> `console.log(this.isMovie);` 제거
>
> `console.log(this.props);` 제거

4. constructor 설정 \& 로직 작성

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
      loading: true,
      detailResult: null,
      error: null,
      isMovie: pathname.includes('/movie/')
    };
  }

  // Logic
  componentDidMount = async () => {
    const {
      match: {
        params: { id }
      }
    } = this.props;

    const parsedId = parseInt(id);
    let detailResult = null;

    try {
      if (this.state.isMovie) {
        detailResult = await movieApi.movieDetail(parsedId);
      } else {
        detailResult = await tvApi.tvDetail(parsedId);
      }
    } catch {
      this.setState({ error: "Can't find anything." });
    } finally {
      this.setState({ loading: false, detailResult });
    }
  };

  render() {
    console.log(this.state);

    ...
  }
}
```

> `Console` 탭에서 `result` 확인
>
> `Check movie or show` 제거

5. result 덮어쓰기

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    ...

    try {
      if (this.state.isMovie) {
        const request = await movieApi.movieDetail(parsedId);
        detailResult = request.data;
      } else {
        const request = await tvApi.tvDetail(parsedId);
        detailResult = request.data;
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

6. Better than before

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    ...

    try {
      if (this.state.isMovie) {
        ({ data: detailResult } = await movieApi.movieDetail(parsedId));
      } else {
        ({ data: detailResult } = await tvApi.tvDetail(parsedId));
      }
    } catch {
      ...
    } finally {
      ...
    }
  };

  render() {
    console.log(this.state); // 확인 후 제거

    ...
  }
}
```

> `console.log(result);` 제거

<br>

<br>