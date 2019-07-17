#### 프로젝트 생성: `movie_app`

```bash
$ cd Documents
$ cd deploying
$ npx create-react-app movie_app
```

<br>

#### VSCode 실행

```bash
$ cd movie_app
$ code .
```

<br>

#### 파일 제거

- src/App.test.js
- logo.svg
- serviceWorker.js

<br>

#### 코드 수정

- public/index.html

```html
<link href="https://fonts.googleapis.com/css?family=Ubuntu&display=swap" rel="stylesheet">
<title>Movie App</title>
```

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

<br>

- index.css

```css
body {
  font-family: 'Ubuntu', sans-serif;
  margin: 0;
}
```

<br>

- App.js

```react
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <h4>What's up?</h4>
      </div>
    );
  }
}

export default App;
```

<br>

- App.css

```css
.App {
  text-align: center;
}
```

<br>

#### React 실행

```bash
$ yarn start
```

> 화면에 `What's up?`이 표시된다.

<br>

<br>

#### 컴포넌트 생성: `MovieCard`

```bash
$ cd src
$ touch MovieCard.js
$ touch MovieCard.css
```

<br>

#### 코드 작성: `MovieCard`

```react
import React, { Component } from 'react';
import './MovieCard.css';

class MovieCard extends Component {
  render() {
    return (
      <div className="Movie__Card">
        <img src="https://dummyimage.com/150x200/ff7373/fff" alt="" />
        <h4>Movie Title</h4>
      </div>
    );
  }
}

export default MovieCard;
```

<br>

#### Import MovieCard

- App.js

```react
...
import MovieCard from './MovieCard';

class App extends Component {
  render() {
    return (
      <div className="App">
        <MovieCard />
      </div>
    );
  }
}

...
```

> 화면에 이미지 \+ 제목이 표시된다.

<br>

#### 더미 데이터 추가: `data`

- App.js

```react
...

const data = [
  {
    cover_img: 'https://dummyimage.com/150x200/ff7373/fff',
    title_english: 'Batman Begins'
  },
  {
    cover_img: 'https://dummyimage.com/150x200/ffc952/fff',
    title_english: 'Batman Dark Knight'
  },
  {
    cover_img: 'https://dummyimage.com/150x200/47b8e0/fff',
    title_english: 'Batman Rises'
  },
  {
    cover_img: 'https://dummyimage.com/150x200/34314c/fff',
    title_english: 'John Wick'
  }
];

class App extends Component {
  ...
}

...
```

<br>

#### props 데이터 확인

- App.js

```react
...

class App extends Component {
  render() {
    return (
      <div className="App">
        {data.map((movie, index) => {
          return (
            <MovieCard
              poster={movie.cover_img}
              title={movie.title_english}
              key={index}
            />
          );
        })}
      </div>
    );
  }
}

...
```

<br>

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    console.log(this.props);

    return (
      ...
    );
  }
}

...
```

> Console 탭에 props 데이터가 표시된다.

<br>

#### props 전달

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    console.log(this.props);	// 제거

    return (
      <div className="Movie__Card">
        <img src={this.props.poster} alt="" />
        <h4>{this.props.title}</h4>
      </div>
    );
  }
}

...
```

> 화면에 4개의 `MovieCard`가 표시된다.
>
> `console.log(this.props);`를 제거한다.

<br>

#### Styling CSS

- App.css

```css
.App {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 50px;
  text-align: center;
}
```

> 모바일 크기는 `flex-wrap: wrap;`으로 조작한다.

<br>

#### prop-types 설치

```bash
$ yarn add prop-types
```

<br>

#### prop-types 설정

- MovieCard.js

```react
...
import PropTypes from 'prop-types';

class MovieCard extends Component {
  ...
}

MovieCard.propTypes = {
  poster: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired
};

...
```

<br>

#### state 변경 01: `greeting`

- App.js

```react
class App extends Component {
  state = {
    greeting: 'Wassup?'
  };
  
  componentDidMount() {
    setTimeout(() => {
      this.setState({
        greeting: 'All good?'
      });
    }, 2000);
  }
  
  render() {
    return (
      <div className="App">
        ...
        {this.state.greeting}
      </div>
    );
  }
}
```

> `Wassup?`이 2초 후에 `All good?`으로 변경된다.

<br>

#### state 변경 02: `Loading`

- App.js

```react
import React, { Component } from 'react';
import './App.css';
import MovieCard from './MovieCard';

class App extends Component {
  state = {};

  componentDidMount() {
    console.log('Did cdm');	// 확인 후 제거
    setTimeout(() => {
      this.setState({
        data: [
          {
            cover_img: 'https://dummyimage.com/150x200/ff7373/fff',
            title_english: 'Batman Begins'
          },
          {
            cover_img: 'https://dummyimage.com/150x200/ffc952/fff',
            title_english: 'Batman Dark Knight'
          },
          {
            cover_img: 'https://dummyimage.com/150x200/47b8e0/fff',
            title_english: 'Batman Rises'
          },
          {
            cover_img: 'https://dummyimage.com/150x200/34314c/fff',
            title_english: 'John Wick'
          }
        ]
      });
    }, 2000);
  }

  renderMovies = () => {
    console.log('Did renderMovies');	// 확인 후 제거
    const movies = this.state.data.map((movie, index) => {
      return (
        <MovieCard
          poster={movie.cover_img}
          title={movie.title_english}
          key={index}
        />
      );
    });
    return movies;
  };

  render() {
    console.log('Did render');	// 확인 후 제거
    return (
      <div className="App">
        {this.state.data ? this.renderMovies() : 'Loading...'}
      </div>
    );
  }
}

...
```

> **Console 탭 확인:**
>
> 1. Did render
> 2. Did cdm
> 3. Did render
> 4. Did renderMovies

> `Loading…` 2초 후, 4개의 `MovieCard`가 표시된다.
>
> 모든 `console.log(…);`를 제거한다.

<br>

#### 함수형 컴포넌트: `stateless`

- MovieCard.js

```react
import React from 'react';
...

function MovieCard({ poster, title }) {
  return (
    <div className="Movie__Card">
      <img src={poster} alt="" />
      <h4>{title}</h4>
    </div>
  );
}

MovieCard.propTypes = {
  ...
};

...
```

<br>

#### AJAX 설정: `App.js`

- Movie DB 확인
  1. [LTS](https://yts.lt/api)로 이동
  2. HTTP GET `https://yts.lt/api/v2/list_movies.json` 확인
  3. Parameter `sort_by` 확인
  4. Type `download_count` 확인
  5. JSON 데이터 `https://yts.lt/api/v2/list_movies.json?sort_by=download_count` 확인
  6. Response Data `movies` 확인 (ARRAY)

<br>

- API 확인: `fetch`

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
> 3. `list_movies.json?sort_by=download_count` 클릭
> 4. `data`의 `movies` 확인

<br>

- Response 확인: `then`, `catch`

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

> Console 탭 `Response {…}`가 표시된다.
>
> `body`의 `ReadableStream`은 바이트(010101…)로 구성되었다는 것을 의미한다. 고로 JSON으로 변경해야 한다.

<br>

- Response를 JSON으로 변경

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

> `data`에서 `movies: Array(20)`를 확인할 수 있다.
>
> `id`, `medium_cover_image`, `genres`, `synopsis`가 필요하다.
>
> `genres`의 데이터 타입은 `Array`이다.
>
> `id`, `medium_cover_image`, `synopsis`의 데이터 타입은 `String`이다.

<br>

- 데이터 가져오기 설정

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

- 데이터 전달

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
    const data = await this.callApi();

    this.setState({
      data: data
    });
  }

  callApi = () => {
    return fetch(
      'https://yts.lt/api/v2/list_movies.json?sort_by=download_count'
    )
      .then(response => response.json())
      .then(json => json.data.movies)
      .catch(err => console.log(err));
  };

  renderMovies = () => {
    const movies = this.state.data.map(movie => {
      return (
        <MovieCard
          poster={movie.medium_cover_image}
          title={movie.title_english}
          key={movie.id}
        />
      );
    });
    return movies;
  };

  ...
}

...
```

> 화면에 포스터와 타이틀이 표시된다.

<br>

#### 데이터 확인

- App.js

```react
...

class App extends Component {
  ...

  renderMovies = () => {
    const movies = this.state.data.map(movie => {
      console.log(movie);	// 데이터 확인
      return (
        ...
      );
    });
    return movies;
  };

  ...
}

...
```

> `genres`, `synopsis`가 필요하다.

<br>

#### 데이터 전달: `genres`, `synopsis`

- App.js

```react
...

class App extends Component {
  ...

  renderMovies = () => {
    const movies = this.state.data.map(movie => {
      console.log(movie);	// 확인 후 제거
      return (
        <MovieCard
          ...
          genres={movie.genres}
          synopsis={movie.synopsis}
          key={movie.id}
        />
      );
    });
    return movies;
  };

  ...
}

...
```

> `console.log(movie);`를 제거한다.

<br>

- MovieCard.js

```react
...

function MovieCard({ poster, title, genres, synopsis }) {
  return (
    <div className="Movie__Card">
      <div className="Movie__Column">
        <img src={poster} alt="" className="Movie__Poster" />
      </div>
      <div className="Movie__Column">
        <h4>{title}</h4>
        <p className="Movie__Genres">{genres}</p>
        <p className="Movie__Synopsis">{synopsis}</p>
      </div>
    </div>
  );
}

MovieCard.propTypes = {
  ...
  genres: PropTypes.array.isRequired,
  synopsis: PropTypes.string.isRequired
};

...
```

<br>

#### Styling CSS

- App.css

```css
.App {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 50px;
}
```

> `text-align: center;` 제거

<br>

- MovieCard.css

```css
.Movie__Card {
  width: 40%;
  box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.2);
  padding: 0 20px;
  margin-bottom: 50px;
  display: flex;
  justify-content: space-between;
}

.Movie__Card h4 {
  font-size: 20px;
}

.Movie__Column {
  width: 30%;
}

.Movie__Column:last-child {
  width: 60%;
  padding: 20px 0;
}

.Movie__Poster {
  max-width: 100%;
  position: relative;
  top: -20px;
  box-shadow: -10px 20px 40px rgba(0, 0, 0, 0.2),
    10px 15px 15px rgba(0, 0, 0, 0.2);
}

.Movie__Genres {
  margin-bottom: 20px;
}

.Movie__Synopsis {
  color: #b4b5bd;
}

@media screen and (min-width: 320px) and (max-width: 667px) {
  .Movie__Card {
    width: 100%;
    flex-direction: column;
    padding-top: 20px;
  }

  .Movie__Column {
    width: 100% !important;
  }

  .Movie__Poster {
    width: 100%;
    top: 0;
    left: 0;
  }
}
```

<br>

#### LinesEllipsis 설치

```bash
$ yarn add react-lines-ellipsis
```

> [react-lines-ellipsis](https://www.npmjs.com/package/react-lines-ellipsis) 참조

<br>

#### LinesEllipsis 추가

- MovieCard.js

```react
...
import LinesEllipsis from 'react-lines-ellipsis';

function MovieCard({ ... }) {
  return (
    <div className="Movie__Card">
      ...
        ...
        <p className="Movie__Synopsis">
          <LinesEllipsis
            text={synopsis}
            maxLine="5"
            ellipsis="..."
            trimRight
            basedOn="letters"
          />
        </p>
      ...
    </div>
  );
}

...
```

> `synopsis`의 텍스트가 5줄 초과일 경우, `...`으로 대체된다.

<br>

#### Refactoring: `MovieGenre` 컴포넌트 추가

- MovieCard.js

```react
...

function MovieCard({ ... }) {
  return (
    <div className="Movie__Card">
      ...
        ...
        <div className="Movie__Genres">
          {genres.map((genre, index) => (
            <MovieGenre genre={genre} key={index} />
          ))}
        </div>
        ...
      ...
    </div>
  );
}

function MovieGenre({ genre }) {
  return <span className="Movie__Genre">{genre} </span>;
}

MovieCard.propTypes = {
  ...
};

MovieGenre.propTypes = {
  genre: PropTypes.string.isRequired
};

...
```

<br>

- MovieCard.css

```css
.Movie__Genre {
  color: #b4b5bd;
}
```

<br>

<br>