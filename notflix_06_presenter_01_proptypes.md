#### prop-types 설치

```bash
$ yarn add prop-types
```

<br>

#### PropTypes 설정

- MoviePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const MoviePresenter = ({ nowPlaying, popular, upcoming, loading, error }) =>
  null;

MoviePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  popular: PropTypes.array,
  upcoming: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
};

export default MoviePresenter;
```

- TVPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
  null;

TVPresenter.propTypes = {
  topRated: PropTypes.array,
  popular: PropTypes.array,
  airingToday: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
};

export default TVPresenter;
```

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const SearchPresenter = ({
  movieResults,
  tvResults,
  searchTerm,
  loading,
  error,
  handleSubmit
}) => null;

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  searchTerm: PropTypes.string,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired
};

export default SearchPresenter;
```

- DetailPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const DetailPresenter = ({ result, loading, error }) => null;

DetailPresenter.propTypes = {
  result: PropTypes.object,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
};

export default DetailPresenter;
```

> 4가지 에러가 발생하지만, 나중에 수정한다.

<br>

<br>