###### react-helmet 설치

```bash
$ yarn add react-helmet
```

<br>

###### react-helmet 설정

- MoviePresenter.js

```react
...
import Helmet from 'react-helmet';

const MoviePresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <React.Fragment>
      <Helmet>
        <title>Movies | NOTFLIX</title>
      </Helmet>
      ...
    </React.Fragment>
  );

...
```

> `Movies`를 클릭하면, 브라우저 탭에 `Movies | NOTFLIX`가 표시된다.

<br>

- TVPresenter.js

```react
...
import Helmet from 'react-helmet';

const TVPresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <React.Fragment>
      <Helmet>
        <title>TV | NOTFLIX</title>
      </Helmet>
      ...
    </React.Fragment>
  );

...
```

> `TV Shows`를 클릭하면, 브라우저 탭에 `TV | NOTFLIX`가 표시된다.

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
    <Form onSubmit={...}>
      ...
    </Form>
    ...
  </Container>
);

...
```

> `🔍`를 클릭하면, 브라우저 탭에 `Search | NOTFLIX`가 표시된다.

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
          {detailResult.title ? detailResult.title : detailResult.name} |
          NOTFLIX
        </title>
      </Helmet>
      ...
    </Container>
  );

...
```

> 각 detail로 이동하면, 브라우저 탭에 `해당 detail | NOTFLIX`가 표시된다.

<br>

<br>