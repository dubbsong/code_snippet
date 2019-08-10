###### 코드 추가

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
  margin: 70px 0 50px 0;
  padding: 0 4%;
`;

const Form = styled.form``;

const Input = styled.input`
  all: unset;
  width: 150px;
  font-size: 20px;
  border-bottom: 2px solid #b3b3b3;
`;

const SearchPresenter = ({
  loading,
  searchWord,
  movieResults,
  tvResults,
  error,
  handleSubmit
}) => (
  <Container>
    <Form>
      <Input value={searchWord} placeholder="Search By Word..." />
    </Form>
  </Container>
);

...
```

> `Enter`를 누르면 `refresh` 된다.
>
> 아직 입력이 되지 않는다.

<br>

###### 이벤트 취소

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

> `Enter`를 눌러도 `refresh` 되지 않는다.

<br>

###### 함수 생성: `updateWord`

1. SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  // Logic
  updateWord = event => {
    console.log(event);
  };

  searchByWord = async () => {
    ...
  };

  handleSubmit = event => {
    ...
  };

  render() {
    return (
      <SearchPresenter
        ...
        updateWord={this.updateWord}
      />
    );
  }
}
```

2. SearchPresenter.js

```react
...

const SearchPresenter = ({...}) => (
  <Container>
    <Form onSubmit={...}>
      <Input
        value={searchWord}
        placeholder="Search Movie or TV Show By Word..."
        onChange={updateWord}
      />
    </Form>
  </Container>
);

SearchPresenter.propTypes = {
  ...
  updateWord: PropTypes.func.isRequired
};

...
```

> `input`에 입력을 하면, `SyntheticEvent {...}`가 표시된다.

<br>

###### input 확인

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  // Logic
  updateWord = event => {
    // 1. 테스트 후 제거
    const { target } = event;
    console.log(target);

    // 2. 테스트 후 보존
    const {target: { value }} = event;
    console.log(value);	// 테스트 후 제거

    // 3. 코드 추가
    this.setState({
      searchWord: value
    });
  };

  searchByWord = async () => {
    ...
  };

  handleSubmit = event => {
    ...
  };

  ...
}
```

> 1. 개발자 도구 `Network` 탭으로 이동
> 2. `input`에 `begins` 입력 후 `Enter`
> 3. `movie?api_key=...` or `tv?api_key=...` 확인
>
> ``console.log(value);`` 제거

<br>

###### 검색 결과 출력

- SearchPresenter.js

```react
...
import Section from 'Components/Section';
import Poster from 'Components/Poster';
import Loader from 'Components/Loader';

...

const SearchPresenter = ({...}) => (
  <Container>
    <Form onSubmit={...}>
      ...
    </Form>
    {loading ? (
      <Loader />
    ) : (
      <React.Fragment>
        {movieResults && movieResults.length > 0 && (
          <Section title="Movie Results">
            {movieResults.map(movie => (
              <Poster
                id={movie.id}
                imageUrl={movie.poster_path}
                title={movie.title}
                year={movie.release_date}
                isMovie={true}
                key={movie.id}
              />
            ))}
          </Section>
        )}
        {tvResults && tvResults.length > 0 && (
          <Section title="TV Show Results">
            {tvResults.map(tv => (
              <Poster
                id={tv.id}
                imageUrl={tv.poster_path}
                title={tv.name}
                year={tv.first_air_date}
                key={tv.id}
              />
            ))}
          </Section>
        )}
      </React.Fragment>
    )}
  </Container>
);

...
```

<br>

<br>