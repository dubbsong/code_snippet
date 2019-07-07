#### 데이터 확인

- App.js

```react
...

class App extends Component {
  ...

  _renderMovies() {
    const movies = this.state.movieData.map(movie => {
      console.log(movie);
      return (
        <MovieCard
          key={movie.id}
          poster={movie.medium_cover_image}
          title={movie.title_english}
        />
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

#### 데이터 가져오기 & PropTypes 설정 & HTML 작성

- App.js

```react
...

class App extends Component {
  ...

  _renderMovies() {
    const movies = this.state.movieData.map(movie => {
      console.log(movie);	// 데이터 확인 후 제거
      return (
        <MovieCard
          key={movie.id}
          poster={movie.medium_cover_image}
          title={movie.title_english}
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

<br>

- MovieCard.js

```react
...

function MovieCard({ poster, title, genres, synopsis }) {
  return (
    <div className="Movie__Card">
      <div className="Movie__Column">
        <MoviePoster poster={poster} />
      </div>
      <div className="Movie__Column">
        <h2>{title.length > 15 ? `${title.substring(0, 15)}...` : title}</h2>
        <div className="Movie__Genres">
          {genres.map((genre, index) => (
            <MovieGenre genre={genre} key={index} />
          ))}
        </div>
        <p className="Movie__Synopsis">{synopsis}</p>
      </div>
    </div>
  );
}

function MoviePoster({ poster }) {
  return <img src={poster} alt="" className="Movie__Poster" />;
}

function MovieGenre({ genre }) {
  return <span className="Movie__Genre">{genre}</span>;
}

MovieCard.propTypes = {
  poster: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired,
  genres: PropTypes.array.isRequired,
  synopsis: PropTypes.string.isRequired
}

...

MovieGenre.propTypes = {
  genre: PropTypes.string.isRequired
};

...
```

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
- [x] Set Stateless Component
- [x] Set AJAX Networking
- [x] Update Component
- [] Styling CSS
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