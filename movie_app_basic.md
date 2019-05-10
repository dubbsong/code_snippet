- Movie.js

```react
import React, { Component } from 'react';
import './Movie.css';

class Movie extends Component {
  render() {
    return <h2>오많배</h2>;
  }
}

export default Movie;
```

<br>

- App.js

```react
import React from 'react';
import './App.css';
import Movie from './Movie';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Movie />
      </div>
    );
  }
}

export default App;
```

<br>