#### prop-types 설치

```bash
$ yarn add prop-types
```

<br>

#### prop-types 작성

- MovieCard.js

```react
...
import PropTypes from 'prop-types';

...

MovieCard.propTypes = {
  poster: PropTypes.string.isRequired,
  title: PropTypes.string.isRequired
};

MoviePoster.propTypes = {
  poster: PropTypes.string.isRequired
};

...
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Set PropTypes'
$ git push origin master
```

<br>

<br>