###### 컴포넌트 생성: `Section` / `Poster`

```bash
$ cd src
$ cd Components
$ touch Section.js
$ touch Poster.js
```

<br>

###### 코드 작성

- Section.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

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
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faPlayCircle } from '@fortawesome/free-solid-svg-icons';
import { faThumbsUp } from '@fortawesome/free-solid-svg-icons';
import { faThumbsDown } from '@fortawesome/free-solid-svg-icons';
import { faPlus } from '@fortawesome/free-solid-svg-icons';

const Image = styled.div`
  background-image: url(${props => props.bgUrl});
  background-size: cover;
  background-position: top center;
  width: var(--width);
  height: var(--height);
`;

const Content = styled.div`
  opacity: 0;
`;

const ImageContainer = styled.div`
  padding: 0 2px;
  transition: 0.2s all;

  &:hover {
    transform: scale(var(--scale));
    margin: 0 25px;

    ${Image} {
      opacity: 0.4;
    }

    ${Content} {
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
  margin: 5px 0;
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
`;

const Poster = ({ id, imageUrl, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <ImageContainer>
      <Image bgUrl={`https://image.tmdb.org/t/p/w300${imageUrl}`} />
      <Content>
        <LeftContent>
          <FontAwesomeIcon icon={faPlayCircle} />
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
      </Content>
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
import styled from 'styled-components';
import Section from 'Components/Section';
import Poster from 'Components/Poster';

const Container = styled.div`
  padding: 0 4%;
`;

const MoviePresenter = ({ loading, nowPlaying, topRated, error }) =>
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
      </Container>
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
import styled from 'styled-components';
import Section from 'Components/Section';
import Poster from 'Components/Poster';

const Container = styled.div`
  padding: 0 4%;
`;

const TVPresenter = ({ loading, topRated, popular, error }) =>
  loading ? null : (
    <React.Fragment>
      <HeaderTV />
      <Container>
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
      </Container>
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