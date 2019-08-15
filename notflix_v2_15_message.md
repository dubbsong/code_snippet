###### 컴포넌트 생성: `Message`

```bash
$ cd src
$ cd Components
$ touch Message.js
```

<br>

###### Message 설정

- Message.js

```react
import React from 'react';
import styled from 'styled-components';
import PropTypes from 'prop-types';

const Container = styled.div``;

const Text = styled.h4``;

const Message = ({ text, color }) => (
  <Container>
    <Text color={color}>{text}</Text>
  </Container>
);

Message.propTypes = {
  text: PropTypes.string.isRequired,
  color: PropTypes.string.isRequired
};

export default Message;
```

<br>

###### Style 설정

- Message.js

```react
...

const Container = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120px;
`;

const Text = styled.h4`
  font-size: 20px;
  color: ${props => props.color};
`;

...
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
      {error && <Message text={error} color="#e50914" />}
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
      {error && <Message text={error} color="#e50914" />}
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
        {error && <Message text={error} color="#e50914" />}
        {movieResults &&
          movieResults.length === 0 &&
          tvResults &&
          tvResults.length === 0 && (
            <Message text="Nothing found" color="#e5e5e5" />
          )}
      </React.Fragment>
    )}
  </Container>
);

...
```

<br>

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set Message'
$ git push origin master
```

<br>

<br>