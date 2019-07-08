#### 함수형 컴포넌트 (stateless)

- MovieCard.js

```react
import React from 'react';
...

function MovieCard({ poster, title }) {
  return (
    <div className="Movie__Card">
      <MoviePoster poster={poster} />
      <h2>{title}</h2>
    </div>
  );
}

function MoviePoster({ poster }) {
  return <img src={poster} alt="" />;
}

...
```

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Component
- [x] Set Props
- [x] Set Maping
- [x] Set PropTypes
- [x] Test Lifecycle
- [x] Set State
- [x] Set Stateless Component
- [] AJAX Networking
- [] Update Component
- [] Styling CSS
- [] Refactoring
- [] Deploying
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Set Stateless Component'
$ git push origin master
```

<br>

<br>