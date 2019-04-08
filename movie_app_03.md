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

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie title={movieTitles[0]} />
        <Movie title={movieTitles[1]} />
        <Movie title={movieTitles[2]} />
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
        <MoviePoster />
        <h1>{this.props.title}</h1>
      </div>
    );
  }
}

class MoviePoster extends Component {
  render() {
    return (
      <img src="https://dummyimage.com/100x150/20a19c/fff" alt="" />
    );
  }
}

export default Movie;
```

<br>