#### 용어 정리

> `AJAX`
>
> Asynchronous JavaScript and XML
>
> 비동기식 정보 교환 기법
>
> 규칙적인 시간 관계가 없는 것으로, 프로그램 실행에서는 명령 순서 예측이 불가능한 것.
>
> 시스템 간의 상호 작용이 어느 정도의 시차를 두고 일어나는 것.

> `JSON`
>
> JavaScript Object Notation
>
> key:value 쌍으로 이루어진 객체 데이터 포맷

> `fetch`
>
> 사전적 의미: 가지고 오다
>
> "얻어서 가져 오는 것"의 의미이지만, 명령을 얻으러 가는 것을 말한다.

> `Promise`
>
> 사전적 의미: 약속하다
>
> "지금은 없으니까 이따가 줄게"라는 의미이다.
>
> 첫 번째 라인이 끝나든 말든, 두 번째 라인을 작업한다.

> `then`
>
> 사전적 의미: 그 다음에

> `catch`
>
> 사전적 의미: 잡다
>
> 주로 에러를 나타낸다.

> `async`
>
> Asynchronous Communication
>
> 비동기 통신
>
> 정보를 일정한 속도로 보낼 것을 요구하지 않는 데이터 전송 방법.

> `await`
>
> 사전적 의미: ~을 기다리다

> `fetch`와 `Promise`가 좋은 이유는, 시나리오가 생기고 이를 관리할 수 있기 때문이다.

<br>

#### Movie DB

1. https://yts.lt/api 이동
2. HTTP GET `https://yts.lt/api/v2/list_movies.json` 확인
3. Parameter `sort_by` 확인
4. Type `download_count` 확인
5. JSON data `https://yts.lt/api/v2/list_movies.json?sort_by=download_count` 확인
6. Response `movies`(array) 확인

<br>

#### fetch 추가 (API 확인)

- App.js

```react
...

class App extends Component {
  state = {};

  componentDidMount() {
    fetch('https://yts.lt/api/v2/list_movies.json?sort_by=download_count');
  }

  ...
}

...
```

> 1. 개발자 도구
> 2. `Network` 탭
> 3. `list_movies.json?sort_by=download_count` API status 확인
> 4. `data: movies: [{…}, {…}, ...]` 확인

<br>

#### then / catch 추가

- App.js

```react
...

class App extends Component {
  state = {};

  componentDidMount() {
    fetch('https://yts.lt/api/v2/list_movies.json?sort_by=download_count')
      .then(response => console.log(response))
      .catch(err => console.log(err));
  }

  ...
}

...
```

> Console 탭에서 `Response {...}`를 확인할 수 있다.
>
> body의 `ReadableStream`은 바이트(010101…)로 구성되었다는 것을 의미한다.
>
> 고로 JSON으로 변경해야 한다.

<br>

#### response를 JSON으로 변경

- App.js

```react
...

class App extends Component {
  state = {};

  componentDidMount() {
    fetch('https://yts.lt/api/v2/list_movies.json?sort_by=download_count')
      .then(response => response.json())
      .then(json => console.log(json))
      .catch(err => console.log(err));
  }

  ...
}

...
```

> `data: movies: Array(20)` 확인
>
> `id`, `medium_cover_image`, `title_english`, `genres (array)`, `synopsis`가 필요하다.

<br>

```react
...

class App extends Component {
  state = {};

  componentDidMount() {
    fetch('https://yts.lt/api/v2/list_movies.json?sort_by=download_count')
      .then(response => response.json())
      .then(json => json.data.movies)
      .catch(err => console.log(err));
  }

  ...
}

...
```

<br>

#### Async / Await 추가

- App.js

```react
import React, { Component } from 'react';
import './App.css';
import MovieCard from './MovieCard';

class App extends Component {
  state = {};

  componentDidMount() {
    this.getMovies();
  }

  async getMovies() {
    const movieData = await this.callApi();

    this.setState({
      movieData: movieData
    });
  }

  callApi() {
    return fetch(
      'https://yts.lt/api/v2/list_movies.json?sort_by=download_count'
    )
      .then(response => response.json())
      .then(json => json.data.movies)
      .catch(err => console.log(err));
  }

  renderMovies() {
    const movies = this.state.movieData.map(movie => {
      return (
        <MovieCard
          poster={movie.medium_cover_image}
          title={movie.title_english}
          key={movie.id}
        />
      );
    });
    return movies;
  }

  render() {
    ...
  }
}

...
```

> 1. render()
> 2. cdm()
> 3. getMovies()
> 4. callApi()
> 5. render()
> 6. renderMovies()

<br>

#### title 길이 수정

- MovieCard.js

```react
<h2>
  {title.length > 15 ? `${title.substring(0, 15)}...` : title}
</h2>
```

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Component
- [x] Set Props
- [x] Set Maping
- [x] Set PropTypes
- [x] Test Lifecycle
- [x] Set State
- [x] Set Stateless Component
- [x] Set AJAX Networking
- [] Update Component
- [] Styling CSS
- [] Refactoring
- [] Deploying
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Set AJAX Networking'
$ git push origin master
```

<br>

<br>