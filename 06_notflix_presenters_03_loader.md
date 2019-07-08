#### 파일 생성

```bash
$ cd src
$ cd Components
$ touch Loader.js
```

<br>

#### 코드 작성 (Loader.js)

```react
import React from 'react';
import styled from 'styled-components';

const Container = styled.div`
  display: flex;
  justify-content: center;
  font-size: 32px;
  width: 100vw;
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

#### 코드 추가 (import Loader)

- HomePresenter.js

```react
...
import Loader from 'Components/Loader';

...

const HomePresenter = ({ nowPlaying, popular, upcoming, loading, error }) =>
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

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
  loading ? (
    <Loader />
  ) : (
    ...
  );

...
```

> 이전보다 빨리 로딩되고, 로딩 화면을 확인할 수 있다. (⏰)

<br>

#### 코드 수정 (span 삽입)

- HomePresenter.js

```react
...

const HomePresenter = ({ nowPlaying, popular, upcoming, loading, error }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
    </Container>
  );

...
```

<br>

- TVPresenter.js

```react
...

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated Shows">
          {topRated.map(tv => (
            <span key={tv.id}>{tv.name}</span>
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Shows">
          {popular.map(tv => (
            <span key={tv.id}>{tv.name}</span>
          ))}
        </Section>
      )}
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          {airingToday.map(tv => (
            <span key={tv.id}>{tv.name}</span>
          ))}
        </Section>
      )}
    </Container>
  );

...
```

<br>

#### 코드 추가 (input 생성 및 설정)

- SearchPresenter.js

```react
...

const Container = styled.div`
  padding: 20px;
`;

const Form = styled.form`
  width: 100%;
  margin-bottom: 50px;
`;

const Input = styled.input`
  all: unset;
  width: 100%;
  font-size: 28px;
`;

const SearchPresenter = ({
  movieResults,
  tvResults,
  searchTerm,
  loading,
  error,
  handleSubmit
}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input placeholder="Search Movies or Tv Shows..." value={searchTerm} />
    </Form>
  </Container>
);

...
```

> 아직 입력이 되지 않는다.
>
> 엔터를 누르면 새로고침이 동작한다.

<br>

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  handleSubmit = event => {
    event.preventDefault();

    ...
  };

  ...
}
```

<br>

#### 함수 생성 및 연결 (updateTerm)

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  updateTerm = event => {
    console.log(event);
  };

  ...

  render() {
    ...

    return (
      <SearchPresenter
        ...
        handleSubmit={this.handleSubmit}
        updateTerm={this.updateTerm}
      />
    );
  }
}

```

<br>

- SearchPresenter.js

```react
...

const SearchPresenter = ({
  ...
  handleSubmit,
  updateTerm
}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input
        placeholder="Search Movies or Tv Shows..."
        value={searchTerm}
        onChange={updateTerm}
      />
    </Form>
  </Container>
);

SearchPresenter.propTypes = {
  ...
  handleSubmit: PropTypes.func.isRequired,
  updateTerm: PropTypes.func.isRequired
};

...
```

> input에 입력을 하면, 콘솔에 SyntheticEvent가 표시된다.

<br>

#### 코드 수정 (test)

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  updateTerm = event => {
		// 1. 입력 테스트 (제거)
    const { target } = event;
    console.log(target);

		// 2. 입력 테스트 (제거 x)
		const {
      target: { value }
    } = event;
		console.log(value);

		// 3. 입력 테스트 (제거 x)
		this.setState({
      searchTerm: value
    });
  };

  ...
}
```

> 각 과정에 따라 input에 입력을 하고, 변화를 살펴본다.
>
> 테스트 후, `console.log(value);`를 제거한다.
>
> 이제 검색을 하면 Network에서 확인할 수 있다.

<br>

#### 코드 추가 (검색 결과 작동)

- SearchPresenter.js

```react
...
import Section from 'Components/Section';
import Loader from 'Components/Loader';

...

const SearchPresenter = ({...}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      ...
    </Form>
    {loading ? (
      <Loader />
    ) : (
      <React.Fragment>
        {movieResults && movieResults.length > 0 && (
          <Section title="Movie Results">
            {movieResults.map(movie => (
              <span key={movie.id}>{movie.title}</span>
            ))}
          </Section>
        )}
        {tvResults && tvResults.length > 0 && (
          <Section title="TV Show Results">
            {tvResults.map(tv => (
              <span key={tv.id}>{tv.name}</span>
            ))}
          </Section>
        )}
      </React.Fragment>
    )}
  </Container>
);

...
```

> 검색 후, 결과 데이터가 잘 표시된다.

<br>

<br>