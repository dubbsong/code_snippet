###### 컴포넌트 생성: `Section` / `Poster`

```bash
$ cd src
$ cd components
$ touch Section.js
$ touch HPoster.js
$ touch VPoster.js
```

<br>

###### 이미지 추가

```bash
assets
  ├─ logo_sm.png
  ├─ no_h_poster.png
  └─ no_v_poster.png
```

<br>

###### Section 설정

- Section.js

```react
import React from 'react';
import styled from 'styled-components';
import PropTypes from 'prop-types';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faArrowsAltH } from '@fortawesome/free-solid-svg-icons';

const Container = styled.div``;

const Top = styled.div``;

const Title = styled.h4``;

const StyledIcon = styled(FontAwesomeIcon)``;

const Bottom = styled.div``;

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

<br>

###### Style 설정

- Section.js

```react
...

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

  @media (max-width: 768px) {
		opacity: 1;
	}
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

...
```

<br>

###### CSS 변수 설정

- GlobalStyle.js

```react
...

const GlobalStyle = createGlobalStyle`
  ...

  :root {
    --h_width: 250px;
    --h_height: calc(var(--h_width) / (16 / 9));
    --h_scale: 1.2;
    --v_width: 180px;
    --v_height: calc(var(--v_width) / (2 / 3));
    --v_scale: 1.1;
  }
`;

...
```

<br>

###### HPoster 설정

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

const ImageContainer = styled.div``;

const Logo = styled.img``;

const Image = styled.div``;

const HoverContent = styled.div``;

const LeftContent = styled.div``;

const StyledIconLeft = styled(FontAwesomeIcon)``;

const Title = styled.h4``;

const Year = styled.p``;

const RightContent = styled.div``;

const StyledIconRight = styled(FontAwesomeIcon)``;

const HPoster = ({ id, imageUrl, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <ImageContainer>
      <Logo />
      <Image />
      <HoverContent>
        <LeftContent>
          <StyledIconLeft />
          <Title>OMB</Title>
          <Year>2019</Year>
        </LeftContent>
        <RightContent>
          <StyledIconRight />
          <StyledIconRight />
          <StyledIconRight />
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

###### Style 설정

- HPoster.js

```react
...

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
  width: var(--h_width);
  height: var(--h_height);
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
    transform: scale(var(--h_scale));
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

	@media (max-width: 576px) {
		display: none;
	}
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
            : require('../assets/no_h_poster.png')
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

...
```

<br>

###### VPoster 설정

- VPoster.js
  1. CSS 변수 `--v_width`, `--v_height`, `--v_scale`로 변경
  2. `cont VPoster = ({...});`로 변경
  3. `VPoster.propTypes = {...};`로 변경
  4. `export default VPoster;`로 변경

<br>

<br>

###### Import

- MoviePresenter.js

```react
...
import Section from 'components/Section';
import HPoster from 'components/HPoster';

const MoviePresenter = ({...}) =>
  loading ? (
    ...
  ) : (
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

...
```

- TVPresenter.js

```react
...
import Section from 'components/Section';
import HPoster from 'components/HPoster';

const TVPresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <React.Fragment>
      <TVHeder />
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

...
```

<br><br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set Section and Poster'
$ git push origin master
```

<br>

<br>