- App.js

```react
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

const movies = [
  {
    title: "Batman Begins",
    poster: "https://dummyimage.com/100x150/ff7373/fff"
  },
  {
    title: "Batman Dark Knight",
    poster: "https://dummyimage.com/100x150/ffc952/fff"
  },
  {
    title: "Batman Rises",
    poster: "https://dummyimage.com/100x150/47b8e0/fff"
  }
]

class App extends Component {
  
  state = {
    greeting: 'Ssup bro?'
  }
  
  render() {
    return (
      <div className="App">
        {this.state.greeting}
        {movies.map((movie, index) => {
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

- Movie.js (변화 없음)

```react
import React, { Component } from 'react';
import PropTypes from 'prop-types';
import './Movie.css';

class Movie extends Component {
  
  static propTypes = {
    title: PropTypes.string.isRequired,
    poster: PropTypes.string.isRequired
  }
  
  render() {
    return (
      <div>
        <MoviePoster poster={this.props.poster} />
        <h1>{this.props.title}</h1>
      </div>
    );
  }
}

class MoviePoster extends Component {
  
  static propTypes = {
    poster: PropTypes.string.isRequired
  }
  
  render() {
    return (
      <img src={this.props.poster} alt="" />
    );
  }
}

export default Movie;
```

<br>