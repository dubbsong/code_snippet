#### 데이터 확인

- App.js

```react
_renderMovies = () => {
  const movies = this.state.movieData.map(movie => {
    console.log(movie);
    return (
      ...
    );
  })
}
```

> `id`, `title_english`, `medium_cover_image`, `genres`, `synopsis`가 필요하다.

<br>

#### 데이터 가져오기 & PropTypes 설정 & HTML 작성

- App.js

```react
...

class App extends Component {
  ...

  _renderMovies = () => {
    const movies = this.state.movieData.map(movie => {
      console.log(movie);
      return (
        <MovieCard
          key={movie.id}
          poster={movie.medium_cover_image}
          title={movie.title}
          genres={movie.genres}
          synopsis={movie.synopsis}
        />
      );
    });
    return movies;
  };

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
        <MoviePoster poster={poster} alt={title} />
      </div>
      <div className="Movie__Column">
        <h2>{title}</h2>
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

function MoviePoster({ poster, alt }) {
  return <img src={poster} alt={alt} className="Movie__Poster" />;
}

function MovieGenre({ genre }) {
  return <span className="Movie__Genre">{genre}</span>;
}

MovieCard.propTypes = {
  ...
  genres: PropTypes.array.isRequired,
  synopsis: PropTypes.string.isRequired
};

MoviePoster.propTypes = {
  ...
  alt: PropTypes.string.isRequired
};

MovieGenre.propTypes = {
  genre: PropTypes.string.isRequired
};

...
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