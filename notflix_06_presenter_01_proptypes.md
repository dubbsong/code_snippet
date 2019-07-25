###### prop-types 설치

```bash
$ yarn add prop-types
```

<br>

###### prop-types 설정

- MoviePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const MoviePresenter = ({ nowPlaying, loading, error }) => null;

MoviePresenter.propTypes = {
  nowPlaying: PropTypes.array,
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

const TVPresenter = ({ topRated, loading, error }) => null;

TVPresenter.propTypes = {
  topRated: PropTypes.array,
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
  searchWord,
  loading,
  error,
  handleSubmit
}) => null;

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  searchWord: PropTypes.string,
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

###### 현재 디렉토리 구조 (변화 없음)

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   └─ GlobalStyle.js
  ├─ Routes
  │   ├─ Movie
  │   │   ├─ index.js
  │   │   ├─ MovieContainer.js
  │   │   └─ MoviePresenter.js
  │   ├─ TV
  │   │   ├─ index.js
  │   │   ├─ TVContainer.js
  │   │   └─ TVPresenter.js
  │   ├─ Search
  │   │   ├─ index.js
  │   │   ├─ SearchContainer.js
  │   │   └─ SearchPresenter.js
  │   └─ Detail
  │       ├─ index.js
  │       ├─ DetailContainer.js
  │       └─ DetailPresenter.js
  ├─ assets
  │   └─ img
  │       └─ logo.png
  ├─ api.js
  └─ index.js
```

<br>

<br>