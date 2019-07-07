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
    return <h2>All good?</h2>;
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
      <div>
        <MovieCard />
      </div>
    );
  }
}

...
```

<br>

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
  font-size: 14px;
  padding: 50px;
}

.App-loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
```

<br>

- MovieCard.css

```css
.Movie__Card {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-start;
  width: 20%;
  padding: 20px;
  box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3), 0 5px 12px rgba(133, 133, 133, 0.22);
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