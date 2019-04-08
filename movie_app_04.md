- App.js

```react
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

const movieTitles = [
  "Batman Begins",
  "Batman Dark Knight",
  "Batman Rises"
]

const movieImages = [
  "https://dummyimage.com/100x150/ff7373/fff",
  "https://dummyimage.com/100x150/ffc952/fff",
  "https://dummyimage.com/100x150/47b8e0/fff"
]

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie title={movieTitles[0]} poster={movieImages[0]} />
        <Movie title={movieTitles[1]} poster={movieImages[1]} />
        <Movie title={movieTitles[2]} poster={movieImages[2]} />
      </div>
    );
  }
}

export default App;
```

<br>

- Movie.js

```react
import React, { Component } from 'react';
import './Movie.css';

class Movie extends Component {
  render() {
    console.log(this.props);
    
    return (
      <div>
        <MoviePoster poster={this.props.poster} />
        <h1>{this.props.title}</h1>
      </div>
    );
  }
}

class MoviePoster extends Component {
  render() {
    return (
      <img src={this.props.poster} alt="" />
    );
  }
}

export default Movie;
```

<br>