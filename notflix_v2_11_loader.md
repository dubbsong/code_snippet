###### 컴포넌트 생성: `Loader`

```bash
$ cd src
$ cd Components
$ touch Loader.js
```

<br>

###### 코드 작성

- Loader.js

```react
import React from 'react';
import styled from 'styled-components';

const Container = styled.div`
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
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
import Loader from 'Components/Loader';

const MoviePresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    ...
  );

...
```

- TVPresenter.js

```react
...
import Loader from 'Components/Loader';

const TVPresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    ...
  );

...
```

<br>

<br>