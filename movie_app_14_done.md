#### 코드 확인

- App.js

```react
import React, { Component } from 'react';
import './App.css';
import MovieCard from './MovieCard';

class App extends Component {
  state = {};

  componentDidMount() {
    this.getMovies();
  }

  async getMovies() {
    const movieData = await this.callApi();

    this.setState({
      movieData: movieData
    });
  }

  callApi() {
    return fetch(
      'https://yts.lt/api/v2/list_movies.json?sort_by=download_count'
    )
      .then(response => response.json())
      .then(json => json.data.movies)
      .catch(err => console.log(err));
  }

  renderMovies() {
    const movies = this.state.movieData.map(movie => {
      return (
        <MovieCard
          poster={movie.medium_cover_image}
          title={movie.title_english}
          key={movie.id}
          genres={movie.genres}
          synopsis={movie.synopsis}
        />
      );
    });
    return movies;
  }

  render() {
    return (
      <div className={this.state.movieData ? 'App' : 'App__Loading'}>
        {this.state.movieData ? this.renderMovies() : 'Loading...'}
      </div>
    );
  }
}

export default App;
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

.App__Loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60vh;
  font-size: 20px;
  color: #b4b5bd;
}
```

<br>

- MovieCard.js

```react
import React from 'react';
import './MovieCard.css';
import PropTypes from 'prop-types';
import LinesEllipsis from 'react-lines-ellipsis';

function MovieCard({ poster, title, genres, synopsis }) {
  return (
    <div className="Movie__Card">
      <div className="Movie__Column">
        <img src={poster} alt="" className="Movie__Poster" />
      </div>
      <div className="Movie__Column">
        <h2>{title}</h2>
        <div className="Movie__Genres">
          {genres.map((genre, index) => (
            <MovieGenre genre={genre} key={index} />
          ))}
        </div>
        <div className="Movie__Synopsis">
          <LinesEllipsis
            text={synopsis}
            maxLine="5"
            ellipsis="..."
            trimRight
            basedOn="letters"
          />
        </div>
      </div>
    </div>
  );
}

function MovieGenre({ genre }) {
  return <span className="Movie__Genre">{genre}</span>;
}

MovieCard.propTypes = {
  poster: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired,
  genres: PropTypes.array.isRequired,
  synopsis: PropTypes.string.isRequired
};

MovieGenre.propTypes = {
  genre: PropTypes.string.isRequired
};

export default MovieCard;
```

<br>

- MovieCard.css

```css
.Movie__Card {
  width: 40%;
  box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.2);
  padding: 0 20px;
  margin-bottom: 50px;
  display: flex;
  justify-content: space-between;
}

.Movie__Card h2 {
  font-size: 20px;
}

.Movie__Column {
  width: 30%;
}

.Movie__Column:last-child {
  width: 60%;
  padding: 20px 0;
}

.Movie__Poster {
  max-width: 100%;
  position: relative;
  top: -20px;
  box-shadow: -10px 20px 40px rgba(0, 0, 0, 0.2),
    10px 15px 15px rgba(0, 0, 0, 0.2);
}

.Movie__Genres {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.Movie__Genre {
  color: #b4b5bd;
  margin-right: 10px;
}

.Movie__Synopsis {
  color: #b4b5bd;
}

@media screen and (min-width: 320px) and (max-width: 667px) {
  .Movie__Card {
    width: 100%;
    flex-direction: column;
    padding-top: 20px;
  }

  .Movie__Column {
    width: 100% !important;
  }

  .Movie__Poster {
    width: 100%;
    top: 0;
    left: 0;
  }
}
```

<br>

<br>