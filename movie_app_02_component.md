#### MovieCard 컴포넌트 연결

- 파일 생성

```bash
$ cd src
$ touch MovieCard.js
$ touch MovieCard.css
```

<br>

- MovieCard.js

```react
import React, { Component } from 'react';
import './MovieCard.css';

class MovieCard extends Component {
  render() {
    return (
      <div className="Movie__Card">
        <h2>All good?</h2>
      </div>
    );
  }
}

export default MovieCard;
```

<br>

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

> 화면에 `All good?`이 표시된다.

<br>

#### 컴포넌트 생성 (MoviePoster)

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    return (
      <div className="Movie__Card">
        <MoviePoster />
        <h2>All good?</h2>
      </div>
    );
  }
}

class MoviePoster extends Component {
  render() {
    return <img src="https://dummyimage.com/150x200/ff7373/fff" alt="" />;
  }
}

...
```

<br>

- App.js

```react
...

class App extends Component {
  render() {
    return (
      <div className="App">
        <MovieCard />
        <MovieCard />
        <MovieCard />
        <MovieCard />
      </div>
    );
  }
}

...
```

<br>

- App.css

```css
.App {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  text-align: center;
  padding: 50px;
  height: 100%;
}
```

> 4개의 `<MovieCard />` 컴포넌트가 화면에 표시된다.

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Add Components'
$ git push origin master
```

<br>

<br>