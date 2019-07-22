###### 컴포넌트 생성: `Message`

```bash
$ cd src
$ cd Components
$ touch Message.js
```

<br>

- Message.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100vh;
  margin-top: 80px;
`;

const Text = styled.span`
  font-size: 20px;
  color: #e50914;
`;

const Message = ({ text }) => (
  <Container>
    <Text>{text}</Text>
  </Container>
);

Message.propTypes = {
  text: PropTypes.string.isRequired
};

export default Message;
```

<br>

###### Error: `Can't find movie information.`

1. MovieContainer.js

```react
...

export default class extends React.Component {
  ...

  // Logic
  async componentDidMount() {
    try {
      ...

      throw Error(); // 테스트 후 제거

      this.setState({
        ...
      });
    } catch {
      ...
    } finally {
      ...
    }
  }

  ...
}
```

2. MoviePresenter.js

```react
...
import Message from '../../Components/Message';

...

const MoviePresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <Container>
      ...
      {error && <Message text={error} />}
    </Container>
  );

...
```

> Nav `Movies` 탭에 `Can't find movie information.`이 표시된다.
>
> `throw Error()`를 제거한다.

<br>

###### Error: `Can't find tv information.`

1. TVContainer.js

```react
...

export default class extends React.Component {
  ...

  // Logic
  componentDidMount = async () => {
    try {
      ...

      throw Error(); // 테스트 후 제거

      this.setState({
        ...
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  ...
}
```

2. TVPresenter.js

```react
...
import Message from '../../Components/Message';

...

const TVPresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <Container>
      ...
      {error && <Message text={error} />}
    </Container>
  );

...
```

<br>

###### Error: `Can't find results.`

1. SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  // Logic
  searchByTerm = async () => {
    ...

    try {
      ...

      throw Error(); // 테스트 후 제거

      this.setState({
        ...
      });
    } catch {
      ...
    } finally {
      ...
    }
  };

  ...
}
```

2. SearchPresenter.js

```react

```

> Nav `TV Shows` 탭에 `Can't find results`가 표시된다.
>
> `throw Error()`를 제거한다.

<br>

###### No result: `Nothing found`

- SearchPresenter.js

```react
...

const SearchPresenter = ({...}) => (
  <Container>
    <Form onSubmit={...}>
      ...
    </Form>
    {loading ? (
      ...
    ) : (
      <React.Fragment>
        ...
        {movieResults &&
          movieResults.length === 0 &&
          tvResults &&
          tvResults.length === 0 && <Message text="Nothing found" />}
      </React.Fragment>
    )}
  </Container>
);

...
```

> Nav `Search` 탭에서 `dhaksgqo`와 같이 존재하지 않는 것을 검색하면, `Nothing found`가 표시된다.

<br>

###### color props 전달: `Can't find`,  `Noting found`

- Message.js

```react
...

const Text = styled.span`
  ...
  color: ${props => props.color};
`;

const Message = ({ text, color }) => (
  <Container>
    <Text color={color}>{text}</Text>
  </Container>
);

Message.propTypes = {
  ...
  color: PropTypes.string.isRequired
};

...
```

- MoviePresenter.js

```react
{error && <Message text={error} color="#e50914" />}
```

- TVPresenter.js

```react
{error && <Message text={error} color="#e50914" />}
```

- SearchPresenter.js

```react
{error && <Message text={error} color="#e50914"}
{movieResults && movieResults.length === 0 && tvResults && tvResults.length === 0 && (
  <Message text="Nothing found" color="e5e5e5" />
)}
```

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
  │   ├─ Loader.js
  │   └─ Message.js
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