#### DB 데이터 가져오기

1. [The Movie DB](https://www.themoviedb.org/) 회원가입
2. profile 클릭
3. settings 클릭
4. API 클릭
5. Request an API Key의 click here 클릭
6. Developer 선택
7. Accept 클릭
8. 개인정보 입력 (영어 주소 필요)
9. API Key 복사
10. Documentation의 developers.themoviedb.org 클릭
11. MOVIES 클릭
12. Get Now Playing 클릭
13. Try it out 클릭
14. Your TMDb API Key에 복사한 API Key 붙여넣기
15. SEND REQUEST 클릭
    - 객체 형태의 데이터를 확인할 수 있다.
    - 버튼 옆의 URL로 요청을 만들 것이다.
      - `https://api.themoviedb.org/3/movie/now_playing?api_key=b1aff257ceb0cbcdd236cef217694a61&language=en-US&page=1`

<br>

#### README 작성

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## Todo
[] Home
[] TV
[] Search
[] Detail

## API Verbs
[] Now Playing (Movie)
[] Popular (Movie)
[] Upcoming (Movie)
[] Top Rated (TV)
[] Popular (TV)
[] Airing Today (TV)
[] Search (Movie, TV)
[] Movie Detail
[] TV Detail
```

<br>

#### Axios 설치

```bash
$ yarn add axios
```

> 나중에 `Unauthorized` 에러가 발생하므로, `$ yarn add axios@0.18.1`로 설치한다.

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

api.get('movie/now_playing');

export default api;
```

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from 'Components/App';
import './api';	// 테스트 후 제거

ReactDOM.render(<App />, document.getElementById('root'));
```

> 개발자 도구의 Network에서 `now_playing?api_key=…`을 확인할 수 있다.
>
> 확인 후, `import './api'`를 제거한다.

<br>

#### 코드 추가 (for Movie, TV API)

- api.js

```react
import axios from 'axios';

const api = axios.create({
  ...
});

export const movieApi = {
  nowPlaying: () => api.get('movie/now_playing'),
  popular: () => api.get('movie/popular'),
  upcoming: () => api.get('movie/upcoming')
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
Learning React and ES6 by building a Movie App.

## Todo
[] Home
[] TV
[] Search
[] Detail

## API Verbs
[x] Now Playing (Movie)
[x] Popular (Movie)
[x] Upcoming (Movie)
[x] Top Rated (TV)
[x] Popular (TV)
[x] Airing Today (TV)
[] Search (Movie, TV)
[] Movie Detail
[] TV Detail
```

<br>

#### 코드 추가 (for Search, Detail API)

- api.js

```react
...

export const movieApi = {
  ...
  upcoming: () => api.get('movie/upcoming'),
  search: term =>
    api.get('search/movie', {
      params: {
        query: encodeURIComponent(term)
      }
    }),
  movieDetail: id =>
    api.get(`movie/${id}`, {
      params: {
        append_to_response: 'videos'
      }
    })
};

export const tvApi = {
  ...
  airingToday: () => api.get('tv/airing_today'),
  search: term =>
    api.get('search/tv', {
      params: {
        query: encodeURIComponent(term)
      }
    }),
  tvDetail: id =>
    api.get(`tv/${id}`, {
      params: {
        append_to_response: 'videos'
      }
    })
};
```

<br>

- README.md

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## Todo
[] Home
[] TV
[] Search
[] Detail

## API Verbs
[x] Now Playing (Movie)
[x] Popular (Movie)
[x] Upcoming (Movie)
[x] Top Rated (TV)
[x] Popular (TV)
[x] Airing Today (TV)
[x] Search (Movie, TV)
[x] Movie Detail (Movie)
[x] TV Detail (TV)
```

<br>

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set API Networking'
$ git push origin master
```

------

<br>

<br>