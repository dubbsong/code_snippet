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
      <h1>Ssup bro?</h1>
    );
  }
}

export default Movie;
```

<br>