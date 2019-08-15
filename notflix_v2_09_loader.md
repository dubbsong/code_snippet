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
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
`;

const Text = styled.p`
  font-size: 20px;
`;

export default () => (
  <Container>
    <Text>Loading...</Text>
  </Container>
);
```

<br>

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set Loader'
$ git push origin master
```

<br>

<br>