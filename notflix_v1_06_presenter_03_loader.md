###### 컴포넌트 생성: `Loader`

```bash
$ cd src
$ cd Components
$ touch Loader.js
```

<br>

- Loader.js

```react
import React from 'react';
import styled from 'styled-components';

const Container = styled.div`
  display: flex;
  justify-content: center;
  font-size: 20px;
  margin-top: 200px;
  width: 100%;
`;

export default () => (
  <Container>
    <p>Loading...</p>
  </Container>
);
```

<br>

###### Import Loader

- MoviePresenter.js

```react
...
import Loader from '../../Components/Loader';

...

const MoviePresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      ...
    </Container>
  );

...
```

- TVPresenter.js

```react
...
import Loader from '../../Components/Loader';

...

const TVPresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      ...
    </Container>
  );

...
```

> 데이터를 가져오기 전까지 `Loading…`을 표시한다.

<br>

<br>

###### 현재 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   ├─ GlobalStyle.js
  │   ├─ Section.js
  │   └─ Loader.js
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