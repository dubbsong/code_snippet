- App.js

```react
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie />
        <Movie />
        <Movie />
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
    return (
      <div>
        <MoviePoster />
        <h1>Ssup bro?</h1>
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