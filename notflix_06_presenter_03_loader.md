#### 파일 생성: `Loader`

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
  font-size: 32px;
  width: 100%;
  height: 100vh;
  margin-top: 40px;
`;

export default () => (
  <Container>
    <span role="img" aria-label="Loading">
      ⏰
    </span>
  </Container>
);
```

<br>

#### import Loader

- MoviePresenter.js

```react
...
import Loader from 'Components/Loader';

...

const MoviePresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    ...
  );

...
```

<br>

- TVPresenter.js

```react
...
import Loader from 'Components/Loader';

...

const TVPresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    ...
  );

...
```

> Loading(⏰)을 확인할 수 있다.
>
> 이전보다 빨리 로딩된다.

<br>

<br>
