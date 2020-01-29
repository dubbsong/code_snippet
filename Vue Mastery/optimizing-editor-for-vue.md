#### Vetur 설치

- `vue` 단축키 사용 가능

<br>

#### Emmet 설치 후 설정

- settings.json

```json
"emmet.includeLanguages": {
  "vue": "html"
}
```

<br>

#### ESLint 설치 후 설정

- \.eslintrc.js

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  extends: [
    "plugin:vue/essential",
    "plugin:prettier/recommended",  // 추가하는 코드
    "@vue/prettier"
  ],
  rules: {
    "no-console": process.env.NODE_ENV === "production" ? "error" : "off",
    "no-debugger": process.env.NODE_ENV === "production" ? "error" : "off"
  },
  parserOptions: {
    parser: "babel-eslint"
  }
}
```

<br>

#### Prettier 설정

- 파일 생성
  - `.prettierrc.js`
- \.prettierrc.js

```js
module.exports = {
  singleQuote: true,
  semi: false
};
```

<br>

#### Vetur의 linting 기능 끄기

- settings.json

```json
"vetur.validation.template": false,
```

<br>

#### autoFix true로 설정

```json
"eslint.validate": [
  {
    "language": "vue",
    "autoFix": true
  },
  {
    "language": "html",
    "autoFix": true
  },
  {
    "language": "javascript",
    "autoFix": true
  }
],
"eslint.autoFixOnSave": true,
"editor.formatOnSave": true
```

<br>

<br>