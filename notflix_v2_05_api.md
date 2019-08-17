###### THE MOVIE DB API 참조

1. [TMDB](https://www.themoviedb.org/) 이동
2. `profile` 클릭
3. `settings` 클릭
4. `API` 클릭
5. `API Key` 복사
6. `developers.themoviedb.org` 클릭
7. `Movies` 클릭
8. `Get Now Playing` 클릭
9. `Definition` 확인
10. `Try it out` 클릭
11. `API Key` 입력
12. `SEND REQUEST` 클릭
13. `Response` 데이터 확인
14. `url` 확인

> `https://api.themoviedb.org/3/` \+
>
> `movie/now_playing` \+
>
> `?api_key=b1aff257ceb0cbcdd236cef217694a61` \+
>
> `&language=en-US` \+
>
> `&page=1`

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
    api_key: '자신의 api key 입력',
    language: 'en-US'
  }
});

api.get('movie/now_playing');

export default api;
```

- index.js

```react
...
import './api'; // 확인 후 제거

...
```

> 개발자 도구 `Network` 탭에서 `now_playing` 데이터(`result`) 확인
>
> `import './api';` 제거
>
> `api.get('movie/now_playing');` 제거
>
> `export default api;` 제거

<br>

<br>

###### API 설정: `movieApi` / `tvApi`

- api.js

```react
...

const api = axios.create({
  ...
});

export const movieApi = {
  trending: () => api.get('trending/movie/week'),
  nowPlaying: () => api.get('movie/now_playing'),
  topRated: () => api.get('movie/top_rated'),
  upcoming: () => api.get('movie/upcoming'),
  search: word =>
    api.get('search/movie', {
      params: {
        query: encodeURIComponent(word)
      }
    }),
  movieDetail: id => api.get(`movie/${id}`)
};

export const tvApi = {
  trending: () => api.get('trending/tv/week'),
  onTheAir: () => api.get('tv/on_the_air'),
  popular: () => api.get('tv/popular'),
  topRated: () => api.get('tv/top_rated'),
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

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Set API'
$ git push origin master
```

<br>

<br>