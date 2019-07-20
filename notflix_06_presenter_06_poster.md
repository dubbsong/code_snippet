#### 파일 생성: `Poster`

```bash
$ cd src
$ cd Components
$ touch Poster.js
```

<br>

- Poster.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div``;

const ImageContainer = styled.div``;

const Image = styled.div``;

const Rating = styled.span``;

const Title = styled.h4``;

const Year = styled.p``;

const Poster = ({ id, imageUrl, rating, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <Container>
      <ImageContainer>
        <Image bgUrl={imageUrl} />
        <Rating>
          <span role="img" aria-label="rating">
            ⭐️
          </span>{' '}
          {rating}/10
        </Rating>
      </ImageContainer>
      <Title>{title}</Title>
      <Year>{year}</Year>
    </Container>
  </Link>
);

Poster.propTypes = {
  id: PropTypes.number.isRequired,
  imageUrl: PropTypes.string,
  rating: PropTypes.number,
  title: PropTypes.string.isRequired,
  year: PropTypes.string,
  isMovie: PropTypes.bool
};

export default Poster;
```

<br>

#### Import Poster

- MoviePresenter.js

```react
...
import Poster from 'Components/Poster';

...

const MoviePresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <Poster />
          ))}
        </Section>
      )}
      ...
    </Container>
  );

...
```

> `⭐️ /10`이 화면에 표시된다.

> 1. 콘솔 `Network` 탭
> 2. `now_playing?api_key=…` 우클릭 
> 3. `Open in new tab` 클릭
> 4. JSON 확인

<br>

#### 코드 추가 (props 전달)

- MoviePresenter.js

```react
...

const MoviePresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <Poster
              id={movie.id}
              imageUrl={movie.poster_path}
              rating={movie.vote_average}
              title={movie.original_title}
              year={movie.release_date.substring(0, 4)}
              isMovie={true}
              key={movie.id}
            />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => (
            <Poster
              id={movie.id}
              imageUrl={movie.poster_path}
              rating={movie.vote_average}
              title={movie.original_title}
              year={movie.release_date.substring(0, 4)}
              isMovie={true}
              key={movie.id}
            />
          ))}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => (
            <Poster
              id={movie.id}
              imageUrl={movie.poster_path}
              rating={movie.vote_average}
              title={movie.original_title}
              year={movie.release_date.substring(0, 4)}
              isMovie={true}
              key={movie.id}
            />
          ))}
        </Section>
      )}
      ...
    </Container>
  );

...
```

> `⭐️ rating/10`, `title`, `year`가 화면에 표시된다.
>
> 아무거나 클릭하면, url에 정보가 표시된다.

<br>

- TVPresenter.js

```react
...
import Poster from 'Components/Poster';

...

const TVPresenter = ({...}) =>
  loading ? (
    ...
  ) : (
    <Container>
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated Shows">
          {topRated.map(tv => (
            <Poster
              id={tv.id}
              imageUrl={tv.poster_path}
              rating={tv.vote_average}
              title={tv.original_name}
              year={tv.first_air_date.substring(0, 4)}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Shows">
          {popular.map(tv => (
            <Poster
              id={tv.id}
              imageUrl={tv.poster_path}
              rating={tv.vote_average}
              title={tv.original_name}
              year={tv.first_air_date.substring(0, 4)}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          {airingToday.map(tv => (
            <Poster
              id={tv.id}
              imageUrl={tv.poster_path}
              rating={tv.vote_average}
              title={tv.original_name}
              year={tv.first_air_date.substring(0, 4)}
              key={tv.id}
            />
          ))}
        </Section>
      )}
      ...
    </Container>
  );

...
```

> `⭐️ rating/10`, `title`, `year`가 화면에 표시된다.
>
> 아무거나 클릭하면, url에 정보가 표시된다.

<br>

- SearchPresenter.js

```react
...
import Poster from 'Components/Poster';

...

const SearchPresenter = ({...}) => (
  <Container>
    ...
    {loading ? (
      ...
    ) : (
      <React.Fragment>
        {movieResults && movieResults.length > 0 && (
          <Section title="Movie Results">
            {movieResults.map(movie => (
              <Poster
                id={movie.id}
                imageUrl={movie.poster_path}
                rating={movie.vote_average}
                title={movie.original_title}
                year={movie.release_date.substring(0, 4)}
                isMovie={true}
                key={movie.id}
              />
            ))}
          </Section>
        )}
        {tvResults && tvResults.length > 0 && (
          <Section title="TV Show Results">
            {tvResults.map(tv => (
              <Poster
                id={tv.id}
                imageUrl={tv.poster_path}
                rating={tv.vote_average}
                title={tv.original_name}
                year={tv.first_air_date.substring(0, 4)}
                key={tv.id}
              />
            ))}
          </Section>
        )}
        ...
      </React.Fragment>
    )}
  </Container>
);

...
```

> `code`를 입력하면, `Movie Results`와 `TV Show Results`의 `⭐️ rating/10`, `title`, `year`가 화면에 표시된다.
>
> 아무거나 클릭하면, url에 정보가 표시된다.

<br>

<br>

#### For example:

```js
const date = '2019-07-05';
date.substring(0, 4);	// '2019'
```

<br>

#### For example: better than before

> `year={movie.release_date.substring(0, 4)}`보다 `year={movie.release_date && movie.release_date.substring(0, 4)}`가 안전하다.

<br>

<br>

#### 이미지 추가: `noPoster.png`

```bash
assets
  └─ img
      ├─ logo.png
      └─ noPoster.png
```

> 이미지가 없는 포스터를 `noPoster.png` 파일로 대체한다.

<br>

#### noPoster 설정

- Poster.js

```react
...

const Container = styled.div`
  font-size: 12px;
`;

const Image = styled.div`
  background-image: url(${props => props.bgUrl});
  background-size: cover;
  background-position: center center;
  height: 180px;
  border-radius: 4px;
  transition: opacity 0.2s linear;
`;

const Rating = styled.span`
  position: absolute;
  right: 5px;
  bottom: 5px;
  opacity: 0;
  transition: opacity 0.2s linear;
`;

const ImageContainer = styled.div`
  position: relative;
  margin-bottom: 5px;
  &:hover {
    ${Image} {
      opacity: 0.3;
    }
    ${Rating} {
      opacity: 1;
    }
  }
`;

const Title = styled.h4`
  margin-bottom: 3px;
`;

const Year = styled.p`
  font-size: 10px;
  color: rgba(255, 255, 255, 0.5);
`;

const Poster = ({...}) => (
  <Link to={...}>
    <Container>
      <ImageContainer>
        <Image
          bgUrl={
            imageUrl
              ? `https://image.tmdb.org/t/p/w300${imageUrl}`
              : require('../assets/img/noPoster.png')
          }
        />
        ...
      </ImageContainer>
      ...
    </Container>
  </Link>
);

...
```

> 1. [The Movie Database API](https://developers.themoviedb.org/3/getting-started/introduction)로 이동
> 2. `GETTING STARTED` 클릭
> 3. `Images` 클릭
> 4. `poster_path` 확인
>    - `https://image.tmdb.org/t/p/w500/….jpg`
>    - `…/w300/….jpg`로 너비 조정이 가능하다.
>    - `height` CSS를 설정해야 이미지가 표시된다.

> `const ImageContainer = styled.div…`를 `Image`와 `Rating` 아래로 이동시킨다.

> 화면에 포스터가 표시된다.

<br>

#### title 길이 단축

- Poster.js

```react
...

const Poster = ({...}) => (
  <Link to={...}>
    ...
      <Title>
        {title.length > 18 ? `${title.substring(0, 18)}...` : title}
      </Title>
      ...
  </Link>
);

...
```

> `John Wick: Chapter…`로 줄여서 표시된다.

<br>

<br>

#### 코드 추가 (DetailPresenter.js)

1. 이미지를 클릭해서 detail로 이동
2. 콘솔의 `Network` 탭으로 이동
3. `121?api_key=…` 클릭
4. bg img를 의미하는 `backdrop_path`를 확인할 수 있다.
   - 또는 [The Movie Database](https://www.themoviedb.org/)에서도 확인할 수 있다.

```react
...
import Loader from 'Components/Loader';

const Container = styled.div`
  position: relative;
  width: 100%;
  height: calc(100vh - 50px);
  padding: 50px;
`;

const Backdrop = styled.div`
  position: absolute;
  background-image: url(${props => props.bgImage});
  background-position: center center;
  background-size: cover;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  filter: blur(3px);
  opacity: 0.5;
  z-index: 0;
`;

const Content = styled.div`
  display: flex;
  position: relative;
  width: 100%;
  height: 100%;
  z-index: 1;
`;

const Cover = styled.div`
  background-image: url(${props => props.bgImage});
  background-position: center center;
  background-size: cover;
  width: 30%;
  height: 100%;
  border-radius: 5px;
`;

const Data = styled.div`
  width: 70%;
  margin-left: 10px;
`;

const Title = styled.h3`
  font-size: 32px;
`;

const ItemContainer = styled.div`
  margin: 20px 0;
`;

const Item = styled.span``;

const Divider = styled.span`
  margin: 0 10px;
`;

const Overview = styled.p`
  width: 50%;
  font-size: 12px;
  line-height: 1.5;
  opacity: 0.7;
`;

const DetailPresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      <Backdrop
        bgImage={`https://image.tmdb.org/t/p/original${result.backdrop_path}`}
      />
      <Content>
        <Cover
          bgImage={
            result.poster_path
              ? `https://image.tmdb.org/t/p/original${result.poster_path}`
              : require('../../assets/img/noPoster.png')
          }
        />
        <Data>
          <Title>
            {result.original_title
              ? result.original_title
              : result.original_name}
          </Title>
          <ItemContainer>
            <Item>
              {result.release_date
                ? result.release_date.substring(0, 4)
                : result.first_air_date.substring(0, 4)}
            </Item>
            <Divider>•</Divider>
            <Item>
              {result.runtime 
                ? result.runtime 
              	: result.episode_run_time[0]} min
            </Item>
            <Divider>•</Divider>
            <Item>
              {result.genres &&
                result.genres.map((genre, index) =>
                  index === result.genres.length - 1
                    ? genre.name
                    : `${genre.name} / `
                )}
            </Item>
          </ItemContainer>
          <Overview>
            {result.overview}
          </Overview>
        </Data>
      </Content>
    </Container>
  );

...
```

> \* CSS 짚어볼 필요가 있다.

<br>

<br>