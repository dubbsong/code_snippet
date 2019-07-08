#### 부가 설명

> github branch의 `gh-pages`는 코드를 실행한다.

<br>

#### CLI

```bash
$ yarn build
```

> terminal에 `"homepage": "http://myname.github.io/myapp"`이 표시된다.
>
> `build`라는 디렉토리가 생성된다.
>
> HTML, CSS, JS 등이 압축되어 저장된다.
>
> 최적화된다고 보면 된다.

<br>

#### 코드 추가

- package.json

```js
{
  ...
  "homepage": "http://dubbsong.github.io/movie_app"
}
```

> "http://`user name`.github.io/`project name`"

<br>

#### CLI

```bash
$ yarn build
$ yarn add --dev gh-pages
```

<br>

#### 코드 추가

```js
{
  ...
  "scripts": {
    ...
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  },
  ...
}
```

<br>

#### CLI

```bash
$ yarn run deploy
```

> Username과 Password를 입력한다.
>
> 약 2-3분 내에 `https://dubbsong.github.io/test_app`으로 배포된다.

<br>

<br>