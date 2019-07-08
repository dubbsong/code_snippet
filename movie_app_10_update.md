#### 데이터 확인

- App.js

```react
...

class App extends Component {
  ...

  renderMovies() {
    const movies = this.state.movieData.map(movie => {
      console.log(movie);	// 데이터 확인
      return (
        ...
      );
    });
    return movies;
  }

  ...
}

...
```

> `id`, `title_english`, `medium_cover_image`, `genres`, `synopsis`가 필요하다.

<br>

#### props 연결

###### genres, synopsis 추가

- App.js

```react
...

class App extends Component {
  ...

  renderMovies() {
    const movies = this.state.movieData.map(movie => {
      console.log(movie);	// 데이터 확인 후 제거
      return (
        <MovieCard
          ...
          genres={movie.genres}
          synopsis={movie.synopsis}
        />
      );
    });
    return movies;
  }

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
        <h2>{title.length > 15 ? `${title.substring(0, 15)}...` : title}</h2>
        <p className="Movie__Genres">{genres}</p>
        <p className="Movie__Synopsis">{synopsis}</p>
      </div>
    </div>
  );
}

MovieCard.propTypes = {
  poster: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired,
  genres: PropTypes.array.isRequired,
  synopsis: PropTypes.string.isRequired
};

...
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
- [x] Update Component
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
$ git commit -m 'Update Component'
$ git push origin master
```

<br>

<br>