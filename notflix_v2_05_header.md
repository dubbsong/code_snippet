###### 컴포넌트 생성: `HeaderMovie` / `HeaderTV`

```bash
$ cd src
$ cd Components
$ touch HeaderMovie.js
$ touch HeaderTV.js
```

<br>

###### HeaderMovie 설정

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

###### 이미지 추가: `bg_movie.jpg` / `bg_tv.webp`

```bash
assets
  └─ img
      ├─ bg_movie.jpg
      └─ bg_tv.webp
```

<br>

###### 배경 이미지 설정

- MoviePresenter.js

```react
import React from 'react';
import HeaderMovie from 'Components/HeaderMovie';

const MoviePresenter = () => <HeaderMovie />;

export default MoviePresenter;
```

- TVPresenter.js

```react
import React from 'react';
import HeaderTV from 'Components/HeaderTV';

const TVPresenter = () => <HeaderTV />;

export default TVPresenter;
```

- HeaderMovie.js

```react
import React from 'react';
import styled from 'styled-components';
import bg from 'assets/img/bg_movie.jpg';

const Header = styled.header`
  background-image: url(${bg});
  background-size: cover;
  background-position: top center;
  height: 80vh;
`;

export default () => (
  <Header>
    <h4>오많배</h4>
  </Header>
);
```

- HeaderTV.js

```react
import React from 'react';
import styled from 'styled-components';
import bg from 'assets/img/bg_tv.webp';

const Header = styled.header`
  background-image: url(${bg});
  background-size: cover;
  background-position: top center;
  height: 80vh;
`;

export default () => (
  <Header>
    <h4>오많배</h4>
  </Header>
);
```

> 각 Header 배경 이미지가 표시된다.

<br>

<br>

###### Header 구조 설정

- HeaderMovie.js

```react
...

const Gradient = styled.div``;

const Content = styled.div``;

const Title = styled.h2``;

const Button = styled.button``;

const Summary = styled.p``;

export default () => (
  <Header>
    <Gradient />
    <Content>
      <Title>The Dark Knight</Title>
      <Button>Play</Button>
      <Button>My List</Button>
      <Summary>
        A city swarms with fear. And a twisted, cackling madman will shatter the
        very notion of a hero. Why so serious?
      </Summary>
    </Content>
  </Header>
);
```

- HeaderTV.js

```react
...

const Gradient = styled.div``;

const Content = styled.div``;

const Title = styled.h2``;

const Button = styled.button``;

const Summary = styled.p``;

export default () => (
  <Header>
    <Gradient />
    <Content>
      <Title>Love Death + Robots</Title>
      <Button>Play</Button>
      <Button>My List</Button>
      <Summary>
        Logn after the fall of humanity, three robots embark on a sightseeing
        tour of a post-apocalyptic city.
      </Summary>
    </Content>
  </Header>
);
```

<br>

###### Header CSS 설정

- HeaderMovie.js
- HeaderTV.js

```react
...
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faPlay } from '@fortawesome/free-solid-svg-icons';
import { faPlus } from '@fortawesome/free-solid-svg-icons';

const Header = styled.header`
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

  @media (max-width: 576px) {
		top: 60%;
    width: 100%;
  }
`;

const Title = styled.h2`
  font-size: 40px;
  letter-spacing: 1.5px;
  margin-bottom: 10px;
  text-shadow: 2px 2px 10px #141414;

  @media (max-width: 576px) {
    font-size: 24px;
  }
`;

const Button = styled.button`
  background-color: rgba(51, 51, 51, 0.4);
  color: inherit;
  width: 120px;
  height: 30px;
  font-size: 14px;
  letter-spacing: 1.5px;
  border-width: 0;
  border-radius: 2px;
  margin-right: 5px;
  cursor: pointer;

  &:hover {
    background-color: #e6e6e6;
    color: #000000;
  }

  &:focus {
    outline: none;
  }

  @media (max-width: 576px) {
    width: 90px;
    height: 25px;
    font-size: 8px;
  }
`;

const Summary = styled.p`
  font-size: 16px;
  line-height: 3vh;
  text-align: justify;
  color: #e6e6e6;
  margin-top: 10px;
  text-shadow: 2px 2px 10px #141414;
`;

export default () => (
  <Header>
    ...
    <Content>
      <Title>...</Title>
      <Button>
        <FontAwesomeIcon icon={faPlay} /> Play
      </Button>
      <Button>
        <FontAwesomeIcon icon={faPlus} /> My List
      </Button>
      <Summary>...</Summary>
    </Content>
  </Header>
);
```

<br>

<br>