#### react-helmet 설치

```bash
$ yarn add react-helmet
```

<br>

#### 코드 추가

- HomePresenter.js

```react
...
import Helmet from 'react-helmet';

...

const HomePresenter = ({...}) => (
  <React.Fragment>
    <Helmet>
      <title>Movies | NOTFLIX</title>
    </Helmet>
    {loading ? (
      ...
    ) : (
      ...
    )}
  </React.Fragment>
);

...
```

> Movies 탭을 클릭하면, `Movies | NOTFLIX`가 표시된다.

<br>

- TVPresenter.js

```react
...
import Helmet from 'react-helmet';

...

const TVPresenter = ({...}) => (
  <React.Fragment>
    <Helmet>
      <title>TV | NOTFLIX</title>
    </Helmet>
    {loading ? (
      ...
    ) : (
      ...
    )}
  </React.Fragment>
);

...
```

> TV 탭을 클릭하면, `TV | NOTFLIX`가 표시된다.

<br>

- SearchPresenter.js

```react
...
import Helmet from 'react-helmet';

...

const SearchPresenter = ({...}) => (
  <Container>
    <Helmet>
      <title>Search | NOTFLIX</title>
    </Helmet>
    <Form onSubmit={handleSubmit}>
      ...
    </Form>
    {loading ? (
      ...
    ) : (
      ...
    )}
  </Container>
);

...
```

> Search 탭을 클릭하면, `Search | NOTFLIX`가 표시된다.

<br>

- DetailPresenter.js

```react
...
import Helmet from 'react-helmet';

...

const DetailPresenter = ({...}) =>
  loading ? (
    <React.Fragment>
      <Helmet>
        <title>Loading | NOTFLIX</title>
      </Helmet>
      <Loader />
    </React.Fragment>
  ) : (
    <Container>
      <Helmet>
        <title>
          {result.original_title 
            ? result.original_title 
          	: result.original_name}{' '}| NOTFLIX
        </title>
      </Helmet>
      ...
    </Container>
  );

...
```

> 이미지를 클릭하면, `해당 Detail | NOTFLIX`가 표시된다.

<br>

<br>