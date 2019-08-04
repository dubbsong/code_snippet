###### prop-types 설치

```bash
$ yarn add prop-types
```

<br>

###### prop-types 설정

- MoviePresenter.js

```react
...
import PropTypes from 'prop-types';

const MoviePresenter = ({ loading, nowPlaying, popular, error }) => (
  <HeaderMovie />
);

MoviePresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  nowPlaying: PropTypes.array,
  popular: PropTypes.array,
  error: PropTypes.string
};

...
```

- TVPresenter.js

```react
...
import PropTypes from 'prop-types';

const TVPresenter = ({ loading, topRated, popular, error }) => (
  <HeaderTV />
);

TVPresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  topRated: PropTypes.array,
  popular: PropTypes.array,
  error: PropTypes.string
};

...
```

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';

const SearchPresenter = ({
  loading,
  movieResults,
  tvResults,
  searchWord,
  error,
  handleSubmit
}) => 'Search Input & Results Area';

SearchPresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  searchWord: PropTypes.string,
  error: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired
};

export default SearchPresenter;
```

- DetailPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';

const SearchPresenter = ({ loading, result, error }) => 'Each Detail Area';

SearchPresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  result: PropTypes.string,
  error: PropTypes.string
};

export default SearchPresenter;
```

<br>

<br>