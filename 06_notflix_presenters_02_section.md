#### 파일 생성

```bash
$ src
$ Components
$ touch Section.js
```

<br>

#### 코드 작성 (Section.js)

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div``;

const Title = styled.span``;

const Grid = styled.div``;

const Section = ({ title, children }) => (
  <Container>
    <Title>{title}</Title>
    <Grid>{children}</Grid>
  </Container>
);

Section.propTypes = {
  title: PropTypes.string.isRequired,
  children: PropTypes.oneOfType([
    PropTypes.arrayOf(PropTypes.node),
    PropTypes.node
  ])
};

export default Section;
```

<br>

#### 코드 추가 (HomePresenter.js)

- nowPlaying 확인

```react
...
import Section from 'Components/Section';

const Container = styled.div`
  padding: 20px;
`;

const HomePresenter = ({ nowPlaying, popular, upcoming, loading, error }) =>
  loading ? null : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => movie.title)}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => movie.title)}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => movie.title)}
        </Section>
      )}
    </Container>
  );

...
```

> 화면에 제목과 영화 목록이 표시된다.

<br>

#### CSS 추가 (Section.js)

```react
...

const Container = styled.div`
  :not(:last-child) {
    margin-bottom: 50px;
  }
`;

const Title = styled.span`
  font-size: 14px;
  font-weight: 600;
`;

const Grid = styled.div`
  display: grid;
  grid-template-columns: repeat(auto-fill, 125px);
  grid-gap: 25px;
  margin-top: 25px;
`;

...
```

<br>

#### 코드 추가 (TVPresenter.js)

```react
...
import Section from 'Components/Section';

const Container = styled.div`
  padding: 20px;
`;

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
  loading ? null : (
    <Container>
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated Shows">
          {topRated.map(tv => tv.name)}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Shows">
          {popular.map(tv => tv.name)}
        </Section>
      )}
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          {airingToday.map(tv => tv.name)}
        </Section>
      )}
    </Container>
  );

...
```

> 화면에 제목과 영화 목록이 표시된다.
>
> 탭을 클릭했을 때, 비어있다가 데이터가 표시된다.

<br>

<br>