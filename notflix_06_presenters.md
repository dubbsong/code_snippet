#### prop-types 설치

```bash
$ yarn add prop-types
```

<br>

#### 코드 작성

- HomePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => null;

HomePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  upcoming: PropTypes.array,
  popular: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default HomePresenter;
```

<br>

- TVPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) => null;

TVPresenter.propTypes = {
  topRated: PropTypes.array,
  popular: PropTypes.array,
  airingToday: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default TVPresenter;
```

<br>

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const SearchPresenter = ({ movieResults, tvResults, loading, searchTerm, handleSubmit, error }) => null;

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  searchTerm: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired,
  error: PropTypes.string
}

export default SearchPresenter;
```

<br>

- DetailPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const DetailPresenter = ({ result, loading, error }) => null;

DetailPresenter.propTypes = {
  result: PropTypes.object,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default DetailPresenter;
```

> 몇 가지 콘솔 에러 발생

<br>

#### 파일 생성

```bash
$ cd src
$ cd Components
$ touch Section.js
```

<br>

#### 코드 작성

- Section.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div``;

const Title = styled.span``;

const Grid = styled.div``;

const Section = ({ title, children }) => (
  <Container>
    <Title>{title}</Title>
    <Grid>{children}</Grid>
  </Container>
);

Section.propTypes = {
  title: PropTypes.string.isRequired,
  children: PropTypes.oneOfType([
    PropTypes.arrayOf(PropTypes.node),
    PropTypes.node
  ])
}

export default Section;
```

<br>

#### 코드 추가 (Home)

- HomePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';

const Container = styled.div`
	padding: 20px;
`;

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => loading ? null : (
  <Container>
    {nowPlaying && nowPlaying.length > 0 && (
      <Section title="Now Playing">
        {nowPlaying.map(movie => (
          <span key={movie.id}>{movie.title}</span>
        ))}
      </Section>
    )}
    {popular && popular.length > 0 && (
      <Section title="Popular Movies">
        {popular.map(movie => (
          <span key={movie.id}>{movie.title}</span>
        ))}
      </Section>
    )}
    {upcoming && upcoming.length > 0 && (
      <Section title="Upcoming Movies">
        {upcoming.map(movie => (
          <span key={movie.id}>{movie.title}</span>
        ))}
      </Section>
    )}
  </Container>
);

HomePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  upcoming: PropTypes.array,
  popular: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default HomePresenter;
```

<br>

#### CSS 추가

- Section.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
	:not(:last-child) {
		margin-bottom: 50px;
	}
`;

const Title = styled.span`
	font-size: 14px;
	font-weight: 600;
`;

const Grid = styled.div`
	margin-top: 25px;
	display: grid;
	grid-template-columns: repeat(auto-fill, 125px);
	grid-gap: 25px;
`;

const Section = ({ title, children }) => (
  <Container>
    <Title>{title}</Title>
    <Grid>{children}</Grid>
  </Container>
);

Section.propTypes = {
  title: PropTypes.string.isRequired,
  children: PropTypes.oneOfType([
    PropTypes.arrayOf(PropTypes.node),
    PropTypes.node
  ])
}

export default Section;
```

<br>

#### 코드 추가 (TV)

- TVPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';

const Container = styled.div`
	padding: 20px;
`;

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) => loading ? null : (
  <Container>
    {topRated && topRated.length > 0 && (
      <Section title="Top Rated Shows">
        {topRated.map(show => show.name)}
      </Section>
    )}
    {popular && popular.length > 0 && (
      <Section title="Popular Shows">
        {popular.map(show => show.name)}
      </Section>
    )}
    {airingToday && airingToday.length > 0 && (
      <Section title="Airing Today">
        {airingToday.map(show => show.name)}
      </Section>
    )}
  </Container>
);

TVPresenter.propTypes = {
  topRated: PropTypes.array,
  popular: PropTypes.array,
  airingToday: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default TVPresenter;
```

> 정상 작동하지만, TV 클릭 시 처음에 비어있다가 채워진다.

<br>

#### 파일 생성

```bash
$ cd src
$ cd Components
$ touch Loader.js
```

<br>

#### 코드 작성

- Loader.js

```react
import React from 'react';
import styled from 'styled-components';

const Container = styled.div`
	width: 100vw;
	height: 100vh;
	display: flex;
	justify-content: center;
	font-size: 32px;
	margin-top: 40px;
`;

export default () => (
  <Container>
    <span role="img" aria-label="Loading">
      ⏰
    </span>
  </Container>
);
```

<br>

#### 코드 추가 (import Loader)

- HomePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';

const Container = styled.div`
	padding: 20px;
`;

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => 
	loading ? (
    <Loader />
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => movie.title)}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => movie.title)}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => movie.title)}
        </Section>
      )}
    </Container>
  );

HomePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  upcoming: PropTypes.array,
  popular: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default HomePresenter;
```

<br>

- TVPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';

const Container = styled.div`
	padding: 20px;
`;

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
	loading ? (
    <Loader />
  ) : (
    <Container>
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated Shows">
          {topRated.map(show => show.name)}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Shows">
          {popular.map(show => show.name)}
        </Section>
      )}
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          {airingToday.map(show => show.name)}
        </Section>
      )}
    </Container>
  )

TVPresenter.propTypes = {
  topRated: PropTypes.array,
  popular: PropTypes.array,
  airingToday: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default TVPresenter;
```

> 이전보다 빠르게 로딩된다.

<br>

#### 코드 수정

- HomePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';

const Container = styled.div`
	padding: 20px;
`;

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => 
	loading ? (
    <Loader />
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => (
            <span key={movie.id}>{movie.title}</span>
          ))}
        </Section>
      )}
    </Container>
  );

HomePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  upcoming: PropTypes.array,
  popular: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default HomePresenter;
```

<br>

- TVPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';

const Container = styled.div`
	padding: 20px;
`;

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
	loading ? (
    <Loader />
  ) : (
    <Container>
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated Shows">
          {topRated.map(show => (
            <span key={show.id}>{show.name}</span>
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Shows">
          {popular.map(show => (
            <span key={show.id}>{show.name}</span>
          ))}
        </Section>
      )}
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          {airingToday.map(show => (
            <span key={show.id}>{show.name}</span>
          ))}
        </Section>
      )}
    </Container>
  )

TVPresenter.propTypes = {
  topRated: PropTypes.array,
  popular: PropTypes.array,
  airingToday: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default TVPresenter;
```

<br>

#### 코드 추가

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div``;

const Form = styled.form``;

const Input = styled.input``;

const SearchPresenter = ({ 
  movieResults,
  tvResults,
  loading,
  searchTerm,
  handleSubmit,
  error
}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input placeholder="Search Movies or TV Shows..." value={searchTerm} />
    </Form>
  </Container>
);

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  searchTerm: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired,
  error: PropTypes.string
}

export default SearchPresenter;
```

<br>

- SearchContainer.js

```react
import React from 'react';
import SearchPresenter from './SearchPresenter';
import { moviesApi, tvApi } from 'api';

export default class extends React.Component {
  state = {
    movieResults: null,
    tvResults: null,
    searchTerm: '',
    loading: false,
    error: null
  };

  handleSubmit = event => {
    event.preventDefault();
    
    const { searchTerm } = this.state;
    
    if (searchTerm !== '') {
      this.searchByTerm();
    }
  };
  
  searchByTerm = async () => {
    const { searchTerm } = this.state;
    
    try {
      const {
        data: { results: movieResults }
      } = await moviesApi.search(searchTerm);
      
      const {
        data: { results: tvResults }
      } = await tvApi.search(searchTerm);
      
      this.setState({
        movieResults,
        tvResults
      });
    } catch {
      this.setState({
        error: "Can't find results."
      });
    } finally {
      this.setState({
        loading: false
      });
    }
  }
  
  render() {
    const { movieResults, tvResults, searchTerm, loading, error } = this.state;
    
    return (
      <SearchPresenter
        movieResults={movieResults}
        tvResults={tvResults}
        searchTerm={searchTerm}
        loading={loading}
        error={error}
        handleSubmit={this.handleSubmit}
      />
    );
  }
}
```

<br>

#### 코드 추가

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
	padding: 20px;
`;

const Form = styled.form`
	width: 100%;
	margin-bottom: 50px;
`;

const Input = styled.input`
	all: unset;
	width: 100%;
	font-size: 28px;
`;

const SearchPresenter = ({ 
  movieResults,
  tvResults,
  loading,
  searchTerm,
  handleSubmit,
  updateTerm,
  error
}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input 
        placeholder="Search Movies or TV Shows..."
        value={searchTerm}
        onChange={updateTerm}
      />
    </Form>
  </Container>
);

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  searchTerm: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired,
  updateTerm: PropTypes.func.isRequired,
  error: PropTypes.string
}

export default SearchPresenter;
```

<br>

#### 코드 추가

- SearchContainer.js

```react
import React from 'react';
import SearchPresenter from './SearchPresenter';
import { moviesApi, tvApi } from 'api';

export default class extends React.Component {
  state = {
    movieResults: null,
    tvResults: null,
    searchTerm: '',
    loading: false,
    error: null
  };

  handleSubmit = event => {
    event.preventDefault();
    
    const { searchTerm } = this.state;
    
    if (searchTerm !== '') {
      this.searchByTerm();
    }
  };

  updateTerm = (event) => {
    // 1. 테스트 후 삭제
    console.log(event);
    
    // 2. 테스트 후 삭제
    const { target } = event;
    console.log(target);
    
    // 3. 테스트 후 삭제 노노
    const {
      target: { value }
    } = event;
    console.log(value);
    
    // 4. 테스트 후 삭제 노노
    this.setState({
      searchTerm: value
    });
  };
  
  searchByTerm = async () => {
    const { searchTerm } = this.state;
    
    try {
      const {
        data: { results: movieResults }
      } = await moviesApi.search(searchTerm);
      
      const {
        data: { results: tvResults }
      } = await tvApi.search(searchTerm);
      
      this.setState({
        movieResults,
        tvResults
      });
    } catch {
      this.setState({
        error: "Can't find results."
      });
    } finally {
      this.setState({
        loading: false
      });
    }
  }
  
  render() {
    const { movieResults, tvResults, searchTerm, loading, error } = this.state;
    
    return (
      <SearchPresenter
        movieResults={movieResults}
        tvResults={tvResults}
        searchTerm={searchTerm}
        loading={loading}
        error={error}
        handleSubmit={this.handleSubmit}
        updateTerm={this.updateTerm}
      />
    );
  }
}
```

<br>

#### 코드 추가

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';

const Container = styled.div`
	padding: 20px;
`;

const Form = styled.form`
	width: 100%;
	margin-bottom: 50px;
`;

const Input = styled.input`
	all: unset;
	width: 100%;
	font-size: 28px;
`;

const SearchPresenter = ({ 
  movieResults,
  tvResults,
  loading,
  searchTerm,
  handleSubmit,
  updateTerm,
  error
}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input 
        placeholder="Search Movies or TV Shows..."
        value={searchTerm}
        onChange={updateTerm}
      />
    </Form>
    {loading ? (
      <Loader />
    ) : (
      <React.Fragment>
        {movieResults && movieResults.length > 0 && (
          <Section title="Movie Results">
            {movieResults.map(movie => (
              <span key={movie.id}>
                {movie.title}
              </span>
            ))}
          </Section>
        )}
        {tvResults && tvResults.length > 0 && (
          <Section title="TV Show Results">
            {tvResults.map(show => (
              <span key={show.id}>
                {show.name}
              </span>
            ))}
          </Section>
        )}
      </React.Fragment>
    )}
  </Container>
);

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  searchTerm: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired,
  updateTerm: PropTypes.func.isRequired,
  error: PropTypes.string
}

export default SearchPresenter;
```

> Search 탭에서 `code`를 검색하면, code가 들어간 영화 및 TV show가 검색된다.

<br>

<br>

## (for error & not found)

#### 파일 생성

```bash
$ cd src
$ cd Components
$ touch Message.js
```

<br>

#### 코드 추가

- Message.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
	width: 100vw;
	display: flex;
	justify-content: center;
`;

const Text = styled.span`
	color: ${props => props.color};
`;

const Message = ({ text, color }) => (
  <Container>
    <Text color={color}>{text}</Text>
  </Container>
);

Message.propTypes = {
  text: PropTypes.string.isRequired,
  color: PropTypes.string.isRequired
}

export default Message;
```

<br>

#### import Error

1. HomeContainer.js

```react
try {
  throw Error();	// 테스트 후 삭제
  
  ...
}
```

<br>

2. HomePresenter.js

```react
...
import Message from 'Components/Message';

...
<Container>
  <Section>
  </Section>
  ...
  )}
  {error && <Message text={error} color="#e74c3c" />}
</Container>
```

> Movies 탭에 `Can't find movie information.`이 표시된다.

<br>

- TVContainer.js

```react
try {
  throw Error();	// 테스트 후 삭제
  
  ...
}
```

<br>

- TVPresenter.js

```react
...
import Message from 'Components/Message';

...
<Container>
  <Section>
  </Section>
  ...
  )}
  {error && <Message text={error} color="#e74c3c" />}
</Container>
```

> TV 탭에 `Can't find TV information.`이 표시된다.

<br>

- SearchPresenter.js

```react
...
import Message from 'Components/Message';

...
<Container>
  <React.Fragment>
    <Section>
      ...
    </Section>
    ...
    )}
    {error && <Message text={error} color="#e74c3c" />}
    {tvResults &&
    movieResults &&
    tvResults.length === 0 &&
    movieResults.length === 0 && (
      <Message
        text="Nothing found"
        color="#95a5a6"
      />
    )}
  </React.Fragment>
</Container>
```

> 에러가 발생하면, `Can't find results.`가 출력된다.
>
> 없는 것을 검색하면, `Nothing found`가 출력된다.

------

<br>

#### (for Poster)

#### 파일 생성

```bash
$ cd src
$ cd Components
$ touch Poster.js
```

<br>

- Poster.js (01)

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div``;

const ImageContainer = styled.div``;

const Image = styled.div``;

const Title = styled.span``;

const Rating = styled.span``;

const Year = styled.span``;

const Poster = ({ id, imageUrl, title, rating, year, isMovie = false }) => (
  <Container>
    <ImageContainer>
      <Image bgUrl={imageUrl} />
      <Rating>
        <span role="img" aria-label="rating">
          ⭐️
        </span>{" "}
        {rating}/10
      </Rating>
    </ImageContainer>
    <Title>{title}</Title>
    <Year>{year}</Year>
  </Container>
);

Poster.propTypes = {
  id: PropTypes.number.isRequired,
  imageUrl: PropTypes.string,
  title: PropTypes.string.isRequired,
  rating: PropTypes.number,
  year: PropTypes.string,
  isMovie: PropTypes.bool
}

export default Poster;
```

<br>

- Poster.js (02, elements를 \<Link> 태그 내로 이동)

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import { Link } from 'react-router-dom';

const Container = styled.div``;

const Image = styled.div``;

const Rating = styled.span``;

const ImageContainer = styled.div``;

const Title = styled.span``;

const Year = styled.span``;

const Poster = ({ id, imageUrl, title, rating, year, isMovie = false }) => (
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
  title: PropTypes.string.isRequired,
  rating: PropTypes.number,
  year: PropTypes.string,
  isMovie: PropTypes.bool
}

export default Poster;
```

<br>

#### 코드 수정

- HomePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';
import Message from 'Components/Message';
import Poster from 'Components/Poster';

const Container = styled.div`
	padding: 20px;
`;

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => 
	loading ? (
    <Loader />
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <Poster />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => (
            <Poster />
          ))}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => (
            <Poster />
          ))}
        </Section>
      )}
      {error && <Message text={error} color="#e74c3c" />}
    </Container>
  );

HomePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  upcoming: PropTypes.array,
  popular: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default HomePresenter;
```

> 1차적으로 화면에 정상적으로 보여진다.
>
> 개발자 도구의 Network에서, movie가 어떻게 생겼는지 확인한다.
>
> Network > `now_playing?api_…`을 우클릭 후, `open in a new tab` 클릭해서 JSON을 확인할 수 있다.

> **Example:**
>
> `title`은 `original_title`로 되어 있다.
>
> `poster`는 `poster_path`로 되어 있다.

<br>

#### 코드 추가

- HomePresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';
import Message from 'Components/Message';
import Poster from 'Components/Poster';

const Container = styled.div`
	padding: 20px;
`;

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => 
	loading ? (
    <Loader />
  ) : (
    <Container>
      {nowPlaying && nowPlaying.length > 0 && (
        <Section title="Now Playing">
          {nowPlaying.map(movie => (
            <Poster
              key={movie.id}
              id={movie.id}
              imageUrl={movie.poster_path}
              title={movie.original_title}
              rating={movie.vote_average}
              year={movie.release_date.substring(0, 4)}
              isMovie={true}
            />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Movies">
          {popular.map(movie => (
            <Poster
              key={movie.id}
              id={movie.id}
              imageUrl={movie.poster_path}
              title={movie.original_title}
              rating={movie.vote_average}
              year={movie.release_date.substring(0, 4)}
              isMovie={true}
            />
          ))}
        </Section>
      )}
      {upcoming && upcoming.length > 0 && (
        <Section title="Upcoming Movies">
          {upcoming.map(movie => (
            <Poster
              key={movie.id}
              id={movie.id}
              imageUrl={movie.poster_path}
              title={movie.original_title}
              rating={movie.vote_average}
              year={movie.release_date.substring(0, 4)}
              isMovie={true}
            />
          ))}
        </Section>
      )}
      {error && <Message text={error} color="#e74c3c" />}
    </Container>
  );

HomePresenter.propTypes = {
  nowPlaying: PropTypes.array,
  upcoming: PropTypes.array,
  popular: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default HomePresenter;
```

> 정상 작동
>
> 아무거나 클릭하면, url에 해당 정보가 표시된다.

<br>

#### 번외: 년월일에서 년만 뽑기

```js
const sth = '2019-07-01';
sth.substring(0, 4);	// '2019'
```

<br>

#### 번외: better than before

> `year={movie.release_date.substring(0, 4)}`보다 `year={movie.release_date && movie.release_date.substring(0, 4)}`가 안전하다.

<br>

#### 코드 추가

- TVPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';
import Message from 'Components/Message';
import Poster from 'Components/Poster';

const Container = styled.div`
	padding: 20px;
`;

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) =>
	loading ? (
    <Loader />
  ) : (
    <Container>
      {topRated && topRated.length > 0 && (
        <Section title="Top Rated Shows">
          {topRated.map(show => (
            <Poster
              key={show.id}
              id={show.id}
              imageUrl={show.poster_path}
              title={show.original_name}
              rating={show.vote_average}
              year={show.first_air_date.substring(0, 4)}
            />
          ))}
        </Section>
      )}
      {popular && popular.length > 0 && (
        <Section title="Popular Shows">
          {popular.map(show => (
            <Poster
              key={show.id}
              id={show.id}
              imageUrl={show.poster_path}
              title={show.original_name}
              rating={show.vote_average}
              year={show.first_air_date.substring(0, 4)}
            />
          ))}
        </Section>
      )}
      {airingToday && airingToday.length > 0 && (
        <Section title="Airing Today">
          {airingToday.map(show => (
            <Poster
              key={show.id}
              id={show.id}
              imageUrl={show.poster_path}
              title={show.original_name}
              rating={show.vote_average}
              year={show.first_air_date.substring(0, 4)}
            />
          ))}
        </Section>
      )}
      {error && <Message text={error} color="#e74c3c" />}
    </Container>
  )

TVPresenter.propTypes = {
  topRated: PropTypes.array,
  popular: PropTypes.array,
  airingToday: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
}

export default TVPresenter;
```

<br>

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import Section from 'Components/Section';
import Loader from 'Components/Loader';
import Message from 'Components/Message';
import Poster from 'Components/Poster';

const Container = styled.div`
	padding: 20px;
`;

const Form = styled.form`
	width: 100%;
	margin-bottom: 50px;
`;

const Input = styled.input`
	all: unset;
	width: 100%;
	font-size: 28px;
`;

const SearchPresenter = ({ 
  movieResults,
  tvResults,
  loading,
  searchTerm,
  handleSubmit,
  updateTerm,
  error
}) => (
  <Container>
    <Form onSubmit={handleSubmit}>
      <Input 
        placeholder="Search Movies or TV Shows..."
        value={searchTerm}
        onChange={updateTerm}
      />
    </Form>
    {loading ? (
      <Loader />
    ) : (
      <React.Fragment>
        {movieResults && movieResults.length > 0 && (
          <Section title="Movie Results">
            {movieResults.map(movie => (
              <Poster
                key={movie.id}
                id={movie.id}
                imageUrl={movie.poster_path}
                title={movie.original_title}
                rating={movie.vote_average}
                year={movie.release_date.substring(0, 4)}
                isMovie={true}
              />
            ))}
          </Section>
        )}
        {tvResults && tvResults.length > 0 && (
          <Section title="TV Show Results">
            {tvResults.map(show => (
              <Poster
                key={show.id}
                id={show.id}
                imageUrl={show.poster_path}
                title={show.original_name}
                rating={show.vote_average}
                year={show.first_air_date.substring(0, 4)}
              />
            ))}
          </Section>
        )}
        {error && <Message text={error} color="#e74c3c" />}
        {tvResults &&
        movieResults &&
        tvResults.length === 0 &&
        movieResults.length === 0 && (
          <Message
            text="Nothing found"
            color="#95a5a6"
          />
        )}
      </React.Fragment>
    )}
  </Container>
);

SearchPresenter.propTypes = {
  movieResults: PropTypes.array,
  tvResults: PropTypes.array,
  loading: PropTypes.bool.isRequired,
  searchTerm: PropTypes.string,
  handleSubmit: PropTypes.func.isRequired,
  updateTerm: PropTypes.func.isRequired,
  error: PropTypes.string
}

export default SearchPresenter;
```

> 정상 작동

<br>

#### CSS 추가

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

const Title = styled.span`
	display: block;
	margin-bottom: 3px;
`;

const Year = styled.span`
	font-size: 10px;
	color: rgba(255, 255, 255, 0.5);
`;

const Poster = ({ id, imageUrl, title, rating, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <Container>
      <ImageContainer>
        <Image
          bgUrl={
            imageUrl
            	? `https://image.tmdb.org/t/p/w300${imageUrl}`
            	: require("../assets/noPosterSmall.png")
          }
        />
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

...
```

<br>

#### noPoster 작업

1. notflix 폴더
2. src
3. assets 폴더 생성
4. noPosterSmall.png 파일 위치
5. 이미지가 없는 포스터에 `noPosterSmall.png` 파일이 표시된다.

<br>

#### 코드 추가 (for shorter title)

- Poster.js

```react
const Poster = ({ id, imageUrl, title, rating, year, isMovie = false }) => (
  <Link to={isMovie ? `/movie/${id}` : `/show/${id}`}>
    <Container>
      <ImageContainer>
        <Image
          bgUrl={
            imageUrl
            	? `https://image.tmdb.org/t/p/w300${imageUrl}`
            	: require("../assets/noPosterSmall.png")
          }
        />
        <Rating>
          <span role="img" aria-label="rating">
            ⭐️
          </span>{' '}
          {rating}/10
        </Rating>
      </ImageContainer>
      <Title>
        {title.length > 18 ? `${title.substring(0, 18)}...` : title}
      </Title>
      <Year>{year}</Year>
    </Container>
  </Link>
);
```

<br>

#### 코드 추가 (for Detail Poster & Text)

- DetailPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';
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

const DetailPresenter = ({ result, loading, error }) =>
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
              : require('../../assets/noPosterSmall.png')
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
              {result.runtime ? result.runtime : result.episode_run_time[0]} min
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
          <Overview>{result.overview}</Overview>
        </Data>
      </Content>
    </Container>
  );

DetailPresenter.propTypes = {
  result: PropTypes.object,
  loading: PropTypes.bool.isRequired,
  error: PropTypes.string
};

export default DetailPresenter;

```

<br>

#### react-helmet 설치 (for Chainging Tab Title)

```bash
$ yarn add react-helmet
```

<br>

#### 코드 추가

- HomePresenter.js

```react
...
import styled from 'styled-components';
import Helmet from 'react-helmet';
...

...

const HomePresenter = ({ nowPlaying, upcoming, popular, loading, error }) => (
  <React.Fragment>
    <Helmet>
      <title>Movies | NOTFLIX</title>
    </Helmet>
    {loading ? (
      <Loader />
    ) : (
      ...
    )}
  </React.Fragment>
);

...
```

> Movies 탭에 `Movies | NOTFLIX`가 표시된다.

<br>

- TVPresenter.js

```react
...
import styled from 'styled-components';
import Helmet from 'react-helmet';
...

...

const TVPresenter = ({ topRated, popular, airingToday, loading, error }) => (
  <React.Fragment>
    <Helmet>
      <title>TV | NOTFLIX</title>
    </Helmet>
    {loading ? (
      <Loader />
    ) : (
      ...
    )}
  </React.Fragment>
);

...
```

> TV 탭에 `TV | NOTFLIX`가 표시된다.

<br>

- SearchPresenter.js

```react
...
import styled from 'styled-components';
import Helmet from 'react-helmet';
...

...
<Container>
  <Helmet>
    <title>Search | NOTFLIX</title>
  </Helmet>
  <Form onSubmit={handleSubmit}>
    ...
  </Form>
  ...
</Container>
```

> Search 탭에 `Search | NOTFLIX`가 표시된다.

<br>

- DetailPresenter.js

```react
...
import styled from 'styled-components';
import Helmet from 'react-helmet';
...

const DetailPresenter = ({ result, loading, error }) =>
loading ? (
  <React.Fragment>
    <Helmet>
      <title>Loading | NOTFLIX</title>
    </Helmet>
    <Loader />
  </React.Fragment>
) : (
  <Container>
    <Helmet>
      <title>{result.original_title ? result.original_title : result.original_name}{' '} | NOTFLIX</title>
    </Helmet>
    <Backdrop ... />
  </Container>
);
```

> Detail 탭에 `해당 Detail | NOTFLIX`가 표시된다.

<br>

###### DONE without Deployment