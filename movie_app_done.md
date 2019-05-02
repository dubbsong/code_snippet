- App.js

```react
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

class App extends Component {
  state = {};
  
  componentDidMount() {
    this._getMovies();
  }
  
  _renderMovies = () => {
    const movies = this.state.movies.map(movie => {
      console.log(movie);
      
      return (
        <Movie
          title={movie.title_english}
          poster={movie.medium_cover_image}
          key={movie.id}
          genres={movie.genres}
          synopsis={movie.synopsis}
        />
      );
    });
    return movies;
  };
  
  _getMovies = async() => {
    const movies = await this._callApi();
    this.setState({
      movies
    });
  };
  
  _callApi = () => {
    return fetch(
      'https://yts.am/api/v2/list_movies.json?sort_by=download_count'
    )
    	.then(response => response.json())
    	.then(json => json.data.movies)
    	.catch(err => console.log(err));
  };
  
  render() {
    const { movies } = this.state;
    
    return (
      <div className={movies ? 'App' : 'App--loading'}>
        {movies ? this._renderMovies() : 'Loading'}
      </div>
    );
  }
}

export default App;
```

<br>

- Movie.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import LinesEllipsis from 'react-lines-ellipsis';
import './Movie.css';

function Movie({ title, poster, genres, synopsis }) {
  return (
    <div className="Movie">
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
        <div className="Movie__Synopsis">
          <LinesEllipsis
            text={synopsis}
            maxLine="3"
            ellipsis="..."
            trimRight
            basedOn="letters"
          />
        </div>
      </div>
    </div>
  );
}

function MoviePoster({ poster, alt }) {
  return <img src={poster} alt={alt} title={alt} className="Movie__Poster" />;
}

function MovieGenre({ genre }) {
  return <span className="Movie__Genre">{genre}</span>;
}

Movie.propTypes = {
  title: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired,
  genres: PropTypes.array.isRequired,
  synopsis: PropTypes.string.isRequired
};

MoviePoster.propTypes = {
  poster: PropTypes.string.isRequired,
  alt: PropTypes.string.isRequired
};

MovieGenre.propTypes = {
  genre: PropTypes.string.isRequired
};

export default Movie;
```

------

<br>

- index.css

```css
body {
  background-color: #eff3f7;
  height: 100%;
  padding: 0;
  margin: 0;
  font-family: 'Ubuntu', sans-serif;
}

html,
#root {
  height: 100%;
}
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

.App--loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
```

<br>

- Movie.css

```css
.Movie {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-start;
  background-color: #ffffff;
  width: 40%;
  padding: 0 20px;
  margin-bottom: 50px;
  text-overflow: ellipsis;
  box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3),
    0 5px 12px rgba(133, 133, 133, 0.22);
}

.Movie__Column {
  box-sizing: border-box;
  width: 30%;
  text-overflow: ellipsis;
}

.Movie__Column:last-child {
  width: 60%;
  padding: 20px 0;
}

.Movie h1 {
  font-size: 20px;
  font-weight: 600;
}

.Movie .Movie__Genres {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.Movie__Genres .Movie__Genre {
  color: #b4b5bd;
  margin-right: 10px;
}

.Movie .Movie__Synopsis {
  color: #b4b5bd;
  overflow: hidden;
  text-overflow: ellipsis;
}

.Movie .Movie__Poster {
  position: relative;
  max-width: 100%;
  top: -20px;
  box-shadow: -10px 19px 38px rgba(83, 83, 83, 0.3),
    10px 15px 12px rgba(80, 80, 80, 0.22);
}

@media screen and (min-width: 320px) and (max-width: 667px) {
  .Movie {
    width: 100%;
  }
}

@media screen and (min-width: 320px) and (max-width: 667px) and (orientation: portrait) {
  .Movie {
    flex-direction: column;
    width: 100%;
  }
  
  .Movie__Poster {
    width: 100%;
    top: 0;
    left: 0;
  }
  
  .Movie__Column {
    width: 100% !important;
  }
}
```

<br>

> `map()` 메소드
>
> 배열 내 모든 element에 대해, 호출한 함수의 결과를 모아 새로운 배열을 반환한다.

<br>