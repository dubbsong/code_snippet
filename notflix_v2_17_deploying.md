###### 코드 수정

- Router.js

```react
...
import {
  HashRouter as ...
} from 'react-router-dom';
...

...
```

<br>

###### Netlify

1. Netlify 가입 (`GitHub`으로 가입)
2. `New site from Git` 클릭
3. `Authorize Netlify by Netlify` 클릭
4. `Configure Netlify on GitHub` 클릭
5. ID 클릭
6. `Only select repositories` 체크
7. repository 선택
8. `Install` 클릭
9. password 입력
10. `clone_01` 클릭
11. `Branch to deploy`에서 `master` 선택
12. `Deploy site` 클릭
13. `Production: master@HEAD`를 클릭하면 `Deploy log` 확인 가능
    - `live`가 표시되면 완성쓰

14. `https://romantic-swanson-971944.netlify.com`를 package.json에 추가

```json
"homepage": "https://romantic-swanson-971944.netlify.com"
```

<br>

###### Commit

```bash
$ git add .
$ git commit -m 'Add Address'
$ git push origin master
```

<br>

<br>