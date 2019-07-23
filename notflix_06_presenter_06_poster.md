###### 컴포넌트 생성: `Poster`

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

const Image = styled.div`
  background-color: #20a19c;
  height: 180px;
`;

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

###### Import Poster

- MoviePresenter.js

```react
...
import Poster from '../../Components/Poster';

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
      ...
    </Container>
  );

...
```

> `이미지`, `평점`, `제목`, `개봉 날짜`가 표시된다.
>
> 이미지를 클릭하면, url에 id가 표시된다.

<br>

- TVPresenter.js

```react
...
import Poster from '../../Components/Poster';

...

const TVPresenter = ({ topRated, loading, error }) =>
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
      ...
    </Container>
  );

...
```

> `이미지`, `평점`, ` 제목`, `개봉 날짜`가 표시된다.
>
> 이미지를 클릭하면, url에 id가 표시된다.

<br>

- SearchPresenter.js

```react
...
import Poster from '../../Components/Poster';

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

> `batman`을 입력하면, `이미지`, `평점`, ` 제목`, `개봉 날짜`가 표시된다.
>
> 이미지를 클릭하면, url에 id가 표시된다.

<br>

<br>

###### 이미지 설정

1. [TMDB API](https://developers.themoviedb.org/3/getting-started/introduction)로 이동
2. `GETTING STARTED`의 `Images` 클릭
3. `poster_path` url 확인
   - `https://image.tmdb.org/t/p/w500/….jpg`
   - `…`에는 `imageUrl` props가 위치하면 된다.

<br>

- Poster.js

```react
...

const Image = styled.div`
  background-image: url(${props => props.bgUrl});
  background-size: cover;
  height: 180px;
`;

...

const Poster = ({...}) => (
  <Link to={...}>
    <Container>
      <ImageContainer>
        <Image bgUrl={`https://image.tmdb.org/t/p/w300${imageUrl}`} />
        ...
      </ImageContainer>
      ...
    </Container>
  </Link>
);

...
```

> 각각의 해당 이미지가 표시된다.

<br>

###### CSS 설정

- Poster.js

```react
...

const Container = styled.div`
  font-size: 14px;
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
      opacity: 0.4;
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
  color: rgba(255, 255, 255, 0.5);
`;

...
```

> `ImageContainer`를 `Rating` 아래로 이동시킨다.

<br>

###### 이미지 추가: `noPoster.png`

```bash
assets
  └─ img
      ├─ logo.png
      └─ noPoster.png
```

> 이미지 정보가 없는 것은, `noPoster.png` 이미지로 대체한다.

<br>

- Poster.js

```react
import React from 'react';
import { Link } from 'react-router-dom';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
  font-size: 14px;
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
      opacity: 0.4;
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
  color: rgba(255, 255, 255, 0.5);
`;

const Poster = ({ id, imageUrl, rating, title, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <Container>
      <ImageContainer>
        <Image
          bgUrl={
            imageUrl
              ? `https://image.tmdb.org/t/p/w300${imageUrl}`
              : require('../assets/img/noPoster.png')
          }
        />
        <Rating>
          <span role="img" aria-label="rating">
            ⭐️
          </span>{' '}
          {rating}/10
        </Rating>
      </ImageContainer>
      ...
    </Container>
  </Link>
);

...
```

<br>

###### title 길이 단축

- Poster.js

```react
...

const Poster = ({...}) => (
  <Link to={...}>
    <Container>
      <ImageContainer>
        ...
      </ImageContainer>
      <Title>
        {title.length > 15 ? `${title.substring(0, 15)}...` : title}
      </Title>
      <Year>{...}</Year>
    </Container>
  </Link>
);

...
```

<br>

###### Detail 설정

1. 이미지 클릭
2. 개발자 도구 `Network` 탭으로 이동
3. `command` \+ `shift` \+ `R` (강제 새로고침)
4. `id?api_key=…` 클릭
5. `배경 이미지`를 나타내는 `backdrop_path` 확인

<br>

- DetailPresenter.js

```react

```



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
  │   ├─ Section.js
  │   ├─ Loader.js
  │   ├─ Message.js
  │   └─ Poster.js
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