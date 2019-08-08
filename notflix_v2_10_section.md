###### 컴포넌트 생성: `Section` / `Poster`

```bash
$ cd src
$ cd Components
$ touch Section.js
$ touch Poster.js
```

<br>

###### 이미지 추가: `logo_sm.png`

```bash
assets
  └─ img
      └─ logo_sm.png
```

<br>

###### 코드 작성

- Section.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
  padding: 0 4%;
  margin-bottom: 20px;
`;

const Title = styled.h4`
  font-size: 20px;
  text-shadow: 2px 2px 10px #000000;
`;

const Carousel = styled.div`
  display: flex;
  overflow-x: auto;
  overflow-y: hidden;
  padding: 20px 0;
  position: relative;

  &::-webkit-scrollbar {
    display: none;
  }
`;

const Section = ({ title, children }) => (
  <Container>
    <Title>{title}</Title>
    <Carousel>{children}</Carousel>
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

- GlobalStyle.js

```react
...

const globalStyle = createGlobalStyle`
  ...

  :root {
    --width: 250px;
    --height: calc(var(--width) / (16 / 9));
    --scale: 1.2;
  }
`;

...
```

- Poster.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import logo from 'assets/img/logo_sm.png';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import {
  faPlayCircle,
  faThumbsUp,
  faThumbsDown,
  faPlus
} from '@fortawesome/free-solid-svg-icons';

const Logo = styled.img`
  width: 20px;
  position: absolute;
  top: 8px;
  left: 3px;
`;

const Image = styled.div`
  background-image: url(${props => props.bgUrl});
  background-size: cover;
  background-position: top center;
  width: var(--width);
  height: var(--height);
`;

const HoverContent = styled.div`
  opacity: 0;

  @media (max-width: 768px) {
    opacity: 1;
  }
`;

const ImageContainer = styled.div`
  position: relative;
  padding: 0 2px;
  transition: 0.2s all;

  &:hover {
    transform: scale(var(--scale));
    margin: 0 25px;

    ${Image} {
      opacity: 0.4;
    }

    ${HoverContent} {
      opacity: 1;
    }
  }
`;

const LeftContent = styled.div`
  position: absolute;
  left: 10px;
  bottom: 10px;
`;

const Title = styled.h4`
  font-size: 14px;
  margin: 10px 0 5px 0;
  text-shadow: 5px 5px 10px #000000;
`;

const Year = styled.p`
  font-size: 10px;
`;

const RightContent = styled.div`
  position: absolute;
  right: 10px;
  bottom: 10px;
`;

const StyledIcon = styled(FontAwesomeIcon)`
  display: block;
  margin-top: 8px;
  font-size: 12px;
`;

const Poster = ({ id, imageUrl, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <ImageContainer>
      <Logo src={logo} alt="" />
      <Image bgUrl={`https://image.tmdb.org/t/p/w300${imageUrl}`} />
      <HoverContent>
        <LeftContent>
          <FontAwesomeIcon icon={faPlayCircle} size="2x" />
          <Title>
            {title.length > 30 ? `${title.substring(0, 30)}...` : title}
          </Title>
          <Year>{year.substring(0, 4)}</Year>
        </LeftContent>
        <RightContent>
          <StyledIcon icon={faThumbsUp} />
          <StyledIcon icon={faThumbsDown} />
          <StyledIcon icon={faPlus} />
        </RightContent>
      </HoverContent>
    </ImageContainer>
  </Link>
);

Poster.propTypes = {
  id: PropTypes.number.isRequired,
  imageUrl: PropTypes.string,
  title: PropTypes.string,
  year: PropTypes.string,
  isMovie: PropTypes.bool
};

export default Poster;
```

<br>

###### props 전달

- MoviePresenter.js

```react
import React from 'react';
import HeaderMovie from 'Components/HeaderMovie';
import PropTypes from 'prop-types';
import Section from 'Components/Section';
import Poster from 'Components/Poster';

const MoviePresenter = ({ loading, nowPlaying, topRated, error }) =>
  loading ? null : (
    <React.Fragment>
      <HeaderMovie />
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
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
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated">
          {topRated.map(movie => (
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
    </React.Fragment>
  );

MoviePresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  nowPlaying: PropTypes.array,
  topRated: PropTypes.array,
  error: PropTypes.string
};

export default MoviePresenter;
```

- TVPresenter.js

```react
import React from 'react';
import HeaderTV from 'Components/HeaderTV';
import PropTypes from 'prop-types';
import Section from 'Components/Section';
import Poster from 'Components/Poster';

const TVPresenter = ({ loading, topRated, popular, error }) =>
  loading ? null : (
    <React.Fragment>
      <HeaderTV />

      {topRated && topRated.length > 0 && (
        <Section title="Top Rated">
          {topRated.map(tv => (
            <Poster
              id={tv.id}
              imageUrl={tv.poster_path}
              title={tv.name}
              year={tv.first_air_date}
              isMovie={true}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular">
          {popular.map(tv => (
            <Poster
              id={tv.id}
              imageUrl={tv.poster_path}
              title={tv.name}
              year={tv.first_air_date}
              isMovie={true}
              key={tv.id}
            />
          ))}
        </Section>
      )}
    </React.Fragment>
  );

TVPresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  topRated: PropTypes.array,
  popular: PropTypes.array,
  error: PropTypes.string
};

export default TVPresenter;
```

<br>

<br>