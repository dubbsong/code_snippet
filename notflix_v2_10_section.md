###### 컴포넌트 생성: `Section` / `Poster`

```bash
$ cd src
$ cd Components
$ touch Section.js
$ touch HPoster.js
$ touch VPoster.js
```

<br>

###### 이미지 추가

```bash
assets
  ├─ logo_sm.png
  ├─ horizontal_no_poster.png
  └─ vertical_no_poster.png
```

<br>

###### 코드 작성

- Section.js

```react
import React from 'react';
import styled from 'styled-components';
import PropTypes from 'prop-types';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faArrowsAltH } from '@fortawesome/free-solid-svg-icons';

const Top = styled.div`
  display: flex;
  justify-content: space-between;
`;

const Title = styled.h4`
  font-size: 20px;
  text-shadow: 5px 5px 20px #000000;
`;

const StyledIcon = styled(FontAwesomeIcon)`
  font-size: 20px;
  text-shadow: 5px 5px 20px #000000;
  opacity: 0;
`;

const Container = styled.div`
  padding: 0 4%;
  margin-bottom: 20px;

  &:hover {
    ${StyledIcon} {
      opacity: 1;
    }
  }
`;

const Bottom = styled.div`
  display: flex;
  overflow-x: auto;
  padding: 20px 0;
  position: relative;

  &::-webkit-scrollbar {
    display: none;
  }
`;

const Section = ({ title, children }) => (
  <Container>
    <Top>
      <Title>{title}</Title>
      <StyledIcon icon={faArrowsAltH} />
    </Top>
    <Bottom>{children}</Bottom>
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
    --horizontal_width: 250px;
    --horizontal_height: calc(var(--horizontal_width) / (16 / 9));
    --horizontal_scale: 1.2;
    --vertical_width: 180px;
    --vertical_height: calc(var(--vertical_width) / (2 / 3));
    --vertical_scale: 1.1;
  }
`;

...
```

- HPoster.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';
import PropTypes from 'prop-types';
import logo from 'assets/logo_sm.png';
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
  width: var(--horizontal_width);
  height: var(--horizontal_height);
`;

const HoverContent = styled.div`
  opacity: 0;

  @media (max-width: 576px) {
    opacity: 1;
  }
`;

const ImageContainer = styled.div`
  position: relative;
  padding: 0 2px;
  transition: 0.2s all;

  &:hover {
    transform: scale(var(--horizontal_scale));
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

const StyledIconLeft = styled(FontAwesomeIcon)`
  font-size: 20px;
`;

const Title = styled.h4`
  font-size: 14px;
  margin: 10px 0 5px;
  text-shadow: 5px 5px 20px #141414;
`;

const Year = styled.p`
  font-size: 10px;
`;

const RightContent = styled.div`
  position: absolute;
  right: 10px;
  bottom: 10px;
`;

const StyledIconRight = styled(FontAwesomeIcon)`
  display: block;
  margin-top: 8px;
  font-size: 12px;
`;

const HPoster = ({ id, imageUrl, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <ImageContainer>
      <Logo src={logo} alt="" />
      <Image
        bgUrl={
          imageUrl
            ? `https://image.tmdb.org/t/p/w300${imageUrl}`
            : require('../assets/horizontal_no_poster.png')
        }
      />
      <HoverContent>
        <LeftContent>
          <StyledIconLeft icon={faPlayCircle} />
          <Title>
            {title.length > 30 ? `${title.substring(0, 30)}...` : title}
          </Title>
          <Year>{year.substring(0, 4)}</Year>
        </LeftContent>
        <RightContent>
          <StyledIconRight icon={faThumbsUp} />
          <StyledIconRight icon={faThumbsDown} />
          <StyledIconRight icon={faPlus} />
        </RightContent>
      </HoverContent>
    </ImageContainer>
  </Link>
);

HPoster.propTypes = {
  id: PropTypes.number.isRequired,
  imageUrl: PropTypes.string,
  title: PropTypes.string,
  year: PropTypes.string,
  isMovie: PropTypes.bool
};

export default HPoster;
```

- VPoster.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';
import PropTypes from 'prop-types';
import logo from 'assets/logo_sm.png';
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
  width: var(--vertical_width);
  height: var(--vertical_height);
`;

const HoverContent = styled.div`
  opacity: 0;

  @media (max-width: 576px) {
    opacity: 1;
  }
`;

const ImageContainer = styled.div`
  position: relative;
  padding: 0 2px;
  transition: 0.2s all;

  &:hover {
    transform: scale(var(--vertical_scale));
    margin: 0 10px;

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

const StyledIconLeft = styled(FontAwesomeIcon)`
  font-size: 20px;
`;

const Title = styled.h4`
  font-size: 14px;
  margin: 10px 0 5px;
  text-shadow: 5px 5px 20px #141414;
`;

const Year = styled.p`
  font-size: 10px;
`;

const RightContent = styled.div`
  position: absolute;
  right: 10px;
  bottom: 10px;
`;

const StyledIconRight = styled(FontAwesomeIcon)`
  display: block;
  margin-top: 8px;
  font-size: 12px;
`;

const HPoster = ({ id, imageUrl, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <ImageContainer>
      <Logo src={logo} alt="" />
      <Image
        bgUrl={
          imageUrl
            ? `https://image.tmdb.org/t/p/w300${imageUrl}`
            : require('../assets/vertical_no_poster.png')
        }
      />
      <HoverContent>
        <LeftContent>
          <StyledIconLeft icon={faPlayCircle} />
          <Title>
            {title.length > 30 ? `${title.substring(0, 30)}...` : title}
          </Title>
          <Year>{year.substring(0, 4)}</Year>
        </LeftContent>
        <RightContent>
          <StyledIconRight icon={faThumbsUp} />
          <StyledIconRight icon={faThumbsDown} />
          <StyledIconRight icon={faPlus} />
        </RightContent>
      </HoverContent>
    </ImageContainer>
  </Link>
);

HPoster.propTypes = {
  id: PropTypes.number.isRequired,
  imageUrl: PropTypes.string,
  title: PropTypes.string,
  year: PropTypes.string,
  isMovie: PropTypes.bool
};

export default HPoster;
```

<br>

###### Import

- MoviePresenter.js

```react
import React from 'react';
import MovieHeader from 'Components/MovieHeader';
import PropTypes from 'prop-types';
import Section from 'Components/Section';
import HPoster from 'Components/HPoster';

const MoviePresenter = ({
  loading,
  trending,
  nowPlaying,
  topRated,
  upcoming,
  error
}) =>
  loading ? null : (
    <React.Fragment>
      <MovieHeader />
      {trending && trending.length > 0 && (
        <Section title="Trending Movies">
          {trending.map(movie => (
            <HPoster
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
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <HPoster
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
            <HPoster
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
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming">
          {upcoming.map(movie => (
            <HPoster
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
  trending: PropTypes.array,
  nowPlaying: PropTypes.array,
  topRated: PropTypes.array,
  upcoming: PropTypes.array,
  error: PropTypes.string
};

export default MoviePresenter;
```

- TVPresenter.js

```react
import React from 'react';
import TVHeader from 'Components/TVHeader';
import PropTypes from 'prop-types';
import Section from 'Components/Section';
import HPoster from 'Components/HPoster';

const TVPresenter = ({
  loading,
  trending,
  onTheAir,
  popular,
  topRated,
  error
}) =>
  loading ? null : (
    <React.Fragment>
      <TVHeader />
      {trending && trending.length > 0 && (
        <Section title="Trending TV Shows">
          {trending.map(tv => (
            <HPoster
              id={tv.id}
              imageUrl={tv.poster_path}
              title={tv.name}
              year={tv.first_air_date}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      {onTheAir && onTheAir.length > 0 && (
        <Section title="On The Air">
          {onTheAir.map(tv => (
            <HPoster
              id={tv.id}
              imageUrl={tv.poster_path}
              title={tv.name}
              year={tv.first_air_date}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular">
          {popular.map(tv => (
            <HPoster
              id={tv.id}
              imageUrl={tv.poster_path}
              title={tv.name}
              year={tv.first_air_date}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated">
          {topRated.map(tv => (
            <HPoster
              id={tv.id}
              imageUrl={tv.poster_path}
              title={tv.name}
              year={tv.first_air_date}
              key={tv.id}
            />
          ))}
        </Section>
      )}
    </React.Fragment>
  );

TVPresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  trending: PropTypes.array,
  onTheAir: PropTypes.array,
  popular: PropTypes.array,
  topRated: PropTypes.array,
  error: PropTypes.string
};

export default TVPresenter;
```

<br><br>