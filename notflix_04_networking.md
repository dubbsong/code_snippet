#### DB 데이터 가져오기

1. [The Movie DB](https://www.themoviedb.org/) 회원가입
2. profile 클릭
3. settings 클릭
4. API 클릭
5. Request an API Key의 click here 클릭
6. Developer 선택
7. Accept 클릭
8. 개인정보 입력
9. API Key 복사
10. Documentation의 developers.themoviedb.org 클릭
11. TV 클릭
12. Get Popular 클릭
13. Try it out 클릭
14. Your TMDb API Key에 복사한 API Key 붙여넣기
15. SEND REQUEST 클릭
    - 객체로 데이터가 들어오는 것을 확인할 수 있다.
    - 버튼 옆의 URL로 요청을 만들 것이다.

<br>

#### README 작성

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie Discovery App.

## Screens
- [] Home
- [] TV
- [] Search
- [] Detail

## API Verbs
- [] Now playing (Movie)
- [] Upcoming (Movie)
- [] Top Rated (TV)
- [] Popular (TV, Movie)
- [] Airing Today (TV)
- [] TV Show Detail
- [] Movie Detail
- [] Search (TV, Movie)
```

<br>

#### Axios 설치

```bash
$ yarn add axios
```

<br>

#### 파일 생성

```bash
$ cd src
$ touch api.js
```

<br>

#### instance test

- api.js

```react
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://api.themoviedb.org/3/',
  params: {
    api_key: 'b1aff257ceb0cbcdd236cef217694a61',
    language: 'en-US'
  }
});

api.get('tv/popular');

export default api;
```

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from 'Components/App';
import './api';

ReactDOM.render(<App />, document.getElementById('root'));
```

> 1. 개발자 도구 > Network > `popular?api_key=…` 확인
> 2. `import './api';` 제거

<br>

#### 코드 수정

- api.js

```react
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://api.themoviedb.org/3/',
  params: {
    api_key: 'b1aff257ceb0cbcdd236cef217694a61',
    language: 'en-US'
  }
});

export const moviesApi = {
  nowPlaying: () => api.get('movie/now_playing'),
  upcoming: () => api.get('movie/upcoming'),
  popular: () => api.get('movie/popular')
};

export const tvApi = {
  topRated: () => api.get('tv/top_rated'),
  popular: () => api.get('tv/popular'),
  airingToday: () => api.get('tv/airing_today')
};
```

<br>

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie Discovery App.

## Screens
- [] Home
- [] TV
- [] Search
- [] Detail

## API Verbs
- [x] Now playing (Movie)
- [x] Upcoming (Movie)
- [x] Top Rated (TV)
- [x] Popular (TV, Movie)
- [x] Airing Today (TV)
- [] TV Show Detail
- [] Movie Detail
- [] Search (TV, Movie)
```

<br>

#### 코드 추가

- api.js

```react
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://api.themoviedb.org/3/',
  params: {
    api_key: 'b1aff257ceb0cbcdd236cef217694a61',
    language: 'en-US'
  }
});

export const moviesApi = {
  nowPlaying: () => api.get('movie/now_playing'),
  upcoming: () => api.get('movie/upcoming'),
  popular: () => api.get('movie/popular'),
  movieDetail: id => api.get(`movie/${id}`, {
    params: {
      append_to_response: 'videos'
    }
  }),
  search: term => api.get('search/movie', {
    params: {
      query: encodeURIComponent(term)
    }
  })
};

export const tvApi = {
  topRated: () => api.get('tv/top_rated'),
  popular: () => api.get('tv/popular'),
  airingToday: () => api.get('tv/airing_today'),
  showDetail: id => api.get(`tv/${id}`, {
    params: {
      append_to_response: 'videos'
    }
  }),
  search: term => api.get('search/tv', {
    params: {
      query: encodeURIComponent(term)
    }
  })
};
```

<br>

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie Discovery App.

## Screens
- [] Home
- [] TV
- [] Search
- [] Detail

## API Verbs
- [x] Now playing (Movie)
- [x] Upcoming (Movie)
- [x] Top Rated (TV)
- [x] Popular (TV, Movie)
- [x] Airing Today (TV)
- [x] TV Show Detail
- [x] Movie Detail
- [x] Search (TV, Movie)
```

------

<br>

<br>