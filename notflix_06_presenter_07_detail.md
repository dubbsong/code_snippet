###### Detail 설정

1. 이미지 클릭
2. 개발자 도구 `Network` 탭으로 이동
3. `command` \+ `shift` \+ `R` (강제 새로고침)
4. `id?api_key=…` 클릭
5. `배경 이미지`를 나타내는 `backdrop_path` 확인

<br>

- DetailPresenter.js

```react
...
import Loader from '../../Components/Loader';

const Container = styled.div`
  position: relative;
  width: 100%;
  height: calc(100vh - 70px);
  padding: 40px;
  display: flex;
`;

const Backdrop = styled.div`
  position: absolute;
  background-image: url(${props => props.bgImage});
  background-size: cover;
  background-position: center center;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  filter: blur(3px);
  z-index: 0;
  opacity: 0.5;
`;

const LeftColumn = styled.div`
  position: relative;
  width: 30%;
  z-index: 1;

  @media only screen and (max-width: 768px) {
    display: none;
  }
`;

const CoverImage = styled.div`
  background-image: url(${props => props.bgImage});
  background-size: cover;
  background-position: center center;
  width: 100%;
  height: 100%;
  box-shadow: 5px 2px 20px rgba(0, 0, 0, 0.8);
`;

const RightColumn = styled.div`
  position: relative;
  width: 70%;
  z-index: 1;
  margin-left: 40px;

  @media only screen and (max-width: 768px) {
    width: 100%;
    margin-left: 0;
  }
`;

const Title = styled.div`
  font-size: 32px;
  margin-top: 50vh;
  text-shadow: 5px 2px 20px rgba(0, 0, 0, 0.8);

  @media only screen and (max-width: 768px) {
    margin-top: 0;
  }
`;

const ItemContainer = styled.div`
  margin: 20px 0;
`;

const Item = styled.span`
  font-size: 14px;
  line-height: 1.5;

  @media only screen and (max-width: 768px) {
    display: block;
    text-align: right;
  }
`;

const Divider = styled.span`
  margin: 0 10px;

  @media only screen and (max-width: 768px) {
    display: none;
  }
`;

const Overview = styled.p`
  font-size: 16px;
  line-height: 1.5;
  opacity: 0.8;
  width: 80%;

  @media only screen and (max-width: 768px) {
    width: 100%;
    text-align: justify;
    line-height: 1.3;
    margin-top: 30px;
  }
`;

const DetailPresenter = ({ result, loading, error }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      <Backdrop
        bgImage={`https://image.tmdb.org/t/p/original${result.backdrop_path}`}
      />
      <LeftColumn>
        <CoverImage
          bgImage={
            result.poster_path
              ? `https://image.tmdb.org/t/p/original${result.poster_path}`
              : require('../../assets/img/noPoster.png')
          }
        />
      </LeftColumn>
      <RightColumn>
        <Title>
          {result.original_title ? result.original_title : result.original_name}
        </Title>
        <ItemContainer>
          <Item>
            {result.release_date
              ? result.release_date.substring(0, 4)
              : result.first_air_date.substring(0, 4)}
          </Item>
          <Divider>•</Divider>
          <Item>
            {result.runtime ? result.runtime : result.episode_run_time} min
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
          <Divider>•</Divider>
          <Item>
            <span role="img" aria-label="rating">
              ⭐️
            </span>{' '}
            {result.vote_average}/10
          </Item>
        </ItemContainer>
        <Overview>{result.overview}</Overview>
      </RightColumn>
    </Container>
  );

...
```

<br>

<br>

###### 현재 디렉토리 구조 (변화 없음)

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