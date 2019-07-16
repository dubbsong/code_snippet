#### props 데이터 확인: `title`

- App.js

```react
...

const movieTitles = [
  'Batman Begins',
  'Batman Dark Knight',
  'Batman Rises',
  'John Wick'
];

class App extends Component {
  render() {
    return (
      <div className="App">
        <MovieCard title={movieTitles[0]} />
        <MovieCard title={movieTitles[1]} />
        <MovieCard title={movieTitles[2]} />
        <MovieCard title={movieTitles[3]} />
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
    console.log(this.props);	// 데이터 확인
    return (
      ...
    );
  }
}

...
```

> 콘솔에서 props 데이터를 확인할 수 있다.
>

<br>

#### props 전달: `title`

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    console.log(this.props);
    return (
      <div className="Movie__Card">
        ...
        <h2>{this.props.title}</h2>
      </div>
    );
  }
}

...
```

> title이 각각 할당된다.
>

<br>

#### props 전달: `poster`

- App.js

```react
...

const moviePoster = [
  'https://dummyimage.com/150x200/ff7373/fff',
  'https://dummyimage.com/150x200/ffc952/fff',
  'https://dummyimage.com/150x200/47b8e0/fff',
  'https://dummyimage.com/150x200/34314c/fff'
];

const movieTitles = [
  ...
];

class App extends Component {
  render() {
    return (
      <div className="App">
        <MovieCard poster={moviePoster[0]} title={movieTitles[0]} />
        <MovieCard poster={moviePoster[1]} title={movieTitles[1]} />
        <MovieCard poster={moviePoster[2]} title={movieTitles[2]} />
        <MovieCard poster={moviePoster[3]} title={movieTitles[3]} />
      </div>
    );
  }
}

...
```

<br>

- MovieCard.js

```react
import React, { Component } from 'react';
import './MovieCard.css';

class MovieCard extends Component {
  render() {
    console.log(this.props);	// 확인 후 제거
    return (
      <div className="Movie__Card">
        <img src={this.props.poster} alt="" />
        <h2>{this.props.title}</h2>
      </div>
    );
  }
}

export default MovieCard;
```

> poster가 각각 할당된다.
>
> `console.log(this.props);`를 제거한다.

<br>

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Component
- [x] Set Props
- [] Set Maping
- [] Set PropTypes
- [] Test Lifecycle
- [] Set State
- [] Set Stateless Component
- [] Set AJAX Networking
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
$ git commit -m 'Set Props'
$ git push origin master
```

<br>

<br>