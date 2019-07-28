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

...

const MoviePresenter = ({...}) => (
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

> Nav `Movies`를 클릭하면, 브라우저 탭에 `Movies | NOTFLIX`가 표시된다.

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

> Nav `TV Shows`를 클릭하면, 브라우저 탭에 `TV | NOTFLIX`가 표시된다.

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
    ...
    {loading ? (
      ...
    ) : (
      ...
    )}
  </Container>
);

...
```

> Nav `🔍`를 클릭하면, 브라우저 탭에 `Search | NOTFLIX`가 표시된다.

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

> 각 이미지를 클릭하면, 브라우저 탭에 `각 해당 Detail | NOTFLIX`가 표시된다.

<br>

<br>