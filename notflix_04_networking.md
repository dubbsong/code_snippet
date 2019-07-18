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

<br>

<br>

#### README 작성

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
- [] popular
- [] upcoming
- [] search
- [] movieDetail

## tvApi
- [] topRated
- [] popular
- [] airingToday
- [] search
- [] tvDetail
```

<br>

#### Axios 설치

```bash
$ yarn add axios@0.18.1
```

> 최신 axios 설치는 `$ yarn add axios`이다.
>
> 하지만 최신 axios에 버그가 있어 `@0.18.1`을 사용한다.

<br>

#### 컴포넌트 생성: `api`

```bash
$ cd src
$ touch api.js
```

<br>

#### 인스턴스 테스트

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
> 1. 개발자 도구
> 2. `Network` 탭
> 3. `now_playing?api_key=b1aff257ceb0cbcdd236cef217694a61&language=en-US` 클릭
> 4. `results`에서 데이터 확인
>    - 20개의 데이터가 객체의 형태로 배열에 담겨 있다.

> 확인 후, `import './api'`를 제거한다.

<br>

#### API 설정

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

## TODO
- [] Movie
- [] TV
- [] Search
- [] Detail

## movieApi
- [x] nowPlaying
- [x] popular
- [x] upcoming
- [] search
- [] movieDetail

## tvApi
- [x] topRated
- [x] popular
- [x] airingToday
- [] search
- [] tvDetail
```

<br>

#### API 설정: `search`, `detail`

- api.js

```react
...

export const movieApi = {
  ...
  search: term =>
    api.get('search/movie', {
      params: {
        query: encodeURIComponent(term)
      }
    }),
  movieDetail: id => api.get(`movie/${id}`)
};

export const tvApi = {
  ...
  search: term =>
    api.get('search/tv', {
      params: {
        query: encodeURIComponent(term)
      }
    }),
  tvDetail: id => api.get(`tv/${id}`)
};
```

<br>

- README.md

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
- [x] popular
- [x] upcoming
- [x] search
- [x] movieDetail

## tvApi
- [x] topRated
- [x] popular
- [x] airingToday
- [x] search
- [x] tvDetail
```

<br>

<br>

#### 디렉토리 구조

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

#### Commit

```bash
$ cd notflix
$ git status
$ git add .
$ git commit -m 'Set API Networking'
$ git push origin master
```

<br>

<br>