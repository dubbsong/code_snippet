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
    font-family: 'Roboto', sans-serif;
    font-size: 14px;
    background-color: #141414;
    color: #ffffff;
    letter-spacing: 0.5px;
  }

  ...
`;

...
```

> `letter-spacing: 0.5px;`을 추가한다.
>
> `padding-top: 70px;`을 제거한다.

<br>

###### 이미지 추가: `movie_bg.jpg` / `tv_bg.webp`

```bash
assets
  └─ img
      ├─ movie_bg.jpg
      └─ tv_bg.webp
```

<br>

###### 배경 이미지 설정

- MoviePresenter.js

```react
import React from 'react';
import HeaderMovie from 'Components/HeaderMovie';

MoviePresenter = () => (
  <HeaderMovie />
);

export default MoviePresenter;
```

- TVPresenter.js

```react
import React from 'react';
import HeaderTV from 'Components/HeaderTV';

TVPresenter = () => (
  <HeaderTV />
);

export default TVPresenter;
```

- HeaderMovie.js

```react
import React from 'react';
import styled from 'styled-components';
import bg from 'assets/img/movie_bg.jpg';

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
import bg from 'assets/img/tv_bg.webp';

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

<br>

###### Header 구조 설정

- HeaderMovie.js

```react
...

const Content = styled.div``;

const Title = styled.h2``;

const Button = styled.button``;

const Summary = styled.p``;

const Gradient = styled.div``;

export default () => (
  <Header>
    <Content>
      <Title>The Dark Knight</Title>
      <Button>Play</Button>
      <Button>My List</Button>
      <Summary>
        A city swarms with fear. And a twisted, cackling madman will shatter the very notion of a hero. Why so serious?
      </Summary>
    </Content>
    <Gradient />
  </Header>
);
```

- HeaderTV.js

```react
...

const Content = styled.div``;

const Title = styled.h2``;

const Button = styled.button``;

const Summary = styled.p``;

const Gradient = styled.div``;

export default () => (
  <Header>
    <Content>
      <Title>Money Heist</Title>
      <Button>Play</Button>
      <Button>My List</Button>
      <Summary>
        Eight thieves take hostages and lock themselves in the Royal Mint of Spain as a criminal mastermind manipulates the police to carry out his plan.
      </Summary>
    </Content>
    <Gradient />
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

const Content = styled.div`
  position: absolute;
  top: 55%;
  left: 0;
  padding: 0 4%;
  width: 40%;

  @media (max-width: 576px) {
    width: 100%;
    top: 60%;
  }
`;

const Title = styled.h2`
  font-size: 40px;
  font-weight: 900;
  margin: 0 0 10px 0;
  text-shadow: 2px 2px 5px #141414;

  @media (max-width: 576px) {
    font-size: 26px;
  }
`;

const Button = styled.button`
  background-color: rgba(51, 51, 51, 0.4);
  color: inherit;
  padding: 0.75em 2.4em;
  border-width: 0;
  border-radius: 0.2vw;
  font-size: 1vw;
  margin-right: 0.75em;
  letter-spacing: 1.5px;
  cursor: pointer;

  &:hover {
    background-color: #e6e6e6;
    color: #000000;
    box-shadow: 0 0.6vw 1vw -0.4vw rgba(0, 0, 0, 0.35);
  }

  &:focus {
    outline: none;
  }
`;

const Summary = styled.p`
  font-size: 16px;
  line-height: 3vh;
  text-align: justify;
  color: #e6e6e6;
  text-shadow: 2px 2px 5px #141414;
  padding: 16px 0;

  @media (max-width: 576px) {
    font-size: 12px;
  }
`;

const Gradient = styled.div`
  background-image: linear-gradient(
    180deg,
    transparent,
    rgba(35, 35, 35, 0.6),
    rgba(20, 20, 20, 1)
  );
  height: 80vh;
`;

export default () => (
  <Header>
    <Content>
      ...
      <Button>
        <FontAwesomeIcon icon={faPlay} /> Play
      </Button>
      <Button>
        <FontAwesomeIcon icon={faPlus} /> My List
      </Button>
      ...
    </Content>
    <Gradient />
  </Header>
);
```

<br>

<br>