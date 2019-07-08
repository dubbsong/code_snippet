#### state 01

###### Change greeting after 2s

- App.js

```react
...

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

...
```

> `Wassup`이 2초 후에 `All good?`으로 변경된다.

> `greeting: 'Wassup?'` 제거
>
> `greeting: 'All good?'` 제거
>
> `{this.state.greeting}` 제거

<br>

#### state 02

###### Add other data after 2s

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
            poster: 'https://dummyimage.com/150x200/998ac5/fff'
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

#### state 03

###### Add Loading

- App.js

```react
...

class App extends Component {
  state = {};

  componentDidMount() {
    setTimeout(() => {
      this.setState({
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
      });
    }, 2000);
  }

  renderMovies() {
    const movies = this.state.movieData.map((movie, index) => {
      return (
        <MovieCard
          poster={movie.poster}
          title={movie.title}
          key={index}
        />
      );
    });
    return movies;
  }

  render() {
    return (
      <div className={this.state.movieData ? 'App' : 'App_Loading'}>
        {this.state.movieData ? this.renderMovies() : 'Loading...'}
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
  height: 60vh;
  font-size: 20px;
  color: #b4b5bd;
}
```

> 먼저 `Loading`이 2초 동안 표시되고, 그 후에 `movieData`가 표시된다.

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
- [] Set Stateless Component
- [] AJAX Networking
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
$ git commit -m 'Set State'
$ git push origin master
```

<br>

<br>