###### 디렉토리 생성

```bash
$ cd Desktop
$ mkdir test_node
```

<br>

###### 파일 생성

```bash
$ touch index.html
$ touch server.js
```

<br>

###### 코드 작성

- index.html

```html
<html>
  <head>
    <title>Test NodeJS</title>
  </head>
  <body>
    <h2>OMB</h2>
  </body>
</html>
```

<br>

- server.js

```js
var http = require('http');
var fs = require('fs');
var url = require('url');

http.createServer(function(req, res) {
  // URL 뒤의 디렉토리 이름과 파일 이름을 파싱
  var pathname = url.parse(req.url).pathname;
  console.log('Request for ' + pathname + ' received.');
  
  // 파일 이름이 비어있다면, index.html로 설정
  if (pathname === '/') {
    pathname = '/index.html'
  }
  
  // 파일 읽기
  fs.readFile(pathname.substr(1), function(err, data) {
    if (err) {
      console.log(err);
      res.writeHead(404, { 'Content-Type': 'text/html' });
    } else {
      res.writeHead(200, { 'Content-Type': 'text/html' });
      res.write(data.toString());
    }
    res.end();
  });
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081');
```

<br>

###### 파일 실행

```bash
$ node server.js
```

> `http://127.0.0.1:8081`: OMB
>
> `http://127.0.0.1:8081/index.html`: OMB
>
> `http://127.0.0.1:8081/omb`: 404

<br>

<br>