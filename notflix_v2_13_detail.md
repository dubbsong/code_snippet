###### 데이터 확인

1. 이미지 클릭 (detail page로 이동)
2. 개발자 도구 `Network` 탭으로 이동
3. `command` \+ `shift` \+ `R` (강제 새로고침)
4. `id?api_key=...` 클릭

<br>

###### 코드 작성

- DetailPresenter.js

```react
...
import styled from 'styled-components';
import Loader from 'Components/Loader';

const Container = styled.div`
  width: 100%;
  height: 100vh;
  padding: 70px 4% 50px;
  position: relative;

  @media (max-width: 768px) {
    padding: 0;
  }
`;

const Backdrop = styled.div`
  background-image: url(${props => props.bgImage});
  background-size: cover;
  background-position: center center;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  filter: blur(3px);
  opacity: 0.4;

  @media (max-width: 768px) {
    display: none;
  }
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
    width: 100%;
    filter: blur(2px);
    opacity: 0.5;
  }
`;

const RightContent = styled.div`
  width: 50%;
  padding-top: 50vh;
  margin-left: 40px;

  @media (max-width: 768px) {
    width: 100%;
    padding: 60% 10px 0;
    margin: 0;
    position: absolute;
    height: 100%;
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
  margin-bottom: 40px;
  text-shadow: 5px 5px 20px #141414;

  @media (max-width: 768px) {
    font-size: 16px;
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
              : require('../../assets/vertical_no_poster.png')
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