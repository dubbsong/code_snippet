#### 함수형 컴포넌트

- MoviePoster.js

```react
import React from 'react';
...

function MoviePoster({ poster }) {
  return <img src={poster} alt="" />;
}

...
```

<br>

- MovieCard.js

```react
import React from 'react';
...

function MovieCard({ title, poster }) {
  return (
    <div>
      <MoviePoster poster={poster} />
      <h2>{title}</h2>
    </div>
  );
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