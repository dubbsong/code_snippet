###### THE MOVIE DB

1. [TMDB](https://www.themoviedb.org/) 회원가입
2. `profile` 클릭
3. `settings` 클릭
4. `API` 클릭
5. `Request an API Key`의 `click here` 클릭
6. `Developer` 클릭
7. `Accept` 클릭
8. 개인정보 입력
   - 영어 주소로 입력
9. `API Key` 복사
10. `Documentation`의 `developers.themoviedb.org` 클릭
11. `MOVIES` 클릭
12. `Get Now Playing` 클릭
13. `Try it out` 클릭
14. `Your TMDb API Key`에 `API Key` 붙여넣기
15. `SEND REQUEST` 클릭
    - 객체 데이터를 확인할 수 있다.

<br>

###### README 작성

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## TODO
- [] Movie
- [] TV
- [] Search
- [] Detail

## movieApi
- [] nowPlaying
- [] search
- [] movieDetail

## tvApi
- [] topRated
- [] search
- [] tvDetail
```

<br>

###### Axios 설치

```bash
$ yarn add axios@0.18.1
```

<br>

###### 컴포넌트 생성: `api`

```bash
$ cd src
$ touch api.js
```

<br>

###### Instance 확인

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
import App from './Components/App';
import './api';	// 확인 후 제거

ReactDOM.render(<App />, document.getElementById('root'));
```

> 1. 개발자 도구 `Network` 탭
> 2. `now_playing?api_key=...` 클릭
> 3. `results` 데이터 확인 (20개)
>
> `import './api';`를 제거한다.

<br>

###### API 설정: `nowPlaying` / `topRated`

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

export const movieApi = {
  nowPlaying: () => api.get('movie/now_playing')
};

export const tvApi = {
  topRated: () => api.get('tv/top_rated')
};

```

<br>

###### README 체크

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## TODO
- [] Movie
- [] TV
- [] Search
- [] Detail

## movieApi
- [x] nowPlaying
- [] search
- [] movieDetail

## tvApi
- [x] topRated
- [] search
- [] tvDetail
```

<br>

###### API 설정: `search` / `detail`

- api.js

```react
...

export const movieApi = {
  ...
  search: word =>
    api.get('search/movie', {
      params: {
        query: encodeURIComponent(word)
      }
    }),
  movieDetail: id => api.get(`movie/${id}`)
};

export const tvApi = {
  ...
  search: word =>
    api.get('search/tv', {
      params: {
        query: encodeURIComponent(word)
      }
    }),
  tvDetail: id => api.get(`tv/${id}`)
};
```

<br>

###### README 체크

```markdown
# NOTFLIX
Learning React and ES6 by building a Movie App.

## TODO
- [] Movie
- [] TV
- [] Search
- [] Detail

## movieApi
- [x] nowPlaying
- [x] search
- [x] movieDetail

## tvApi
- [x] topRated
- [x] search
- [x] tvDetail
```

<br>

<br>

###### 현재 디렉토리 구조

```bash
src
  ├─ Components
  │   ├─ App.js
  │   ├─ Router.js
  │   ├─ Nav.js
  │   └─ GlobalStyle.js
  ├─ Routes
  │   ├─ Movie.js
  │   ├─ TV.js
  │   ├─ Search.js
  │   └─ Detail.js
  ├─ assets
  │   └─ img
  │       └─ logo.png
  ├─ api.js
  └─ index.js
```

<br>

<br>