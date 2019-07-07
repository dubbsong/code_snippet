#### state 설정

###### change greeting after 2s

- App.js

```react
...

class App extends Component {
  state = {
    greeting: "What's up?"
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
        {movieData.map((movie, index) => {
          ...
        })}
        {this.state.greeting}
      </div>
    );
  }
}

...
```

> `What's up?`이 2초 후에 `All good?`으로 변경된다.

> `greeting: "What's up?"` 제거
>
> `greeting: 'All good?'` 제거
>
> `{this.state.greeting}` 제거

<br>

#### state 설정

###### move data in state / add other data after 2s

- App.js

```react
...

class App extends Component {
  state = {
    movieData: [
      {
        title: 'Batman Begins',
        poster: 'https://dummyimage.com/150x200/ff7373/fff'
      },
      {
        title: 'Batman Dark Knight',
        poster: 'https://dummyimage.com/150x200/ffc952/fff'
      },
      {
        title: 'Batman Rises',
        poster: 'https://dummyimage.com/150x200/47b8e0/fff'
      },
      {
        title: 'John Wick',
        poster: 'https://dummyimage.com/150x200/34314c/fff'
      }
    ]
  };

  componentDidMount() {
    setTimeout(() => {
      this.setState({
        movieData: [
          ...this.state.movieData,
          {
            title: 'John Wick: Reload',
            poster: 'https://dummyimage.com/150x200/c6e5d9/fff'
          }
        ]
      });
    }, 2000);
  }

  render() {
    return (
      <div className="App">
        {this.state.movieData.map((movie, index) => {
          ...
        })}
      </div>
    );
  }
}

...
```

> 2초 후에 `John Wick: Reload`가 추가된다.

<br>

#### state 설정

###### add loading

- App.js

```react
...

class App extends Component {
  state = {};

  componentDidMount() {
    setTimeout(() => {
      this.setState({
        movieData: [...]
      });
    }, 2000);
  }

  _renderMovies() {
    const movies = this.state.movieData.map((movie, index) => {
      return (
        <MovieCard key={index} poster={movie.poster} title={movie.title} />
      );
    });
    return movies;
  }

  render() {
    return (
      <div className={this.state.movieData ? 'App' : 'App__Loading'}>
        {this.state.movieData ? this._renderMovies() : 'Loading...'}
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
  ...
}

.App__Loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-size: 20px;
}
```

> 먼저 `Loading`이 2초 동안 표시되고, 그 후에 `movieData`가 표시된다.

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Components
- [x] Set Props
- [x] Set Maping
- [x] Set PropTypes
- [x] Test Lifecycle
- [x] Set State
- [] Set Stateless Component
- [] AJAX Networking
- [] Update Component
- [] Styling CSS
- [] Deploying
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Set State'
$ git push origin master
```

<br>

<br>