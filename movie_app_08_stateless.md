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

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Modify Functional Components'
$ git push origin master
```

<br>

<br>