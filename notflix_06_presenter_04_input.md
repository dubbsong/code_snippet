#### input 생성 및 설정

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
  font-size: 20px;
`;

const SearchPresenter = ({...}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input value={searchTerm} placeholder="Search Movies or TV Shows" />
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

> 엔터를 눌러도 새로고침이 동작하지 않는다.

<br>

#### updateTerm 함수 생성 및 연결

- SearchContainer.js

```react
...

export default class extends React.Component {
  ...

  handleSubmit = event => {
    ...
  };

  updateTerm = event => {
    console.log(event);
  };

  ...

  render() {
    const {...} = this.state;

    return (
      <SearchPresenter
        ...
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
        ...
        onChange={updateTerm}
      />
    </Form>
  </Container>
);

SearchPresenter.propTypes = {
  ...
  updateTerm: PropTypes.func.isRequired
};

...
```

> input에 입력을 하면, Console 탭에 SyntheticEvent가 표시된다.

<br>

#### Test input

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
		console.log(value);	// 테스트 후 제거

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
> input에 `code`를 입력하고 엔터를 누르면, Network 탭에서 movie와 tv의 결과를 확인할 수 있다.

> `console.log(value);`를 제거한다.

<br>

#### 검색 구현

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

> input에 `code`를 입력하고 엔터를 누르면, 검색 결과가 화면에 표시된다.

<br>

<br>