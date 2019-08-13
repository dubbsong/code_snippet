###### 컴포넌트 생성: `Message`

```bash
$ cd src
$ cd Components
$ touch Message.js
```

<br>

###### 코드 작성

- Message.js

```react
import React from 'react';
import styled from 'styled-components';
import PropTypes from 'prop-types';

const Container = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120px;
`;

const Text = styled.h4`
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

###### Import Message

- MoviePresenter.js

```react
...
import Message from 'Components/Message';

const MoviePresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <React.Fragment>
      ...
      {error && <Message text={error} />}
      <Footer />
    </React.Fragment>
  );

...
```

- TVPresenter.js

```react
...
import Message from 'Components/Message';

const TVPresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <React.Fragment>
      ...
      {error && <Message text={error} />}
      <Footer />
    </React.Fragment>
  );

...
```

- SearchPresenter.js

```react
...
import Message from 'Components/Message';

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
        {error && <Message text={error} />}
      </React.Fragment>
    )}
  </Container>
);

...
```

<br>

###### Error Test

- MovieContainer.js

```react
// Logic
...

throw Error();

...
```

> `Can't find movie information.`이 표시된다.
>
> `throw Error()` 제거

- TVContainer.js

```react
// Logic
...

throw Error();

...
```

> `Can't find tv information.`이 표시된다.
>
> `throw Error()` 제거

- SearchContainer.js

```react
// Logic
...

throw Error();

...
```

> `begins`를 입력하면, `Can't find results.`가 표시된다.
>
> `throw Error()` 제거

<br>

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

> `asdf;213`과 같이 존재하지 않는 것을 검색하면, `Nothing found`가 표시된다.

<br>

<br>

###### color props 전달

- Message.js

```react
...

const Text = styled.h4`
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
{error && <Message text={error} color="#e50914" />}
{movieResults && movieResults.length === 0 && tvResults && tvResults.length === 0 && (
  <Message text="Nothing found" color="#e5e5e5" />
)}
```

<br>

<br>