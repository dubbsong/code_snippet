- App.js

```react
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

class App extends Component {
  state = {
    movies: [
      {
        title: 'Batman Begins',
        poster: 'https://dummyimage.com/100x150/ff7373/fff'
      },
      {
        title: 'Batman Dark Knight',
        poster: 'https://dummyimage.com/100x150/ffc952/fff'
      },
      {
        title: 'Batman Rises',
        poster: 'https://dummyimage.com/100x150/47b8e0/fff'
      }
    ]
  };
  
  componentDidMount() {
    setTimeout(() => {
      this.setState({
        movies: [
          ...this.state.movies,
          {
            title: 'Iron Man',
            poster: 'https://dummyimage.com/100x150/31314c/fff'
          }
        ]
      });
    }, 2000);
  }
  
  render() {
    return (
      <div className="App">
        {this.state.movies.map((movie, index) => {
          return (
            <Movie title={movie.title} poster={movie.poster} key={index} />
          );
        })}
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
import './Movie.css';

function Movie({ title, poster }) {
  return (
    <div>
      <MoviePoster poster={poster} />
      <h2>{title}</h2>
    </div>
  );
}

function MoviePoster({ poster }) {
  return <img src={poster} alt="" />;
}

Movie.propTypes = {
  title: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired
};

MoviePoster.propTypes = {
  poster: PropTypes.string.isRequired
};

export default Movie;
```

<br>