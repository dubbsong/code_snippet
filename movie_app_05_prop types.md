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

class MovieCard extends Component {
  ...
}

MovieCard.propTypes = {
  title: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired
};

...
```

<br>

- MoviePoster.js

```react
...
import PropTypes from 'prop-types';

class MoviePoster extends Component {
  ...
}

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