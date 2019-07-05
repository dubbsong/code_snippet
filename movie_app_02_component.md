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

> 화면에 `All good?`이 표시된다.

<br>

#### MoviePoster 컴포넌트 연결

- 파일 생성

```bash
$ cd src
$ touch MoviePoster.js
$ touch MoviePoster.css
```

<br>

- MoviePoster.js

```react
import React, { Component } from 'react';
import './MoviePoster.css';

class MoviePoster extends Component {
  render() {
    return <img src="https://dummyimage.com/150x200/ff7373/fff" alt="" />;
  }
}

export default MoviePoster;
```

<br>

- MovieCard.js

```react
...
import MoviePoster from './MoviePoster';

class MovieCard extends Component {
  render() {
    return (
      <div>
        <MoviePoster />
        <h2>Dummy Title</h2>
      </div>
    );
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
      <div>
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

> 4개의 `<MovieCard />` 컴포넌트가 화면에 표시된다.

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Add MovieCard and MoviePoster Component'
$ git push origin master
```

<br>

<br>