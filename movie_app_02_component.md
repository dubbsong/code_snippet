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
        <h2>Batman Begins</h2>
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

> 화면에 `Batman Begins`가 표시된다.

<br>

#### 포스터 이미지 추가

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    return (
      <div className="Movie__Card">
        <img src="https://dummyimage.com/150x200/ff7373/fff" alt="" />
        <h2>Batman Begins</h2>
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
  padding: 50px;
}
```

> 4개의 `<MovieCard />` 컴포넌트가 화면에 표시된다.
>
> 모바일 크기도 확인한다.

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Component
- [] Set Props
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
$ git commit -m 'Add Component'
$ git push origin master
```

<br>

<br>