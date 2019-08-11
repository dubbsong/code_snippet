###### 데이터 확인

1. 이미지 클릭 (detail page로 이동)
2. 개발자 도구 `Network` 탭으로 이동
3. `command` \+ `shift` \+ `R` (강제 새로고침)
4. `id?api_key=...` 클릭

<br>

###### 이미지 추가: `no_poster.png`

```bash
assets
  └─ img
      └─ no_poster.png
```

<br>

###### 코드 작성

- DetailPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Loader from 'Components/Loader';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faPlay } from '@fortawesome/free-solid-svg-icons';
import { faPlus } from '@fortawesome/free-solid-svg-icons';

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
  padding-top: 80px;
  margin-left: 40px;

  @media (max-width: 768px) {
    width: 100%;
    padding: 80px 10px;
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
  margin-bottom: 40px;
  text-shadow: 5px 5px 20px #141414;

  @media (max-width: 768px) {
    font-size: 16px;
  }
`;

const ButtonContainer = styled.div`
  @media (max-width: 768px) {
    position: absolute;
    bottom: 20px;
  }
`;

const Button = styled.button`
  background-color: transparent;
  color: inherit;
  width: 120px;
  height: 40px;
  font-size: 16px;
  letter-spacing: 1.5px;
  border-width: 0;
  border-radius: 3px;
  margin-right: 5px;
  cursor: pointer;

  &:first-child {
    color: #e50914;
    border: 2px solid #e50914;
  }

  &:last-child {
    color: #ffffff;
    border: 2px solid #ffffff;
  }
`;

const DetailPresenter = ({ loading, detailResult, error }) =>
  loading ? (
    <Loader />
  ) : (
    <Container>
      <Backdrop
        bgImage={`https://image.tmdb.org/t/p/original${
          detailResult.backdrop_path
        }`}
      />
      <Content>
        <LeftContent
          bgImage={
            detailResult.poster_path
              ? `https://image.tmdb.org/t/p/original${detailResult.poster_path}`
              : require('../../assets/img/no_poster.png')
          }
        />
        <RightContent>
          <Title>
            {detailResult.title ? detailResult.title : detailResult.name}
          </Title>
          <ItemContainer>
            <Item>
              {detailResult.release_date
                ? detailResult.release_date.substring(0, 4)
                : detailResult.first_air_date.substring(0, 4)}
            </Item>
            <Divider>•</Divider>
            <Item>
              {detailResult.runtime
                ? detailResult.runtime
                : detailResult.episode_run_time}{' '}
              min
            </Item>
            <Divider>•</Divider>
            <Item>
              {detailResult.genres &&
                detailResult.genres.map((genre, index) =>
                  index === detailResult.genres.length - 1
                    ? genre.name
                    : `${genre.name} / `
                )}
            </Item>
          </ItemContainer>
          <Overview>
            {detailResult.overview.length > 450
              ? `${detailResult.overview.substring(0, 450)}...`
              : detailResult.overview}
          </Overview>
          <ButtonContainer>
            <Button>
              <FontAwesomeIcon icon={faPlay} /> Play
            </Button>
            <Button>
              <FontAwesomeIcon icon={faPlus} /> My List
            </Button>
          </ButtonContainer>
        </RightContent>
      </Content>
    </Container>
  );

DetailPresenter.propTypes = {
  loading: PropTypes.bool.isRequired,
  detailResult: PropTypes.object,
  error: PropTypes.string
};

export default DetailPresenter;
```

<br>

<br>