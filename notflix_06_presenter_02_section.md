###### 컴포넌트 생성: `Section`

```bash
$ cd src
$ cd Components
$ touch Section.js
```

<br>

- Section.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div``;

const Title = styled.h4``;

const Grid = styled.div``;

const Section = ({ title, children }) => (
  <Container>
    <Title>{title}</Title>
    <Grid>{children}</Grid>
  </Container>
);

Section.propTypes = {
  title: PropTypes.string.isRequired,
  cihldren: PropTypes.oneOfType([
    PropTypes.arrayOf(PropTypes.node),
    PropTypes.node
  ])
};

export default Section;
```

<br>

###### props 전달: `MoviePresenter`

```react
...
import Section from '../../Components/Section';

const Container = styled.div`
  padding: 20px;
`;

const MoviePresenter = ({ nowPlaying, loading, error }) =>
  loading ? null : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
    </Container>
  );

...
```

> `Now Playing` Section title과 `nowPlaying` movie list가 표시된다.

<br>

###### CSS 추가

- Section.js

```react
...

const Container = styled.div`
  :not(:last-child) {
    margin-bottom: 50px;
  }
`;

const Title = styled.h4`
  font-size: 20px;
  font-weight: 600;
`;

const Grid = styled.div`
  margin-top: 25px;
  display: grid;
  grid-template-columns: repeat(auto-fill, 125px);
  grid-gap: 25px;
`;

...
```

<br>

###### props 전달: `TVPresenter`

```react
...
import Section from '../../Components/Section';

const Container = styled.div`
  padding: 20px;
`;

const TVPresenter = ({ topRated, loading, error }) =>
  loading ? null : (
    <Container>
      <Section title="Popular Shows">
        {topRated.map(tv => (
          <span key={tv.id}>{tv.name}</span>
        ))}
      </Section>
    </Container>
  );

...
```

> `Top Rated Shows` Section title과 `topRated` movie list가 표시된다.

<br>

<br>

###### 현재 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   ├─ GlobalStyle.js
  │   └─ Section.js
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