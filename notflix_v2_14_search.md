###### Search 설정

- SearchPresenter.js

```react
...
import styled from 'styled-components';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faSearch } from '@fortawesome/free-solid-svg-icons';

const Container = styled.div``;

const Form = styled.form``;

const StyledIcon = styled(FontAwesomeIcon)``;

const Input = styled.input``;

const SearchPresenter = ({...}) => (
  <Container>
    <Form>
      <StyledIcon />
      <Input placeholder="Search by word..." />
    </Form>
  </Container>
);

...
```

<br>

###### Style 설정

- SearchPresenter.js

```react
...

const Container = styled.div``;

const Form = styled.form`
  padding: 80px 4% 0;
  margin-bottom: 60px;
  display: flex;
  align-items: center;
`;

const StyledIcon = styled(FontAwesomeIcon)`
  font-size: 16px;
`;

const Input = styled.input`
  all: unset;
  width: 100%;
  font-size: 20px;
  margin-left: 8px;
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
    <Form onSubmit={handleSubmit}>
      <StyledIcon icon={faSearch} />
      <Input placeholder="Search by word..." value={searchWord} />
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

  handleSubmit = event => {
    ...
  };

  searchByWord = async () => {
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

const SearchPresenter = ({
  ...
  updateWord
}) => (
  <Container>
    <Form onSubmit={...}>
      ...
      <Input
        placeholder="..."
        value={...}
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
import Loader from 'Components/Loader';
import Section from 'Components/Section';
import VPoster from 'Components/VPoster';

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
              <VPoster
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
              <VPoster
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

> `begins`를 입력하고 `Enter`를 누르면, 각 결과가 표시된다.

<br>

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set Search'
$ git push origin master
```

<br>

<br>