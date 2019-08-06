###### 컴포넌트 생성: `Section`

```bash
$ cd src
$ cd Components
$ touch Section.js
```

<br>

###### 코드 작성

- Section.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Title = styled.h4`
  font-size: 16px;
  text-shadow: 2px 2px 5px #141414;
`;

const Carousel = styled.div`
  display: flex;
  overflow-x: auto;
  overflow-y: hidden;
`;

const Section = ({ title, children }) => (
  <React.Fragment>
    <Title>{title}</Title>
    <Carousel>{children}</Carousel>
  </React.Fragment>
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

###### props 전달

- MoviePresenter.js

```react
import React from 'react';
import HeaderMovie from 'Components/HeaderMovie';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Poster from 'Components/Poster';

const Container = styled.div`
  padding: 0 4%;
`;

const MoviePresenter = ({ loading, nowPlaying, popular, error }) =>
  loading ? null : (
    <React.Fragment>
      <HeaderMovie />
      <Container>
        {nowPlaying && nowPlaying.length > 0 && (
          <Section title="Now Playing">
            {nowPlaying.map(movie => (
              <Poster
                id={movie.id}
                imageUrl={movie.poster_path}
                isMovie={true}
                key={movie.id}
              />
            ))}
          </Section>
        )}
        {popular && popular.length > 0 && (
          <Section title="Popular">
            {popular.map(movie => (
              <Poster
                id={movie.id}
                imageUrl={movie.poster_path}
                isMovie={true}
                key={movie.id}
              />
            ))}
          </Section>
        )}
      </Container>
    </React.Fragment>
  );

MoviePresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  nowPlaying: PropTypes.array,
  popular: PropTypes.array,
  error: PropTypes.string
};

export default MoviePresenter;
```

<br>

###### 컴포넌트 생성: `Poster.js`

```bash
$ cd src
$ cd Components
$ touch Poster.js
```

<br>

###### 코드 작성

- Poster.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Wrapper = styled.div`
  white-space: nowrap;
  width: 250px;
  height: 140px;
`;

const ImageContainer = styled.div`
  display: inline-block;
`;

const Image = styled.div`
  background-image: url(${props => props.bgUrl});
  background-size: cover;
  background-position: center center;
  width: 250px;
  height: 140px;
`;

const Poster = ({ id, imageUrl, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <Wrapper>
      <ImageContainer>
        <Image bgUrl={`https://image.tmdb.org/t/p/w300${imageUrl}`} />
      </ImageContainer>
    </Wrapper>
  </Link>
);

Poster.propTypes = {
  id: PropTypes.number.isRequired,
  imageUrl: PropTypes.string,
  isMovie: PropTypes.bool
};

export default Poster;
```

<br>

<br>