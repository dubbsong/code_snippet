###### input 설정

- SearchPresenter.js

```react
...

const Container = styled.div`
  padding: 20px 30px;

	@media only screen and (max-width: 576px) {
		padding: 20px;
	}
`;

const Form = styled.form`
  width: 100%;
  margin-bottom: 50px;
`;

const Input = styled.input`
  all: unset;
  width: 100%;
  font-size: 20px;
`;

const SearchPresenter = ({...}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input
        value={searchWord}
        placeholder="Search Movies or TV Shows"
      />
    </Form>
  </Container>
);

...
```

> `Enter`를 누르면 `refresh` 된다.
>
> 아직 입력이 되지 않는다.

<br>

###### 이벤트 취소: `preventDefault()`

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  // Logic
  handleSubmit = event => {
    event.preventDefault();

    ...
  };

  ...
}
```

> `Enter`를 눌러도 `refresh` 하지 않는다.

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

  ...

  render() {
    ...

    return (
      <SearchPresenter
        ...
        updateWord={this.updateWord}
      />
    );
  }
}
```

<br>

2. SearchPresenter.js

```react
...

const SearchPresenter = ({
  ...
  updateWord
}) => (
  <Container>
    <Form onSubmit={...}>
      <Input
        value={searchWord}
        onChange={updateWord}
        placeholder="Search Movies or TV Shows"
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

> `input`에 입력을 하면, `SyntheticEvent {…}`가 표시된다.

<br>

###### input 확인

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  updateWord = event => {
    // 1. Test (제거)
    const { target } = event;
    console.log(target);

    // 2. Test (보존)
    const {
      target: { value }
    } = event;
    console.log(value); // 확인 후 제거

    // 3 Test (보존)
    this.setState({
      searchWord: value
    });
  };

  ...
}
```

> `input`에 `batman`을 입력하고 `Enter`를 누르면, Network 탭에서 `movie`, `tv`의 `results`를 확인할 수 있다.
>
> `console.log(value);` 제거

<br>

###### 검색 기능 구현

- SearchPresenter.js

```react
...
import Section from '../../Components/Section';
import Loader from '../../Components/Loader';


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
              <p key={movie.id}>{movie.title}</p>
            ))}
          </Section>
        )}
        {tvResults && tvResults.length > 0 && (
          <Section title="TV Show Results">
            {tvResults.map(tv => (
              <p key={tv.id}>{tv.name}</p>
            ))}
          </Section>
        )}
      </React.Fragment>
    )}
  </Container>
);

...
```

> `input`에 `batman`을 입력하고 `Enter`를 누르면, `Movie Results`, `TV Shows Results`가 표시된다.

<br>

<br>

###### 현재 디렉토리 구조 (변화 없음)

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   ├─ GlobalStyle.js
  │   ├─ Section.js
  │   └─ Loader.js
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