#### 파일 생성:  `Message`

- error & not found

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
  width: 100vw;
  display: flex;
  justify-content: center;
`;

const Text = styled.span`
  color: #e74c3c;
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

#### Error Test

1. MovieContainer.js

```react
...

export default class extends React.Component {
  ...

  async componentDidMount() {
    try {
      ...

      const {
        data: { results: upcoming }
      } = await movieApi.upcoming();

      throw Error();	// 테스트 후 제거

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

<br>

2. MoviePresenter.js

```react
...
import Message from 'Components/Message';

...

const MoviePresenter = ({ ... }) =>
  ...
  ) : (
    <Container>
      ...
      {upcoming && upcoming.length > 0 && (
        ...
      )}
      {error && <Message text={error} />}
    </Container>
  );

...
```

> Movies 탭에 `Can't find movie information.`이 표시된다.
>
> `throw Error();`를 제거한다.

<br>

#### Error Test

- TVContainer.js

```react
...

export default class extends React.Component {
  ...

  componentDidMount = async () => {
    try {
      ...
      
      const {
        data: { results: airingToday }
      } = await tvApi.airingToday();

      throw Error();	// 테스트 후 제거

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

<br>

- TVPresenter.js

```react
...
import Message from 'Components/Message';

...

const TVPresenter = ({ ... }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      ...
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          ...
        </Section>
      )}
      {error && <Message text={error} />}
    </Container>
  );

...
```

> TV 탭에 `Can't find tv information.`이 표시된다.
>
> `throw Error();`를 제거한다.

<br>

#### Error Test

1. SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  searchByTerm = async () => {
    ...

    try {
      throw Error();	// 테스트 후 제거

      ...
    } catch {
      ...
    } finally {
      ...
    }
  };

  ...
}

```

<br>

2. SearchPresenter.js

```react
...
import Message from 'Components/Message';

...

const SearchPresenter = ({...}) => (
  <Container>
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

> Search 탭에서 검색을 하면, `Can't find tv results.`가 표시된다.
>
> `throw Error();`를 제거한다.

<br>

#### 코드 수정 (color props 추가)

- Message.js

```react
...

const Text = styled.span`
  color: ${props => props.color};
`;

const Message = ({ text, color }) => (
  <Container>
    <Text color={color}>{text}</Text>
  </Container>
);

Message.propTypes = {
  text: PropTypes.string.isRequired,
  color: PropTypes.string.isRequired
};

...
```

<br>

- MoviePresenter.js

```react
...
{error && <Message text={error} color="#e74c3c" />}
...
```

<br>

- TVPresenter.js

```react
...
{error && <Message text={error} color="#e74c3c" />}
...
```

<br>

- SearchPresenter.js

```react
...

const SearchPresenter = ({...}) => (
  <Container>
    ...
    ) : (
      <React.Fragment>
        ...
        
        {error && <Message text={error} color="#e74c3c" />}
        {movieResults &&
          tvResults &&
          movieResults.length === 0 &&
          tvResults.length === 0 && (
            <Message text="Nothing found" color="#95a5a6" />
          )}
      </React.Fragment>
    )}
  </Container>
);

...
```

> Search 탭에서 `ahsdfals`와 같이 없는 것을 검색하면, `Nothing found`가 표시된다.

<br>

<br>