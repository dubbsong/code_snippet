###### 데이터 확인

1. 이미지 클릭 (detail page로 이동)
2. 개발자 도구 `Network` 탭으로 이동
3. `command` \+ `shift` \+ `R` (강제 새로고침)
4. `id?api_key=...` 클릭

<br>

###### Detail 설정

- DetailPresenter.js

```react
...
import styled from 'styled-components';
import Loader from 'Components/Loader';

const Container = styled.div``;

const Backdrop = styled.div``;

const Content = styled.div``;

const LeftContent = styled.div``;

const RightContent = styled.div``;

const Title = styled.h2``;

const ItemContainer = styled.div``;

const Item = styled.span``;

const Divider = styled.span``;

const Overview = styled.p``;

const DetailPresenter = ({ loading, result, error }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      <Backdrop />
      <Content>
        <LeftContent />
        <RightContent>
          <Title>title</Title>
          <ItemContainer>
            <Item>2019</Item>
            <Divider>•</Divider>
            <Item>112 min</Item>
            <Divider>•</Divider>
            <Item>Action • Comedy</Item>
            <Divider>•</Divider>
          </ItemContainer>
          <Overview>Lorem Ipsum...</Overview>
        </RightContent>
      </Content>
    </Container>
  );

...
```

<br>

###### Style 설정

- DetailPresenter.js

```react
...

const Container = styled.div`
  width: 100%;
  height: 100vh;
  padding: 70px 4% 50px;
  position: relative;
`;

const Backdrop = styled.div`
  background-image: url(${props => props.bgImage});
  background-size: cover;
  background-position: center center;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0%;
  filter: blur(3px);
  opacity: 0.8;
`;

const Content = styled.div`
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
`;

const LeftContent = styled.div`
  background-image: url(${props => props.bgImage});
  background-size: cover;
  background-position: center center;
  width: 35%;
  height: 100%;
  border-radius: 5px;
  box-shadow: 5px 5px 20px #141414;

  @media (max-width: 768px) {
    display: none;
  }
`;

const RightContent = styled.div`
  width: 50%;
  padding-top: 50vh;
  margin-left: 40px;

  @media (max-width: 768px) {
    width: 100%;
    position: absolute;
    bottom: 0;
    margin-left: 8px;
  }
`;

const Title = styled.h2`
  font-size: 40px;
  font-weight: 700;
  text-shadow: 5px 5px 20px #141414;
  margin-bottom: 8px;

  @media (max-width: 768px) {
    font-size: 24px;
  }
`;

const ItemContainer = styled.div`
  font-size: 16px;
  margin-bottom: 20px;
`;

const Item = styled.span`
  text-shadow: 5px 5px 20px #141414;
`;

const Divider = styled.span`
  margin: 0 8px;
`;

const Overview = styled.p`
  font-size: 20px;
  line-height: 1.4;
  color: #e6e6e6;
  text-shadow: 5px 5px 20px #141414;

  @media (max-width: 768px) {
    font-size: 18px;
  }
`;

const DetailPresenter = ({ loading, result, error }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      <Backdrop
        bgImage={`https://image.tmdb.org/t/p/original${result.backdrop_path}`}
      />
      <Content>
        <LeftContent
          bgImage={
            result.poster_path
              ? `https://image.tmdb.org/t/p/original${result.poster_path}`
              : require('../../assets/no_v_poster.png')
          }
        />
        <RightContent>
          <Title>{result.title ? result.title : result.name}</Title>
          <ItemContainer>
            <Item>
              {result.release_date
                ? result.release_date.substring(0, 4)
                : result.first_air_date.substring(0, 4)}
            </Item>
            <Divider>•</Divider>
            <Item>
              {result.runtime ? result.runtime : result.episode_run_time}
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
            {result.overview.length > 450
              ? `${result.overview.substring(0, 450)}...`
              : result.overview}
          </Overview>
        </RightContent>
      </Content>
    </Container>
  );

...
```

<br>

<br>