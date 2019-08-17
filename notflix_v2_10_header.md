###### 컴포넌트 생성: `MovieHeader`

```bash
$ cd src
$ cd components
$ touch MovieHeader.js
```

<br>

###### MovieHeader 설정

- GlobalStyle.js

```react
...

const globalStyle = createGlobalStyle`
  ...

  body {
    font-family: 'Blinker', sans-serif;
    font-size: 14px;
    background-color: #141414;
    color: #ffffff;
  }

  ...
`;

...
```

> `padding-top: 70px;` 제거

<br>

###### 이미지 추가

```bash
assets
  └─ bg_movie.webp
```

<br>

###### 배경 이미지 설정

- MovieHeader.js

```react
import React from 'react';
import styled from 'styled-components';
import bg from 'assets/bg_movie.webp';

const Container = styled.div`
  background-image: url(${bg});
  background-size: cover;
  background-position: top center;
  height: 80vh;
`;

export default () => (
  <Container>
    <h4>오많배</h4>
  </Container>
);
```

- MoviePresenter.js

```react
...
import Loader from 'components/Loader';
import MovieHeader from 'components/MovieHeader';

const MoviePresenter = ({...}) =>
  loading ? (
    <Loader />
  ) : (
    <React.Fragment>
      <MovieHeader />
    </React.Fragment>
  );

...
```

> Header 배경 이미지가 표시된다.

<br>

<br>

###### Header 구조 설정

- MovieHeader.js

```react
...

const Gradient = styled.div``;

const Content = styled.div``;

const Title = styled.h2``;

const Button = styled.button``;

const Overview = styled.p``;

export default () => (
  <Container>
    <Gradient />
    <Content>
      <Title>The Dark Knight</Title>
      <Button>Play</Button>
      <Button>My List</Button>
      <Overview>
        A city swarms with fear. And a twisted, cackling madman will shatter the
        very notion of a hero. Why so serious?
      </Overview>
    </Content>
  </Container>
);
```

<br>

###### Style 설정

- MovieHeader.js

```react
...
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faPlay, faPlus } from '@fortawesome/free-solid-svg-icons';

const Container = styled.div`
  ...
  position: relative;
`;

const Gradient = styled.div`
  background-image: linear-gradient(
    180deg,
    transparent,
    rgba(40, 40, 40, 0.6),
    rgba(20, 20, 20, 1)
  );
  height: 80vh;
`;

const Content = styled.div`
  position: absolute;
  top: 50%;
  left: 0;
  padding: 0 4%;
  width: 35%;

  @media (max-width: 768px) {
    top: 60%;
    width: 100%;
  }
`;

const Title = styled.h2`
  font-size: 40px;
  font-weight: 900;
  letter-spacing: 1.2px;
  margin-bottom: 8px;
  text-shadow: 5px 5px 20px #141414;

  @media (max-width: 768px) {
    font-size: 24px;
  }
`;

const Button = styled.button`
  width: 120px;
  height: 30px;
  background-color: rgba(51, 51, 51, 0.4);
  color: inherit;
  font-size: 14px;
  letter-spacing: 1.5px;
  border-width: 0;
  border-radius: 2px;
  margin-right: 8px;
  cursor: pointer;

  &:hover {
    background-color: #e6e6e6;
    color: #000000;
  }

  &:focus {
    outline: none;
  }

  @media (max-width: 768px) {
    width: 85px;
    height: 22px;
    font-size: 8px;
  }
`;

const Overview = styled.p`
  font-size: 16px;
  letter-spacing: 1.2px;
  line-height: 1.2;
  color: #e6e6e6;
  text-shadow: 5px 5px 20px #141414;
  margin-top: 8px;
`;

const StyledIcon = styled(FontAwesomeIcon)`
  font-size: 12px;
`;

export default () => (
  <Container>
    ...
    <Content>
      ...
      <Button>
        <StyledIcon icon={faPlay} /> Play
      </Button>
      <Button>
        <StyledIcon icon={faPlus} /> My List
      </Button>
      ...
    </Content>
  </Container>
);
```

<br>

> `TVHeader`도 동일하게 진행쓰

<br>

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set Header';
$ git push origin master
```

<br>

<br>